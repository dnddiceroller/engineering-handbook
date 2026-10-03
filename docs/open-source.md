# Open source

[Handbook](../README.md) · [Principles](principles.md) · [Coding standards](coding-standards.md) · [Randomness](randomness.md) · [Testing](testing.md) · [Performance](performance.md) · **Open source** · [Glossary](glossary.md)

GitHub is our museum. The workshop is private.

## What we publish

The parts we are happy to prove in public: the ideas, the interfaces, the tools, and how we work.

| Repo | Why it is public |
| --- | --- |
| [roll-verification-spec](https://github.com/dnddiceroller/roll-verification-spec) | A receipt is only worth something if anyone can read exactly what it claims |
| [examples](https://github.com/dnddiceroller/examples) | So you can check a receipt with code you can read in five minutes, not ours |
| [dice-probability-tools](https://github.com/dnddiceroller/dice-probability-tools) | Exact odds are useful to every table, not only ours |
| [engineering-handbook](https://github.com/dnddiceroller/engineering-handbook) | How we build is worth sharing even where the code is not |
| [.github](https://github.com/dnddiceroller/.github) | The org profile, and contributing, security and conduct defaults for every repo |

## What stays private

- **The production site.** The roller, the server, the build and the deploy.
- **Secrets.** The server key behind each roll, credentials, and anything that would let someone predict or forge a roll.
- **Infrastructure details.** Account identifiers, database names, internal endpoints.
- **Business data.** Visitors, revenue, partners.

## Why the split

1. **Verifying doesn't need our code.** The receipt check runs against the beacon, in your browser or your terminal. Publishing the spec and a reference checker gives you everything you need to check us without trusting us.
2. **Some secrets are the security.** The dice derivation uses a secret key on purpose. Publish it and anyone watching the beacon could predict every roll.
3. **Curated beats mirrored.** A mirror of a private repo goes stale and looks abandoned. A small set of intentional repos stays accurate.
4. **Careful code is easier kept careful.** The production code has load-bearing quirks. Keeping it private lets us change it slowly and on purpose.

## What that means for you

- The spec describes the live site on the date it names. If the site changes what a receipt means, the spec changes with it.
- The examples are deliberately simplified. They teach the idea; they are not the production code.
- An issue or pull request here changes these repos, not the live roller. Found something wrong with the site itself? Email dev@dnddiceroller.com. Security problems: [SECURITY.md](https://github.com/dnddiceroller/.github/blob/main/SECURITY.md).

## Licences

| What | Licence |
| --- | --- |
| Code in every public repo | MIT |
| Prose in this handbook | CC BY 4.0 |
