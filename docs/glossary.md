# Glossary

[Handbook](../README.md) · [Principles](principles.md) · [Coding standards](coding-standards.md) · [Randomness](randomness.md) · [Testing](testing.md) · [Performance](performance.md) · [Open source](open-source.md) · **Glossary**

Words we use, in plain English. Alphabetical.

**Beacon.** A public service that issues a fresh random value on a fixed clock and keeps every past value at a public address. Nobody can know a value before it is issued. We use two: NIST and drand. See [Randomness](randomness.md).

**Block.** Everything one press of Roll or Roll All produces. One block gets one receipt line.

**Certificate.** A page on the site that reads a receipt's link, fetches the named record from the beacon in your browser, and says **match** or **does not match**. It signs nothing. Format: [SPEC.md section 3](https://github.com/dnddiceroller/roll-verification-spec/blob/main/SPEC.md#3-the-certificate-url).

**Chain.** Which sequence of records a beacon value belongs to. For NIST, a small number; the site uses chain 2. For drand, a 64-hex-digit chain hash.

**Chunk.** A batch of random bytes in the browser's pool, labelled with the beacon record it came from. The pool is a queue of chunks, so every byte keeps its label.

**`+ device`.** The end of a receipt when part of a roll used device randomness, because the beacons were unreachable or the pool ran dry.

**Device randomness.** Your browser's cryptographic generator, `crypto.getRandomValues`. Labelled **Secure Enclave** in the picker. Fast, offline, and no public record, so no receipt.

**drand.** A beacon run by the League of Entropy, a group of independent organisations. A new **round** every 30 seconds. The site's second source.

**Fallback.** What happens when a source cannot answer. NIST falls back to drand, drand to NIST, and both to the device. A roll never waits and never hides which source it used.

**HMAC-SHA256.** A keyed hash. The server mixes a beacon record with a secret key, the account, a nonce and a counter to produce dice bytes. See [SPEC.md section 5](https://github.com/dnddiceroller/roll-verification-spec/blob/main/SPEC.md#5-from-pulse-to-dice).

**Match.** The certificate's verdict when the hash in your link equals the one the beacon published for that record.

**NIST Beacon.** The Randomness Beacon run by the US National Institute of Standards and Technology. A new **pulse** every 60 seconds. The site's default source.

**Nonce.** A per-request value mixed into the dice derivation and never published. With the server key, it stops anyone predicting a roll from the public record.

**Output value.** NIST's name for a pulse's 512-bit random value, written as 128 hex digits. The `hash` in a NIST certificate link.

**Pool.** The bytes your browser holds, ready for the next die. It refills in the background before it runs low.

**Pulse.** One NIST record: an index, a timestamp and an output value.

**Randomness.** drand's name for a round's random value, written as 64 hex digits. The `hash` in a drand certificate link.

**Receipt.** The line the roll log prints after a block in NIST Beacon mode. It names each beacon record the dice drew on, the first 12 hex digits of its hash, and a certificate link. Format: [SPEC.md section 2](https://github.com/dnddiceroller/roll-verification-spec/blob/main/SPEC.md#2-the-receipt).

**Rejection sampling.** Throwing away random values that would favour some faces, so every face is exactly equally likely. Shown in [derive-roll.mjs](https://github.com/dnddiceroller/examples).

**Round.** One drand record: a number and its randomness.

**Server key.** The secret the server uses in the dice derivation. Never published. It is why a receipt proves when, not what.

**Theme token.** A named CSS custom property, like `var(--theme-primary)`. The only way a colour reaches a page outside a theme file. See [Coding standards](coding-standards.md).

**Uncursed.** Table slang for dice nobody has tampered with. The site's own banner once said "Your dice are uncursed · your plan is another matter." A receipt is the closest thing we have to proof: it shows the roll's input came from a public record nobody could pick in advance.
