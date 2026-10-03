# engineering-handbook



https://github.com/user-attachments/assets/23eb1016-591f-43bc-a888-dbb481be2103



From the team behind [dnddiceroller.com](https://www.dnddiceroller.com) · [more from us](https://github.com/dnddiceroller)

**Roll dice. Keep the receipt.**

How we build the dice roller: the rules we follow, why each one exists, and the numbers behind them. The production code stays private. The way we work does not need to.

Every rule here comes from the team's own working notes. Most exist because something broke once and the reason was not obvious afterwards. Where we have not got there yet, the page says **We aim to**.

## Pages

| Page | Read it for |
| --- | --- |
| [Principles](docs/principles.md) | How we decide what to build, and what a change must carry with it |
| [Coding standards](docs/coding-standards.md) | The HTML, CSS and JavaScript rules the site actually follows |
| [Randomness](docs/randomness.md) | NIST beacon, drand and device randomness in plain English, and what a receipt proves |
| [Testing](docs/testing.md) | The build as a test, plain Node tests, screenshots, and the traps that fool them |
| [Performance](docs/performance.md) | Measured page weight and speed, and the open items |
| [Open source](docs/open-source.md) | What we publish, what stays private, and why |
| [Glossary](docs/glossary.md) | Receipt, pulse, beacon, chain, round and the rest |

## Start here

- **New to the site?** Read [Randomness](docs/randomness.md), then the [Glossary](docs/glossary.md).
- **Want to contribute?** Read [Principles](docs/principles.md), then [CONTRIBUTING.md](https://github.com/dnddiceroller/.github/blob/main/CONTRIBUTING.md).
- **Want the exact receipt format?** That lives in [roll-verification-spec](https://github.com/dnddiceroller/roll-verification-spec). This handbook explains it; the spec defines it.

## The rest of the box

| Repo | What's inside |
| --- | --- |
| [roll-verification-spec](https://github.com/dnddiceroller/roll-verification-spec) | What a roll receipt means and how a certificate is checked |
| [dice-probability-tools](https://github.com/dnddiceroller/dice-probability-tools) | Exact odds for tabletop dice |
| [examples](https://github.com/dnddiceroller/examples) | Verify a receipt yourself; see how a hash becomes a fair die face |

## Fix something

Found a rule that reads wrong, or a term we forgot? Open an issue or a pull request. [CONTRIBUTING.md](https://github.com/dnddiceroller/.github/blob/main/CONTRIBUTING.md) has the short version.

## Licence

Code in this repo is MIT ([LICENSE](LICENSE)). The prose in `docs/` and this README is [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): share and adapt it, and credit Iron Code Studios.




