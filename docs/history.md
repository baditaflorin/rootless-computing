# History

## Origin

The term *rootless computing* was coined by [Florin Bădiță (Vivi)](https://badita.lv3.org) in May 2026, during a personal challenge to open-source one application per day for 31 days.

By around day 10 of that month, the apps shipped — a mix of mesh tools for teams (anonymous polls, retro boards, pomodoro rooms, standup batons), situated apps using AprilTag fiducials, and the immediate predecessor [anon-conf-poll](https://github.com/baditaflorin/anon-conf-poll) — had developed a recognizable shape that the available vocabulary failed to capture cleanly.

"Static site" undersold the runtime work (DuckDB-WASM analytics, Yjs CRDTs, Semaphore-style ZK proofs). "Serverless" was misleading — those apps were not running on rented compute, they were running in browsers. "P2P" was too broad and historically loaded. "Decentralized" had been captured by the blockchain world.

A name was needed for *apps that assume no origin, treat the repository as the distribution, and let peers do the coordinating*. The name was borrowed from rootless containers — runtimes that operate without a privileged root daemon — because the analogy was tight: in both cases, the privileged coordinator turned out to be historical accident rather than necessity.

The manifesto was written on day 12, while the build-in-public month was still in progress. The 31 apps from that month form the seed of the [examples list](examples.md).

## Changelog

### v0.1.1 — 2026-05-12 (same-day correction)

Added principle 4: *"The artifact carries compute, not just content."* The original v0.1 draft mentioned WASM only in passing under principles 3 and 6, but WASM is what separates rootless apps from plain static sites and from JAMstack — it deserves its own principle. Principles formerly numbered 4–10 are now 5–11. Example entries updated to reflect the renumbering, and WASM-heavy apps now list principle 4 and a `WASM` tag.

### v0.1 — 2026-05-12

Initial publication.

- Manifesto with 10 principles
- Four-layer vocabulary (Rootless-First, Rootless Apps, Rootless Runtime, the Manifesto itself)
- FAQ, adjacent-work survey, examples seed
- Hand-rolled static site under `docs/`, no build step
- Pages deploy workflow

Future versions will be dated and listed here as they are published. The manifesto is meant to evolve; corrections, additions, and disputes are tracked as ordinary git history in this repository.
