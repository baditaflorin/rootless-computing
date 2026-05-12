# Examples

Rootless apps in the wild. This list is the canonical index. To add yours, see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example) or open an issue with the [submit-example](https://github.com/baditaflorin/rootless-computing/issues/new?template=submit-example.md) template.

Each entry includes which principles it demonstrates (by number from the [manifesto](../MANIFESTO.md)) and which adjacent concepts it relies on (Pages-Native, BTB = Bake-Time Backend, Mesh, WASM, ZK, Fiducials).

## Confirmed entries

### anon-conf-poll
Static, anonymous live polling with CRDT sync, zk one-vote proofs, and local analytics.
- Repo: https://github.com/baditaflorin/anon-conf-poll
- Principles: 1, 2, 3, 4, 5, 6, 7, 9, 10
- Uses: Pages-Native, BTB, Mesh, WASM, ZK

## Seed entries from the May 2026 build-in-public month

These were shipped as part of a single-author 31-app challenge. Each one is a candidate rootless app pending confirmation that it satisfies all relevant principles. Repo links resolve under https://github.com/baditaflorin/.

### mesh-pair-rotation
Pair-programming rotation manager. Suggests fresh pairs, sync driver-navigator role flip every 25 min.
- Repo: https://github.com/baditaflorin/mesh-pair-rotation
- Principles: 1, 2, 3, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-brain-write
Silent brainstorm. Type ideas privately on a timer; pooled anonymously. ArUco mode for paper ideas.
- Repo: https://github.com/baditaflorin/mesh-brain-write
- Principles: 1, 2, 3, 4, 5, 7, 8, 9
- Uses: Pages-Native, Mesh, WASM, Fiducials

### mesh-lunch-roulette
Weekly coffee-chat pairing for teams. History-aware so no two people repeat until everyone has met.
- Repo: https://github.com/baditaflorin/mesh-lunch-roulette
- Principles: 1, 2, 3, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-retro
Anonymous retro board. Mad/Sad/Glad + dot voting. ArUco mode for hands-free wall publish.
- Repo: https://github.com/baditaflorin/mesh-retro
- Principles: 1, 2, 3, 4, 5, 7, 8, 9
- Uses: Pages-Native, Mesh, WASM, Fiducials

### mesh-trivia
Kahoot-style trivia. Mesh-time synchronized reveal; fair first-to-answer scoring.
- Repo: https://github.com/baditaflorin/mesh-trivia
- Principles: 1, 2, 3, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-direction-finder
Site-specific compass-aligned panorama. Each phone shows its panorama slice only when pointed at the correct bearing.
- Repo: https://github.com/baditaflorin/mesh-direction-finder
- Principles: 1, 2, 3, 7, 8, 9
- Uses: Pages-Native, BTB, Fiducials

### mesh-pulse-photo
Group heart-rate biofeedback. Camera+flash reads your pulse; all phones glow at the room's average BPM.
- Repo: https://github.com/baditaflorin/mesh-pulse-photo
- Principles: 1, 2, 4, 5, 7, 9
- Uses: Pages-Native, Mesh, WASM

### mesh-light-paint
Synchronized phone-screen light painting. Long-exposure photo composites mesh-synced patterns.
- Repo: https://github.com/baditaflorin/mesh-light-paint
- Principles: 1, 2, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-standup
Round-robin standup timer with ArUco baton-pass. Hold up your tag card to claim the floor.
- Repo: https://github.com/baditaflorin/mesh-standup
- Principles: 1, 2, 4, 5, 7, 8, 9
- Uses: Pages-Native, Mesh, WASM, Fiducials

### mesh-icebreaker
Curated icebreaker prompt decks with round-robin. Kickoffs, retros, year-end reviews, conflict resets.
- Repo: https://github.com/baditaflorin/mesh-icebreaker
- Principles: 1, 2, 3, 5, 7, 9
- Uses: Pages-Native, BTB, Mesh

### mesh-applause
Anonymous kudos wall. Send appreciations to teammates; reveal at standup.
- Repo: https://github.com/baditaflorin/mesh-applause
- Principles: 1, 2, 4, 5, 6, 7, 9
- Uses: Pages-Native, Mesh, WASM, ZK

### mesh-shadow-paint
Phones become colored fill lights. One phone is the camera; others show solid hues from different angles.
- Repo: https://github.com/baditaflorin/mesh-shadow-paint
- Principles: 1, 2, 5, 9
- Uses: Pages-Native, Mesh

### mesh-quiet-quest
Gamified group silence. Mic-monitored quiet game; shared score ticks up while the room stays quiet.
- Repo: https://github.com/baditaflorin/mesh-quiet-quest
- Principles: 1, 2, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-stretch-class
Group yoga / stretch class. Phones detect 'holding the pose' via accelerometer; instructor sees the aggregate.
- Repo: https://github.com/baditaflorin/mesh-stretch-class
- Principles: 1, 2, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-mood-check
Daily team mood barometer. Tap one of 5 face emojis; aggregate displayed instantly; never logged centrally.
- Repo: https://github.com/baditaflorin/mesh-mood-check
- Principles: 1, 2, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-pomodoro-room
Group pomodoro. All phones run a mesh-time-synced 25/5 timer; signals for done-early or stuck.
- Repo: https://github.com/baditaflorin/mesh-pomodoro-room
- Principles: 1, 2, 5, 7, 9
- Uses: Pages-Native, Mesh

### mesh-skill-tree
Anonymous team skill radar. Self-rate 8-12 skills 1-4; team gets aggregate radar chart with no individual data.
- Repo: https://github.com/baditaflorin/mesh-skill-tree
- Principles: 1, 2, 4, 5, 6, 7, 9
- Uses: Pages-Native, Mesh, WASM, ZK

### mesh-silent-vote
Ranked-choice or approval voting on a list of options.
- Repo: https://github.com/baditaflorin/mesh-silent-vote
- Principles: 1, 2, 4, 5, 6, 7, 9
- Uses: Pages-Native, Mesh, WASM, ZK

### mesh-anonymous-qa
Audience submits questions anonymously, upvotes others. Replaces Slido / Mentimeter Q&A.
- Repo: https://github.com/baditaflorin/mesh-anonymous-qa
- Principles: 1, 2, 4, 5, 6, 7, 9
- Uses: Pages-Native, Mesh, WASM, ZK

### trust-no-one-anonymizer
Client-side face and voice anonymizer for private browser-based video calls.
- Repo: https://github.com/baditaflorin/trust-no-one-anonymizer
- Principles: 1, 2, 4, 7, 9
- Uses: Pages-Native, WASM

### Pending — slot 21
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 22
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 23
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 24
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 25
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 26
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 27
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 28
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 29
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 30
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

### Pending — slot 31
Entry pending — see [CONTRIBUTING.md](../CONTRIBUTING.md#submitting-an-example).

## Submission template

```markdown
### <app name>
<one-line description>
- Repo: https://github.com/<owner>/<repo>
- Principles: <comma-separated principle numbers from the manifesto>
- Uses: <comma-separated adjacent concepts: Pages-Native, BTB, Mesh, WASM, ZK, Fiducials, IPFS, etc.>
```

Submit by opening a PR that adds your entry to this file and to [examples/README.md](../examples/README.md), or by filing an issue with the [submit-example](https://github.com/baditaflorin/rootless-computing/issues/new?template=submit-example.md) template.
