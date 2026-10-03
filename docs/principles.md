# Principles

[Handbook](../README.md) · **Principles** · [Coding standards](coding-standards.md) · [Randomness](randomness.md) · [Testing](testing.md) · [Performance](performance.md) · [Open source](open-source.md) · [Glossary](glossary.md)

A dice roller should be fast enough for the game table, and rigorous enough that anyone curious can see what happened. Everything below serves one of those two.

## 1. Plain tools

The site is vanilla HTML, CSS and JavaScript. No framework, no bundler, no transpiler, no CSS preprocessor. A small Node script builds it, and its one build dependency turns Markdown into HTML.

What you write is what the browser runs. Edit a file, build, reload.

## 2. Brief first, then build

Before a feature starts, it gets a one-page brief:

- what it does
- why it is worth doing
- what it costs in bytes and dependencies
- how to check it
- how to undo it

Writing the cost down before the code exists is the cheapest review there is.

## 3. The five rules every brief follows

1. **No new dependencies.** No package, no CDN, no new build step.
2. **No new assets** unless the brief names the file and its size.
3. **Nothing runs that is not asked for.** No polling, no new fetch on page load.
4. **Every change is reversible** by one revert, and the brief says what that revert restores.
5. **Every claim is measured.** Page weight, request count and render time, before and after, on the machine that did the work.

## 4. Small, careful changes

The site works. Some of its patterns are unusual, and some of those are load-bearing.

- We do not refactor or "tidy" code without agreeing it first.
- We explain a change before making it: what it does, what it touches, what could break.
- One branch does one job, and its name says which.

## 5. Checkable, not trusted

A randomness source belongs on the site only if anyone can check it without asking us and without trusting us. That rules out sources with good bytes and no public record. See [Randomness](randomness.md).

## 6. Never round a claim up

A receipt proves the beacon record is real and existed at that moment. It does not let anyone recompute the dice. We say both, every time. A claim that reads stronger than the system supports is a bug, and we fix the words the same day.

## 7. A promise is a promise

Some things look like settings and are really promises to people already using the site:

- **Source order.** NIST first, drand second, then the device. We do not reorder because one is healthier this week.
- **Stored names.** A saved setting keeps its storage key. Renaming it silently resets everyone's choice.
- **What someone sees.** When we upgrade a feature, a person who changed nothing sees nothing change.

## 8. Fail the build, don't warn

A warning scrolls past in a log nobody reads. Our build stops on the problems we care about: two files that would land on one URL, a canonical tag pointing at an address that redirects, a colour written outside a theme file. See [Testing](testing.md).

## 9. The docs are part of the change

If a change alters behaviour that a doc describes, the doc changes in the same branch. When code and doc disagree, that is a finding to report, not a licence to pick one. Read the spec before deciding it is stale.

Each branch leaves a short log: what changed, why, what was checked, and any box left unticked with the reason. A judgement call is marked as one, so a design decision never reads as a fix.

## 10. Honest by default

When something degrades, it says so. If a beacon cannot be reached, the roll still happens on the device, and the receipt ends in `+ device`. A roll is never blocked and never mislabelled.
