# The Rootless Computing Manifesto

Version 0.1 — 2026-05-12

A rootless application has no origin server. There is no canonical instance, no privileged runtime coordinator, no host you can take offline. The repository that contains the app is also the way the app is distributed. Every browser that loads the page is an equal peer; every fork is an equally legitimate instance. The server, when it exists at all, is a convenience that the application can outgrow without changing what it is.

This manifesto names that pattern and lays out the principles that keep it coherent.

## Principles

1. **Rootless apps have no origin server.**

   Coordination, when needed, happens between peers — not through a host that can be subpoenaed, sunsetted, or starved of funding. The absence of an origin is not an absence of capability; it is the absence of a single point of capture.

2. **The repository is the distribution.**

   Cloning the repo, opening the artifact, or visiting any fork's Pages URL each yield a working application. There is no install step that depends on private infrastructure. If the artifact survives, the app survives.

3. **Backend work happens at build time, not request time.**

   What used to be a runtime database query becomes a baked file. What used to be a server function becomes a precomputed table. This is the Bake-Time Backend pattern: CI does the work once so every browser can do it for free, forever.

4. **Peers are the runtime.**

   When an app needs coordination — a shared cursor, a vote tally, a live presence indicator — it asks the other browsers in the room, not a server in a region. WebRTC, CRDTs, and small signaling shims are enough for the vast majority of what was once "real-time backend."

5. **Trust is proven, not asserted.**

   Eligibility, uniqueness, and authority are demonstrated with cryptographic proofs the receiver can verify locally. A rootless app does not say "trust me, I checked"; it produces an artifact anyone can check. Zero-knowledge membership proofs and nullifiers replace session tokens and admin endpoints.

6. **The user's machine is the database.**

   Persistence lives in the browser: IndexedDB for documents, DuckDB-WASM for analytical queries, the file system access API for exports. The user owns their data because the data never leaves their machine unless they choose to share it.

7. **Physical space can carry state.** *(optional, advanced)*

   Some rootless apps anchor coordination to the physical world: AprilTags or other fiducials let phones agree on geometry, identity, or order without a network round-trip to a server. The room itself becomes part of the protocol.

8. **A rootless app must be forkable into existence on someone else's account in under five minutes.**

   "Fork, enable Pages, done" is the test. If standing up your own instance requires secrets, DNS, paid services, or operator knowledge, the app is not rootless — it is a hosted app with a public repo.

9. **Rootless does not mean trustless. It means uncoordinated.**

   A rootless app may rely on trusted code, trusted cryptography, trusted hardware, or trusted humans. What it does not rely on is a trusted coordinator. Removing the coordinator is the design move; removing trust altogether is a different project, and a much harder one.

10. **Progressive enhancement, not regressive purity.**

    A rootless app may accept a server — for relays, for storage, for richer presence — but it must not require one. If the server disappears tomorrow, the app keeps working with reduced features rather than ceasing to exist. Purity is a tactic, not a virtue.

## How this came to be

This term arrived while I was shipping [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll), a static, anonymous live-polling app with CRDT sync, zero-knowledge one-vote proofs, and local analytics. It is day 12 of a 31-day month in May 2026 in which I am open-sourcing one app per day in public. By day ten the apps had a shape I could not name with the available vocabulary. "Static site" undersold the runtime compute. "Serverless" was misleading — those apps still have servers. "P2P" was too broad and dragged in twenty years of unrelated baggage. I needed a word for *apps that assume no origin, treat the repo as the distribution, and let peers do the coordinating*. I borrowed "rootless" from the containers world, where it already means "runs without a privileged root daemon," and the analogy carried.

## What rootless computing is not

It is not **blockchain or web3**. Rootless apps do not need consensus, do not have native tokens, and do not require global agreement on order. Most rootless apps have no chain anywhere.

It is not **serverless**. Serverless is a billing and deployment model — the servers still exist, they are just rented by the millisecond. Rootless removes the server entirely from the application's critical path.

It is not **JAMstack**. JAMstack is a build-and-deploy pattern that produces static artifacts which then call APIs at runtime. Rootless apps may share JAMstack's static-first instinct, but they do not depend on runtime APIs to function.

It is not **just a static site**. Static sites are the ancestor. A rootless app inherits the static site's deployment story and adds browser-resident compute, peer coordination, cryptographic eligibility, and optional physical-world anchoring on top.

## Invitation

This document is version 0.1. It is wrong in places I cannot yet see. If you have built something that fits this shape, please add it to [examples](docs/examples.md). If you think a principle is redundant, weak, or missing, open an issue and argue for the change. If you want to fork the manifesto entirely and run a competing definition, that is also fine — the manifesto is itself a rootless artifact, and there is no canonical instance.
