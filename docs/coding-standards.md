# Coding standards

[Handbook](../README.md) · [Principles](principles.md) · **Coding standards** · [Randomness](randomness.md) · [Testing](testing.md) · [Performance](performance.md) · [Open source](open-source.md) · [Glossary](glossary.md)

The rules the site actually follows. Each one has a reason, and the reason is usually an incident.

## Layout of a project

- **Built and copied are separate.** Source the build processes lives in one folder. Static files that reach the browser exactly as written live in another and are copied untouched.
- **A route folder is public.** Every file in the serverless routes folder becomes a live URL. Shared helpers live outside it, so a helper never turns into an endpoint by accident.
- **Blog posts are pre-rendered.** Markdown becomes static HTML at build time. No Markdown parsing in the browser.

## JavaScript

- Vanilla, browser-ready. No framework, no transpiler. Keep existing file names and conventions.
- **Randomness comes from one place.** The roller draws every die through a single function, so swapping the source reaches every roll without touching roller code.
- **Never spend roll randomness on decoration.** Sound jitter and similar effects use `crypto.getRandomValues` directly, never the roll source.
- **`markBlock()` and `blockReceipt()` stay in one synchronous block.** Other things on the page draw from the same randomness pool. Synchronous code cannot interleave, and that alone keeps their draws out of a roll's receipt. Put anything async between the two and the receipts start lying, silently.
- **The pool is a queue of chunks, and each chunk carries its own beacon record.** A single flat buffer with one label let a refill relabel bytes from the previous pulse. Do not flatten it.
- **Degrade out loud.** If the pool runs dry mid-roll, the die comes from the device and the receipt says `+ device`.

## CSS

- Plain CSS. No preprocessor.
- **Theme tokens only.** A colour may be written in a theme file and nowhere else. Everything else uses `var(--token)`. The build fails on a hex, `rgb()`, `hsl()` or named colour anywhere else.
- **One escape, used sparingly.** A depth shadow or a scrim is not a theme colour, so a line may end with `/* allowed: why */`. If you reach for it to set a foreground or a panel, the token is missing. Add the token.
- **One theme file per page.** A tiny inline script picks it before first paint, so the theme never flashes in.
- **Night is a theme file, not a media query.** The site follows its own day/night toggle, not `prefers-color-scheme`.
- **Scope generic rules.** The roller's dice rows are hand-tuned so the inputs line up. A rule touching `ul`, `li`, line-height or spacing is scoped to content areas so it can never reach them.
- **Paths inside CSS variables are absolute.** A variable read on a nested page resolves relative paths against that page and 404s.

## HTML

- Shared header and footer are baked into every page at build time.
- A page references its own scripts and styles by bare name. The build stamps each with a content hash (`?v=<hash>`), so a changed file gets a new URL and nobody bumps a version by hand.
- Every canonical tag and sitemap entry names an address that returns 200, never one that redirects. The build checks.

## Data from people

- **Validate on the server, field by field, against an allow-list.** A colour must be six-digit hex. A scene must be one we ship. Values that end up inside CSS custom properties get the strictest checks.
- **Escape everything printed.**
- **User-submitted links carry `rel="ugc nofollow"`.** A test checks it.

## Images

- **Ship WebP.** Try lossy and lossless, keep the smaller file:

  ```sh
  cwebp -q 82 -alpha_q 100 in.png -o out.webp     # lossy: photos, painted art
  cwebp -lossless -z 9      in.png -o out.webp    # lossless: flat colour, UI captures
  ```

- **Over about 200 KB?** It almost certainly wants re-encoding.
- **Keep the original.** Full-resolution masters live outside the published build, with a note mapping each to what it became and the command that made it.
- **Blur ahead of time.** Glass panes show a pre-blurred copy of the theme art, not a live CSS blur. See [Performance](performance.md).

## Git

- `main` is production. Work lands on `dev`, which gets its own preview. A job gets a short branch off `dev`.
- One branch, one job. The name is the description.
- Never rewrite `main`'s history. Merge `main` into an older branch before pushing it.
- Merge with `--no-ff`, so one revert undoes a whole feature.
- Delete the branch after merging. Done means gone.
- Work in a fresh worktree, not in someone else's checkout.
- Commit messages: one line, what changed and why.
- Run `git status` before every commit and read it. Every file listed is going in.

Read with: [Testing](testing.md) for the checks every change passes.
