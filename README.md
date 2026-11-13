# Ad Media Bridge

Public delivery bridge for current, approved advertising artwork across Meta and other ad platforms.

## Admission rule

Only upload the exact approved version of an asset that is still approved for use. Never upload rejected artwork, correction drafts, superseded artwork, editable source files, strategy documents, customer information, credentials or access tokens. A FINAL folder or filename is not proof of current approval.

## Keep artwork out of Git history

Do **not** commit artwork into Git: Git retains old versions after replacement or deletion.

Use one mutable GitHub release tagged `current` for delivery assets. Replace or remove its files when approval changes. Do not create archival media releases, version folders or backup copies in this bridge. Text configuration and catalog history may remain in Git; artwork must not.

The release is not initialized and the catalog is empty. This setup did not publish any artwork.

Removing an asset here does not erase copies already downloaded, cached or uploaded to ad platforms. Those platform copies require their own withdrawal action; the bridge cannot guarantee deletion outside its control.

## Naming

- Asset ID: `<product>/<creative-id>/<format>`
- Delivery filename: `<product>--<creative-id>--<format>.<extension>`

Example naming only: `bonus-depreciation/ECC9BF/1x1` and `bonus-depreciation--ECC9BF--1x1.png`. This example is not an uploaded file or catalog entry. Keep the asset ID stable; replace its current delivery object rather than keeping old variants alongside it.

## Publish and verify

1. Confirm exact-version approval and no outstanding correction or withdrawal.
2. Read real file type, dimensions, byte size and SHA-256.
3. Upload that approved file as a release asset in `current`, not as a Git-tracked file.
4. Admit it to `catalog.json` only after its public delivery URL and actual bytes are verified.
5. Send that URL through the ad platform's media-upload plugin/API. Save returned platform media IDs in private platform records.
6. Verify the saved asset and a paused preview. A stored image reference alone does not prove rendering.
7. Activate ads only with explicit human authorization.

Release-asset upload and removal capabilities still need to be connected and tested. This repository alone does not automate publication.

## Corrections and withdrawal

Remove a correction-requested, rejected or withdrawn item from the current catalog and remove its delivery release asset. Never upload an unapproved replacement. Re-admit only after exact-version approval.

Do not silently alter approved images, copy or disclaimers. Check disclosure in artwork and primary text; do not assume the ad description is displayed.

## Current state

- Repository and operating files initialized.
- Zero artwork entries in `catalog.json`.
- No media release initialized or artwork published by this setup.
- No ad-platform credentials stored here.
- No dependency on the landing-page deployment.
- Next prototype: connect release-asset upload, publish one approved image, then verify GitHub → platform upload → paused preview.

## Files

- `catalog.json`: current approved delivery media.
- `catalog.schema.json`: catalog format.
- `AGENTS.md`: operator instructions.
- `.gitignore`: ordinary staging allowlist. This is not a security boundary and cannot prevent forced commits.
