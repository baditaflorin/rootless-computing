# Principles, expanded

The [manifesto](../MANIFESTO.md) states the principles tersely. This page expands each one with rationale, prior art, and concrete consequences. The numbering matches the manifesto exactly.

## 1. Rootless apps have no origin server

A rootless app has no host you can subpoena, sunset, or starve. There is no "production" deployment that is more real than your fork. The application's identity is the artifact, not the URL.

The consequence at the architectural level: there is no privileged client. Every browser holds the entire app and runs the same code. The author cannot ship a feature flag that only their copy honors, because there is no central authority to consult.

**Prior art:** This generalizes the static-site instinct and absorbs lessons from local-first software and Beaker Browser's "dat" model. Rootless tightens the constraint: not just *runs without a server*, but *has no privileged coordinator anywhere*.

## 2. The repository is the distribution

The unit of shipping is a git repository whose contents render to a working app when served. There is no separate "release pipeline" producing artifacts that the repo does not contain. Cloning the repo is sufficient to run the app; visiting any fork's Pages URL is sufficient to use it.

This is what makes rootless apps survive their authors. A fork is not a copy of the source — it *is* the app, in every operational sense.

## 3. Backend work happens at build time, not request time

Anything that looks like a database query, a precomputed aggregation, or a server function should be resolved at CI time and committed as a static file. Browsers then read the file directly.

This is the **Bake-Time Backend** pattern. The economic argument is overwhelming: a baked artifact serves a million users for the cost of serving one. The architectural argument is stronger still: a baked artifact has no failure mode beyond "the static host is down," which is the same failure mode as the rest of the site.

**Concrete:** If your app needs "the list of valid voter Ethereum addresses," bake the Merkle root at CI time. If your app needs "the top 100 GitHub repos in category X," scrape and bake nightly. If your app needs FTS over 100k documents, bake a DuckDB file and ship it.

## 4. The artifact carries compute, not just content

WebAssembly is the second leg of the rootless runtime, after the static artifact itself. It lets the browser execute the kind of code that used to live behind an API: database engines, media transcoders, cryptographic provers, machine-learning inference, document converters. The `.wasm` file is shipped from the same static host as the HTML — there is no separate service tier and no separate failure mode.

**Capabilities that are routine in 2026, not exotic:**

- **Real database engines in the browser.** [DuckDB-WASM](https://duckdb.org/docs/api/wasm/overview) runs analytical SQL against multi-gigabyte parquet files loaded over HTTP range requests. SQLite via [sql.js](https://sql.js.org) and [wa-sqlite](https://github.com/rhashimoto/wa-sqlite) gives a full transactional engine. [PGlite](https://pglite.dev) is Postgres compiled to WASM, running entirely in the page.
- **Media and document tooling.** [FFmpeg.wasm](https://ffmpegwasm.netlify.app) transcodes video client-side. [libvips](https://github.com/kleisauke/wasm-vips), [OpenCV.js](https://docs.opencv.org/4.x/d5/d10/tutorial_js_root.html), [libheif](https://github.com/strukturag/libheif), and [MediaPipe](https://developers.google.com/mediapipe) handle imaging and pose tasks that used to require an upload-and-process pipeline. [PDFium](https://github.com/hyzyla/pdfium) and [mupdf.js](https://github.com/ArtifexSoftware/mupdf.js) render and parse PDFs without a server.
- **Cryptography and zero-knowledge.** [snarkjs](https://github.com/iden3/snarkjs) generates Groth16 and Plonk proofs in the browser; [Halo2](https://github.com/zcash/halo2) and [Noir](https://noir-lang.org) provers compile to WASM. Hashes, signatures, and post-quantum primitives run via WASM ports of audited C/Rust libraries (libsodium, BoringSSL builds, oqs).
- **Machine-learning inference.** [ONNX Runtime Web](https://onnxruntime.ai/docs/tutorials/web/) and TensorFlow.js's WASM backend run model inference locally. [transformers.js](https://huggingface.co/docs/transformers.js) runs quantized transformer models — embeddings, sentiment, summarization — on user input that never leaves the device. [llama.cpp WASM builds](https://github.com/ngxson/wllama) run small chat models on a phone.
- **Compilers and language runtimes in the page.** [Pyodide](https://pyodide.org) brings CPython with NumPy and pandas. [Ruby (ruby.wasm)](https://github.com/ruby/ruby.wasm), [PHP (php-wasm)](https://github.com/WordPress/wordpress-playground), [Lua](https://github.com/ceifa/wasmoon), and Go all run client-side. [esbuild-wasm](https://github.com/evanw/esbuild) and [SWC](https://github.com/swc-project/swc) do TypeScript and JSX transformation in-browser.

**Three properties make this load-bearing for rootless apps:**

1. **Same-origin delivery.** The `.wasm` binary is a static file in the repository, served by the same Pages instance as the HTML. No second hop, no separate auth, no separate failure mode. If the page loads, the engine loads.
2. **Determinism.** WebAssembly's execution model is portable across browsers and architectures (modulo a small set of well-specified float behaviors). The result a peer computes locally is the result every other peer would have computed. This pairs directly with [principle 6](#6-trust-is-proven-not-asserted) — proofs and votes are only meaningful if every participant agrees on what the program does.
3. **Performance.** WASM runs within 20–50% of native for most workloads. With COOP/COEP headers (which GitHub Pages can set via a `<meta>` `Cross-Origin-Opener-Policy` setup or via `_headers` on Cloudflare Pages / Netlify forks), `SharedArrayBuffer` and multi-threading become available, recovering most of the rest. SIMD instructions are supported in every shipping browser.

**Combination with the rest of the manifesto.**

This principle compounds with [principle 3](#3-backend-work-happens-at-build-time-not-request-time) (Bake-Time Backend) to give rootless apps their reach: BTB precomputes what can be precomputed at CI time; WASM lets the browser do everything else. Together they replace the pattern "client calls server function, gets response" with "client loads static file, runs it locally." It compounds with [principle 7](#7-the-users-machine-is-the-database) by making it tractable to query that local data — DuckDB-WASM is the canonical example. And it compounds with [principle 6](#6-trust-is-proven-not-asserted) by making proof generation a client capability, not a server-mediated one.

**What does not yet work well.**

WASM is not free. Cold-load times for large engines (FFmpeg.wasm ≈ 25 MB, DuckDB-WASM ≈ 5 MB, transformers.js models ≈ tens to hundreds of MB) matter on mobile and on first visit. WASM cannot use GPU directly; you need WebGPU for that, and the two are bridged by libraries like ONNX Runtime Web's WebGPU backend. Some libraries that look "WASM-ready" (notably anything depending on `pthread` without COOP/COEP) need a hosting setup beyond what plain GitHub Pages provides. None of this defeats the principle; it shapes which apps are sensible candidates.

## 5. Peers are the runtime

When a rootless app needs synchronous coordination — a cursor, a vote, a presence indicator — it asks the browsers in the room, not a server in a region. WebRTC handles transport; CRDTs handle merge; a small public signaling shim handles introductions.

The signaling shim is the one place where rootless apps lean on shared infrastructure. This is acceptable because: (a) signaling is stateless and replaceable, (b) the data flowing through it is opaque and short-lived, and (c) for many use cases a QR code or copy-paste link is a sufficient signal channel.

**Prior art:** This descends directly from the WebRTC ecosystem, Yjs and Automerge, and the broader peer-to-peer web tradition. Rootless adds: peer coordination is not a feature, it is the default.

## 6. Trust is proven, not asserted

In a rootless app, eligibility ("this voter is on the allowlist"), uniqueness ("this voter has not voted yet"), and authority ("this command came from a holder of role X") are demonstrated with cryptographic proofs that any other peer can verify locally.

Zero-knowledge membership proofs (Semaphore-style) and nullifiers are the most common building blocks. The user produces a proof that they belong to a set baked into the artifact; the proof reveals nothing about *which* member they are, but exposes a unique nullifier that prevents double-action.

**Concrete:** [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll) proves "this ballot came from a member of the conference attendee list" without identifying which attendee. The nullifier guarantees one ballot per attendee. No server is involved in the verification.

## 7. The user's machine is the database

Persistence in a rootless app lives in the browser. IndexedDB and the Origin Private File System hold documents. DuckDB-WASM runs analytical queries against multi-gigabyte parquet files loaded over HTTP range requests. The File System Access API lets the user export to disk.

This is liberating and lonely in equal measure. The user owns their data — but they also have to back it up themselves. A rootless app should make export trivial and import obvious.

## 8. Physical space can carry state *(optional, advanced)*

A subset of rootless apps — call them *situated* — use the physical world as part of their protocol. AprilTags, ArUco markers, or other fiducials let phones agree on geometry, identity, or order without consulting a server. The room becomes a coordination substrate.

This is the most experimental principle. Many rootless apps will not use physical anchors. But the apps that do — group photo coordination, hands-free retro voting, mesh standup baton-passing — get capabilities that are otherwise impossible without a server.

## 9. A rootless app must be forkable into existence on someone else's account in under five minutes

This is the operational test. Fork the repository, enable Pages on the fork, wait for the action to complete, open the URL — done. If standing up your own instance requires secrets in env vars, DNS configuration, paid service signups, or operator-only knowledge, the app is not rootless. It is a hosted app that happens to publish its source.

The five-minute budget is not arbitrary. It is roughly the threshold below which a curious user will try it and above which they will not.

## 10. Rootless does not mean trustless. It means uncoordinated

This is the principle most likely to be misread. A rootless app may rely on trusted code (the artifact itself), trusted cryptography (the proofs), trusted hardware (the user's device), and trusted humans (the maintainers who keep the repo honest). What it does not rely on is a *trusted coordinator* — a single host whose continued cooperation is required for the app to function.

Removing the coordinator is the design move. Removing trust altogether is a different project, with a much larger blast radius and a much harder threat model. Rootless is not crypto-libertarianism; it is the narrower, more practical observation that *most coordination did not actually need a coordinator.*

## 11. Progressive enhancement, not regressive purity

A rootless app may accept a server. It may benefit from one. It may even encourage you to run one. What it must not do is *require* one. The acid test: if every server affiliated with the app disappears overnight, does the app keep working with reduced features, or does it stop being an app?

If reduced features: rootless. If stops being an app: hosted.

The point of rootlessness is not to refuse infrastructure. It is to refuse *dependence* on infrastructure.
