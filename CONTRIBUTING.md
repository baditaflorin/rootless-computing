# Contributing

This repository codifies a category. Contributions sharpen the category. Three kinds of contribution are explicitly welcome:

1. **Propose a principle** — argue that the manifesto is missing something load-bearing, or that an existing principle should be split, merged, or removed.
2. **Submit an example** — add a rootless app to the index.
3. **Dispute a definition** — argue that a vocabulary entry is wrong, ambiguous, or misnames the thing it points at.

If your contribution fits none of those, open an issue anyway and describe what you'd like to change.

## Proposing a principle

Open an issue with the [propose-principle](https://github.com/baditaflorin/rootless-computing/issues/new?template=propose-principle.md) template. State:

- The proposed principle as a single declarative sentence (in bold, in the issue body).
- The rationale, in 2–4 sentences.
- Which existing principle it complements, replaces, or contradicts.
- A concrete example of a rootless app that demonstrates the principle.

Principles enter the manifesto when at least one of the existing principles cannot be derived from it and it cannot be derived from them. The bar is high on purpose. The manifesto is better at 8 strong principles than 12 mediocre ones.

## Submitting an example

Open a PR adding your entry to [docs/examples.md](docs/examples.md) using the submission template at the bottom of that file. The entry must include:

- Repo URL — the app's source.
- Principles demonstrated — the numbers from the [manifesto](MANIFESTO.md).
- Adjacent concepts used — Pages-Native, Bake-Time Backend, Mesh, ZK, Fiducials, IPFS, etc.

Apps that fail the "fork-and-enable-Pages-in-five-minutes" test will not be accepted as examples. They may still be linked from [adjacent-work.md](docs/adjacent-work.md) if they illustrate a closely related pattern.

## Disputing a definition

Open an issue with the [dispute-definition](https://github.com/baditaflorin/rootless-computing/issues/new?template=dispute-definition.md) template. Quote the existing language, state what's wrong with it, and propose a replacement. Definitions evolve via PR; arguments happen in issues first.

## Style notes

- Prose should match the manifesto's voice: confident, plain, technical, no LLM tells.
- No "in today's fast-paced world," no "leverage," no "revolutionize," no "paradigm shift," no "ecosystem."
- Avoid emoji in the manifesto body and adjacent-work doc. Sparing use elsewhere is fine.
- Cite prior work honestly. The point is not to claim novelty over everything that came before.

## License of contributions

By contributing, you agree that:

- Prose contributions are licensed under [CC BY 4.0](LICENSE).
- Code contributions are licensed under [MIT](LICENSE).

Both licenses are in the same `LICENSE` file.

## Code of conduct

This project follows the [Contributor Covenant 2.1](CODE_OF_CONDUCT.md). Disagree freely, attack ideas not people.

## Forking

If you disagree with the manifesto's direction and your changes are not accepted, you are encouraged to fork the manifesto entirely and run a competing definition. The manifesto is itself a rootless artifact — there is no canonical instance, and a fork is an equally legitimate copy. The category benefits from competition.
