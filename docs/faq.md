# FAQ

Honest answers to the obvious questions. Where something is genuinely unsolved, this page says so.

## Isn't this just static sites with extra steps?

Static sites are the ancestor, and the family resemblance is real. The difference is what runs after the page loads. A static site renders HTML and stops. A rootless app loads a static artifact and then does meaningful work in the browser — analytical queries against a baked database, ZK proof generation, CRDT merge against other peers, fiducial-aligned compass math. The deployment story is shared; the runtime is not.

## How is this different from local-first software?

Rootless and local-first are siblings, and the Ink & Switch [2019 essay](https://www.inkandswitch.com/local-first/) is required reading. Local-first centers *data ownership* and *sync*: your data lives on your device, and synchronization is a property of the data, not of a service. Rootless centers *deployment* and *coordination*: the application has no origin, and peers coordinate without a host.

In practice they are highly compatible. Most rootless apps are local-first by necessity (no server means no remote database). But you can build local-first apps that depend on a sync service (still local-first, not rootless), and you can build rootless apps that hold no user data at all (still rootless, not really local-first).

## How is this different from JAMstack?

JAMstack names a build-and-deploy pattern: ship static markup, hydrate with JavaScript, call APIs at runtime. The "A" in JAM is *API* — JAMstack apps are typically thin clients to managed backends. Rootless apps inherit JAMstack's static-first deployment story but reject the runtime-API assumption. There is no API to call because there is no server to host it. Coordination, when needed, happens between peers.

## How is this different from web3 / dApps?

This is the comparison that matters most, because surface vocabulary is similar and the underlying philosophy is opposed.

Web3 / dApps require *global consensus*: every node agrees on the ordered history. This is expensive, slow, and necessary only if you are minting scarce digital assets. Rootless apps require *no consensus* — they accept that two forks may diverge and that two participants may see different views. Rootless apps have no native token, no chain, no gas, no validator set, no canonical state.

Rootless borrows from web3's better ideas: zero-knowledge proofs for eligibility, nullifiers for one-action-per-user, content addressing for artifacts. It refuses the framing that *every* coordination problem is a ledger problem. Most are not.

## What about authentication?

There are three honest answers:

1. Many rootless apps need no authentication at all. A retro board, a poll, a stretch class — the participants do not need accounts. They need an invitation link.
2. When eligibility matters, prefer cryptographic proofs over identity. A Semaphore-style group membership proof says "this person is in the allowed set" without saying *which* person, and pairs with a nullifier to enforce one-action-per-member.
3. When stable identity is required, lean on existing identity providers via OAuth — but treat the resulting token as a peer-to-peer credential, not a server session. The provider becomes a trusted issuer, not a coordinator.

## What about abuse, moderation, and spam?

This is the hardest open problem in rootless computing, and pretending otherwise would be dishonest.

Without a coordinator there is no central place to ban a user, take down content, or rate-limit a flood. Several partial answers exist: cryptographic eligibility narrows who can participate; nullifiers cap how often; local client-side filters let each peer choose what to see; physical anchors limit participation to people in a room. None of these are sufficient on their own, and none scale to "anonymous strangers on the public internet."

The honest framing: rootless apps work well for *bounded* groups — a conference, a team, a class, a room — and degrade for *unbounded* ones. This is a real limit of the architecture, not a defect of this manifesto.

## Does this scale?

For the cases rootless apps target, yes — sometimes spectacularly. A baked artifact serves a million users for the cost of serving one. Peer coordination scales with the number of people in a room, not the number of users worldwide. The user's device is the database, so the database scales by the number of devices.

It does not scale to *global*, *strongly consistent*, *coordinator-driven* workloads. That is what hosted services are for. Use those when you need them.

## Why coin a new term instead of using existing vocabulary?

Because the existing terms are each pointing at one face of the thing.

- "Static site" describes the deployment but underdescribes the runtime.
- "Local-first" describes the data ownership but is silent on deployment topology.
- "P2P" describes the transport but is silent on artifact distribution.
- "Serverless" describes a billing model and is actively misleading here.
- "Decentralized" has been overloaded by crypto and now connotes ledger consensus.

*Rootless computing* names the intersection. A rootless app is static-deployed, local-first in data, P2P in coordination, server-free in dependency, and decentralized in the older sense (no privileged coordinator). The single term lets people find each other.

## What does this have to do with rootless containers?

The name is borrowed deliberately. In containers, *rootless* means "runs without a privileged root daemon" — no `dockerd` running as root, no system-level coordinator required. The analogy is tight: rootless containers remove the privileged daemon; rootless apps remove the privileged server. In both cases the unprivileged version turns out to be enough for most real-world cases, and the privileged version was historical accident more than necessity.
