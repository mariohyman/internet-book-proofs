# Internet Book proofs

Every day at 07:00 America/Chicago, Internet Book asks Google a fixed panel of questions
and stores each response exactly as received. This repository proves when each day's
capture existed and that it hasn't changed since. It holds no captured content.

`runs/<date>/` holds, for each day:

- `manifest.json`: the SHA-256 and size of every file in that day's capture
- `manifest.sha256`: the SHA-256 of `manifest.json`, the day's fingerprint
- `manifest.json.ots`: an OpenTimestamps proof that `manifest.json` existed by the time
  of a Bitcoin block, usually within a few hours of the capture

## Checking a capture

1. Hash the capture file: `shasum -a 256 A01/organic.json`. It must match that file's
   entry in the day's `manifest.json`.
2. Check the timestamp: drop `manifest.json` and `manifest.json.ots` onto
   https://opentimestamps.org. With a Bitcoin node, `ots verify manifest.json.ots` works
   offline too.

A proof added in the last few hours may still say pending. The daily job upgrades it
once the Bitcoin transaction confirms.
