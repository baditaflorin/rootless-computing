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

## 4. Peers are the runtime

When a rootless app needs synchronous coordination — a cursor, a vote, a presence indicator — it asks the browsers in the room, not a server in a region. WebRTC handles transport; CRDTs handle merge; a small public signaling shim handles introductions.

The signaling shim is the one place where rootless apps lean on shared infrastructure. This is acceptable because: (a) signaling is stateless and replaceable, (b) the data flowing through it is opaque and short-lived, and (c) for many use cases a QR code or copy-paste link is a sufficient signal channel.

**Prior art:** This descends directly from the WebRTC ecosystem, Yjs and Automerge, and the broader peer-to-peer web tradition. Rootless adds: peer coordination is not a feature, it is the default.

## 5. Trust is proven, not asserted

In a rootless app, eligibility ("this voter is on the allowlist"), uniqueness ("this voter has not voted yet"), and authority ("this command came from a holder of role X") are demonstrated with cryptographic proofs that any other peer can verify locally.

Zero-knowledge membership proofs (Semaphore-style) and nullifiers are the most common building blocks. The user produces a proof that they belong to a set baked into the artifact; the proof reveals nothing about *which* member they are, but exposes a unique nullifier that prevents double-action.

**Concrete:** [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll) proves "this ballot came from a member of the conference attendee list" without identifying which attendee. The nullifier guarantees one ballot per attendee. No server is involved in the verification.

## 6. The user's machine is the database

Persistence in a rootless app lives in the browser. IndexedDB and the Origin Private File System hold documents. DuckDB-WASM runs analytical queries against multi-gigabyte parquet files loaded over HTTP range requests. The File System Access API lets the user export to disk.

This is liberating and lonely in equal measure. The user owns their data — but they also have to back it up themselves. A rootless app should make export trivial and import obvious.

## 7. Physical space can carry state *(optional, advanced)*

A subset of rootless apps — call them *situated* — use the physical world as part of their protocol. AprilTags, ArUco markers, or other fiducials let phones agree on geometry, identity, or order without consulting a server. The room becomes a coordination substrate.

This is the most experimental principle. Many rootless apps will not use physical anchors. But the apps that do — group photo coordination, hands-free retro voting, mesh standup baton-passing — get capabilities that are otherwise impossible without a server.

## 8. A rootless app must be forkable into existence on someone else's account in under five minutes

This is the operational test. Fork the repository, enable Pages on the fork, wait for the action to complete, open the URL — done. If standing up your own instance requires secrets in env vars, DNS configuration, paid service signups, or operator-only knowledge, the app is not rootless. It is a hosted app that happens to publish its source.

The five-minute budget is not arbitrary. It is roughly the threshold below which a curious user will try it and above which they will not.

## 9. Rootless does not mean trustless. It means uncoordinated

This is the principle most likely to be misread. A rootless app may rely on trusted code (the artifact itself), trusted cryptography (the proofs), trusted hardware (the user's device), and trusted humans (the maintainers who keep the repo honest). What it does not rely on is a *trusted coordinator* — a single host whose continued cooperation is required for the app to function.

Removing the coordinator is the design move. Removing trust altogether is a different project, with a much larger blast radius and a much harder threat model. Rootless is not crypto-libertarianism; it is the narrower, more practical observation that *most coordination did not actually need a coordinator.*

## 10. Progressive enhancement, not regressive purity

A rootless app may accept a server. It may benefit from one. It may even encourage you to run one. What it must not do is *require* one. The acid test: if every server affiliated with the app disappears overnight, does the app keep working with reduced features, or does it stop being an app?

If reduced features: rootless. If stops being an app: hosted.

The point of rootlessness is not to refuse infrastructure. It is to refuse *dependence* on infrastructure.
