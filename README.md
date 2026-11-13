# Ad Media Bridge

Public delivery bridge for current, approved advertising artwork across Meta and other ad platforms.

## Admission rule

Only upload the exact approved version of an asset that is still approved for use. Never upload rejected artwork, correction drafts, superseded artwork, editable source files, strategy documents, customer information, credentials or access tokens. A FINAL folder or filename is not proof of current approval.

## Keep artwork out of Git history

Do **not** commit artwork into Git: Git retains old versions after replacement or deletion.

Use one mutable GitHub release tagged `current` for delivery assets. Replace or remove its files when approval changes. Do not create archival media releases, version folders or backup copies in this bridge. Text configuration and catalog history may remain in Git; artwork must not.

The `current` release contains the six approved ECC9BF PNG formats from FINAL. `catalog.json` records their verified source checksums and stable release URLs.

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

Release upload/removal works through the authenticated GitHub CLI API. Meta rejected the ordinary GitHub release URL; importing the public `release-assets.githubusercontent.com` delivery URL resolved from that release succeeded. Resolve a fresh delivery URL immediately before each platform upload; it expires and must not be stored as the permanent catalog URL. This repository alone does not automate publication.

## Corrections and withdrawal

Remove a correction-requested, rejected or withdrawn item from the current catalog and remove its delivery release asset. Never upload an unapproved replacement. Re-admit only after exact-version approval.

Do not silently alter approved images, copy or disclaimers. Check disclosure in artwork and primary text; do not assume the ad description is displayed.

## Current state

- Repository and operating files initialized.
- Six verified ECC9BF image entries in `catalog.json`.
- One mutable `current` release; no artwork committed into Git.
- No ad-platform credentials stored here.
- No dependency on the landing-page deployment.
- GitHub → Meta image upload verified for all six ECC9BF formats.
- One paused ECC9BF ad created through the Meta plugin; Feed, Stories, Reels and square fallback reviewed in-app. Meta uses the 4:5, 9:16 and 1:1 formats; other exports remain available for appropriate platform use.

## Files

- `catalog.json`: current approved delivery media.
- `catalog.schema.json`: catalog format.
- `AGENTS.md`: operator instructions.
- `.gitignore`: ordinary staging allowlist. This is not a security boundary and cannot prevent forced commits.

## Tested Meta build contract

Keep one ad per content ID, with its format variations inside the ad. Use the content ID in the ad name, for example S01-01-I01 - ECC9BF. Do not create separate ads for aspect ratios.

The tested placement-controlled recipe uses asset_feed_spec.optimization_type = PLACEMENT, media labels, uniquely labeled copy sets and one body/title/description per placement rule. Page and Instagram identity stay in object_story_spec. The existing instant form is retained through asset_feed_spec.call_to_actions[].value.lead_gen_form_id. No new form is required.

Five approved copy variations can coexist in that one ad when assigned to placement groups. This is not random text rotation across every placement. Do not silently drop copy variants or claim random optimization.

Verify actual saved placement previews: image arrays alone do not prove selection. Omitting the placement mode classified the tested asset feed as Dynamic Creative and caused placement restrictions; DOF mode did not apply the requested image mapping. Explicit PLACEMENT mode rendered the tested Feed, Stories and Reels with the intended ratios.

For the tested Meta static pack, use 4:5 for Feed, 9:16 for Stories/Reels and 1:1 as the fallback. Keep the other approved export ratios in the bridge for platforms where appropriate; do not force every export into Meta placements.

Keep all review builds paused. Detailed platform IDs, request payloads, diagnostics and screenshots belong in private project records, not this public repository.
