# Vocabulary

Rootless computing is a stack of four ideas. Each names a distinct layer; conflating them muddies all four.

## 1. Rootless-First

**Gloss:** The design stance. A sibling to *local-first* and *offline-first*.

Rootless-first means starting from the assumption that no server exists, and treating any server you eventually add as a progressive enhancement rather than a foundation. The default execution context is a browser holding a static artifact. Coordination, persistence, and verification are designed to work in that context; a relay or storage backend may improve the experience but cannot be load-bearing.

**Example:** [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll) designs voting around CRDT merge and ZK proofs first; the optional signaling relay only accelerates peer discovery and can be replaced by a QR code.

**Not to be confused with:**
- *Offline-first* — which assumes a server exists but might be unreachable.
- *Local-first* — which centers data ownership and sync, but typically still imagines a sync server in the loop.

## 2. Rootless Apps

**Gloss:** The category. The things you can point at and say "this one."

A rootless app is an application with no origin server, no canonical instance, and no privileged runtime coordinator. Every browser that loads it is an equal peer. Every fork of the repository, deployed to any host (or no host), is an equally legitimate copy. Liveness of the app does not depend on the liveness of the author.

**Example:** [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll) is a rootless app. If the author deletes the GitHub account, every existing fork still runs.

**Not to be confused with:**
- A *static site* — which is a rootless app's ancestor but typically does no runtime computation beyond rendering.
- A *self-hosted app* — which still has an origin server; you just happen to run it.

## 3. Rootless Runtime

**Gloss:** The technical architecture. The execution topology of a rootless app.

The rootless runtime is the set of pieces that make rootless apps possible: browser-resident compute (WASM, DuckDB-WASM, ZK circuits), baked artifacts produced at CI time (the [Bake-Time Backend](https://github.com/baditaflorin/rootless-computing) pattern), peer-to-peer transport (WebRTC + signaling), local-first storage (IndexedDB, OPFS), and — for situated apps — physical-world anchors like AprilTags. A given rootless app uses some subset of these.

**Example:** [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll)'s runtime is: Pages-served artifact + DuckDB-WASM for tallying + Yjs CRDT for sync + Semaphore-style ZK proofs for eligibility + IndexedDB for local persistence.

**Not to be confused with:**
- The *runtime* of a hosted app (which means "the server process"). Here, the runtime is distributed across all participating browsers.

## 4. The Rootless Computing Manifesto

**Gloss:** The foundational document.

The manifesto is a versioned, dated, citable text that codifies the principles distinguishing rootless apps from their neighbors. It is itself a rootless artifact: published in a git repository, served as a static page, forkable into an alternative manifesto if you disagree with this one. It is the answer to "what are we actually claiming?"

**Example:** The file you started with — [MANIFESTO.md](../MANIFESTO.md) v0.1, dated 2026-05-12.

**Not to be confused with:**
- A *spec* — the manifesto does not normatively define protocols. It defines a category.
- A *license* — it does not grant or restrict rights. See [LICENSE](../LICENSE).

## How the layers relate

```
                 ┌──────────────────────────────────────┐
                 │  The Rootless Computing Manifesto    │  ← the document
                 │  (codifies the principles below)     │
                 └──────────────────────────────────────┘
                                  │ defines
                                  ▼
                 ┌──────────────────────────────────────┐
                 │  Rootless-First (design stance)      │  ← the philosophy
                 └──────────────────────────────────────┘
                                  │ produces
                                  ▼
                 ┌──────────────────────────────────────┐
                 │  Rootless Apps (the category)        │  ← the things
                 └──────────────────────────────────────┘
                                  │ run on
                                  ▼
                 ┌──────────────────────────────────────┐
                 │  Rootless Runtime (the architecture) │  ← the how
                 └──────────────────────────────────────┘
```

## How it composes with adjacent vocabulary

The author of this manifesto has previously named several adjacent patterns. Rootless computing layers on top of them rather than replacing them.

| Adjacent term | What it names | Relationship to rootless |
|---------------|---------------|--------------------------|
| **Pages-Native** | Deployment axis — *where* the app lives (in a repo, served from Pages). | Most rootless apps are Pages-Native, but a rootless app could also be distributed as an IPFS bundle or a downloadable zip. |
| **Bake-Time Backend (BTB)** | Resolution axis — *when* "server work" happens (at CI, not at request time). | Most rootless apps use BTB because it eliminates the need for runtime APIs. |
| **Mesh Apps / Situated Mesh** | Runtime topology with WebRTC + physical anchors. | A common runtime *for* rootless apps, especially situated ones. |

A rootless app is typically Pages-Native, often uses a Bake-Time Backend, and frequently has a Mesh runtime — but none of those is required. Rootlessness is the principle; the others are implementation choices.
