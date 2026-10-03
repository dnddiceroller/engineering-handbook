# Performance

[Handbook](../README.md) · [Principles](principles.md) · [Coding standards](coding-standards.md) · [Randomness](randomness.md) · [Testing](testing.md) · **Performance** · [Open source](open-source.md) · [Glossary](glossary.md)

Only numbers we measured. Each has a date or a source.

## What the site is built on

- **Static, pre-rendered pages.** The blog is rendered to HTML at build time. No Markdown in the browser.
- **No framework, no bundler.** Nothing to download before the page can run its own code.
- **One build dependency**, the Markdown renderer, and it never reaches the browser.

## Measured

| What | Number | When |
| --- | --- | --- |
| Time to first byte, homepage | 45 ms | 9 Aug 2026 |
| Homepage HTML | 20 KB | 9 Aug 2026 |
| Homepage total weight, after moving every image to WebP | 425 KB, down from 3,782 KB | 30 Aug 2026 |
| Glass blur images | 7 JPEGs, 14 to 31 KB each. A visitor downloads one (two for the classic theme on phones) | 30 Sep 2026 |
| Glass script | under 2 KB | 30 Sep 2026 |

## Budgets we hold

- **Image ceiling.** Over about 200 KB, an image almost certainly wants re-encoding. One 1 MB PNG once sat in a published post for months.
- **Every feature declares its cost.** Briefs state bytes and dependencies before the work starts. Recent examples:

| Feature | Declared cost |
| --- | --- |
| Custom controls on the dice lines | ~24 KB, 0 dependencies, 0 assets |
| Blog booklet | ~23 KB, 0 dependencies, 0 assets |
| One page per die | 12 pages, ~15 KB JS, 0 dependencies |
| Exploding dice | ~62 lines, 0 assets, off by default |

## Choices that save bytes and work

- **Pre-blurred glass.** Glass panes show a blurred copy of the theme art, made once ahead of time, instead of a live `backdrop-filter` that re-blurs whenever something moves. A user's own uploaded image has no copy, so it still blurs live.

  ```sh
  magick <art>.webp -resize 900x -blur 0x14 -strip -quality 68 <art>_blur.jpg
  ```

- **Content-hashed assets.** Browsers cache scripts and styles for hours. The build stamps each with a hash of its contents, so a deploy reaches people on their next page load and an unchanged file stays cached.
- **No flash of the wrong theme.** One small inline script picks the theme file before first paint.
- **Nothing runs unasked.** No polling and no new fetch on page load without a brief that names it.

## Open items

We aim to stop scripts blocking the first render. On 9 August 2026 the homepage loaded 15 scripts and 13 blocked rendering, including jQuery from a third-party host. The server is fast; the gap between the page arriving and the page being usable is what we aim to close.

The fix is mostly `defer` on each tag. The roller's core script defines functions that inline click handlers call, so it needs a change before it can take `defer`.

## Measure your own change

- Page weight, request count and render time, before and after, on the same machine.
- Put the numbers in the pull request or the branch log.

See [Testing](testing.md) for the screenshot and diff routine.
