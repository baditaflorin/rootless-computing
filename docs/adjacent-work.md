# Adjacent work

Rootless computing is not the first attempt to name "applications that don't need a server in the middle." It is the most recent, and it sits at a specific intersection that the prior names individually miss. This page summarizes the prior work honestly and locates rootless relative to it.

## Local-first software

**Summary.** The Ink & Switch essay "Local-First Software: You own your data, in spite of the cloud" ([inkandswitch.com/local-first](https://www.inkandswitch.com/local-first/), 2019) names seven ideals: no spinners, multi-device sync, offline-by-default, collaboration without a central server, longevity beyond any vendor, security and privacy by default, and user-owned data. The essay frames CRDTs as the enabling technology.

**Overlap and difference.** Rootless computing inherits local-first's user-ownership ethic almost completely. The difference is the framing axis: local-first foregrounds *data*; rootless foregrounds *deployment and coordination*. Many apps are both. Some local-first apps still rely on a sync service (Automerge's relay) and so are not rootless. Some rootless apps hold no user data and so are not meaningfully local-first.

## JAMstack

**Summary.** A deployment pattern coined by Mathias Biilmann in 2015: JavaScript + APIs + Markup, served from CDN. The site itself is static; dynamic features come from runtime API calls.

**Overlap and difference.** Rootless apps share JAMstack's static-first instinct and benefit from the same CDN economics. Rootless rejects the "A" — the runtime API call to a managed backend. Where JAMstack defers backend work to runtime APIs, rootless defers it to *build-time bakes* and *peer coordination*.

## The IndieWeb

**Summary.** A movement and set of conventions ([indieweb.org](https://indieweb.org)) advocating personal ownership of one's content via self-hosted sites, with interop protocols (Webmention, Microformats, IndieAuth) for federation.

**Overlap and difference.** IndieWeb shares rootless's anti-platform ethic but assumes you *do* run a server (your own). Rootless removes the server entirely. The two are complementary: an IndieWeb site can host a rootless app, and a rootless app can syndicate via IndieWeb protocols.

## Solid (Social Linked Data)

**Summary.** Tim Berners-Lee's project ([solidproject.org](https://solidproject.org)) separating apps from data: users own Pods (personal data stores), apps request access. The Pod is the user's data layer; apps are stateless clients.

**Overlap and difference.** Solid and rootless both want user-owned data and app-independence, but Solid still presumes a Pod-host (yours or your provider's) acting as the data coordinator. Rootless puts the data on the device itself — no Pod, no host, no auth dance.

## IPFS, Hypercore, dat

**Summary.** Content-addressed peer-to-peer storage protocols. IPFS (Protocol Labs), Hypercore/Hyperdrive (Holepunch, formerly Dat Project), Beaker Browser (now retired). Files are addressed by hash; any peer that has them can serve them.

**Overlap and difference.** These protocols would be natural distribution substrates for rootless apps. The reason most rootless apps today use HTTPS + GitHub Pages instead of IPFS is operational, not philosophical: browser support, gateway reliability, and discoverability are all weaker for content-addressed networks today. A future where IPFS or successors carry rootless artifacts directly is plausible and welcome.

## Serverless / edge functions

**Summary.** Cloud-vendor execution models (AWS Lambda, Cloudflare Workers, Vercel Functions) that run server code on demand without managing servers. Billing is per-invocation.

**Overlap and difference.** "Serverless" is a misnomer — the servers are very much there, just rented finely. Rootless apps share none of the architectural pattern; they share only the absence of a long-running owned process. A rootless app may use an edge function for a single narrow purpose (a signaling shim, an OAuth callback handler) without ceasing to be rootless, as long as the function is replaceable and not load-bearing.

## Peer-to-peer web / Beaker Browser

**Summary.** Beaker Browser ([beakerbrowser.com](https://beakerbrowser.com), 2016–2022, retired) was a Chromium fork that natively spoke the dat protocol, letting users publish sites peer-to-peer with no server. The project ended but the ideas continue under Hypercore.

**Overlap and difference.** Beaker was probably the closest prior approximation of rootless apps as a category. The conceptual debt is large. The reason rootless is a current term and not a continuation of Beaker's vocabulary is that browsers in 2026 have absorbed enough P2P primitives (WebRTC, WebTransport, OPFS) that a custom browser is no longer required. Beaker imagined a different transport; rootless settles for the transport browsers already ship.

## Rootless containers (etymological ancestor)

**Summary.** Container runtimes (`podman`, rootless Docker, `runc` in user mode) that operate without a privileged root daemon. The user's UID owns the containers; no system-level coordinator is required.

**Overlap and difference.** This is where the name comes from. The analogy is deliberate: rootless containers removed the privileged daemon from container execution and discovered that the daemon was mostly historical. Rootless computing removes the privileged server from application execution and bets the same is true.

## Where rootless sits

```
                         user ownership of data
                                  ▲
                                  │
                       Local-first│  ●
                                  │
                                  │       ●  Rootless
                                  │
                    Solid  ●      │
                                  │
                IPFS/dat  ●       │       ●  Beaker
                                  │
                                  │
                       JAMstack   │
                            ●     │     ●  IndieWeb
                                  │
                  Serverless  ●   │
                                  │
                                  └──────────────────────►
                                       independence from
                                       privileged coordinator
```

The point of locating rootless on this map is not to claim it dominates the others. It is to show that no prior name occupies the upper-right corner — high data-ownership *and* high coordinator-independence *and* low operational burden — which is the corner most of these apps actually live in.
