# Blue Station: live content

This folder feeds the Blue Station homeworld and the public events page. Everything here is published by GitHub Pages at:

- Events page: https://blue0890.github.io/img-repo/station/
- Files the world reads: `https://blue0890.github.io/img-repo/station/<file>`

The images in the top of the repo are untouched. Worlds may be loading them by their links, so don't rename or move them.

## Posting an event

1. Open **Issues → New issue → ⭐ New Blue Star event** (or tap "Post an event" at the bottom of the events page).
2. Fill it in. You can drag a flyer image straight into the Flyer box. Submit.
3. A minute or two later a comment appears on the issue: ✅ if it's on the board, or ⚠️ with what to fix.

- **Change an event:** edit the issue. Paste the instance link in once the instance is open.
- **Take it down:** close the issue.
- Events disappear by themselves after they end.
- The board shows the next 6 events.
- Only events posted by **Blue0890** count. Issues from anyone else are ignored.

## Swapping photos and text (no world re-upload)

- **Photos:** replace a file in `photos/` (`01.jpg` … `08.jpg`) with a new image **of the same name**. Keep it at 2048 × 2048 pixels or smaller (VRChat refuses bigger ones); 1024 wide is plenty for a picture frame.
- **Text:** edit `world.json` (welcome message, a notice banner, the featured group, group taglines and links, photo captions).
- The world picks up changes when someone joins. GitHub Pages can take a few minutes to publish.

Adding *new* slots (another photo frame, a new sign) needs one world re-upload, because VRChat only allows web links that are built into the world.

## How it works (for Claude)

- `.github/ISSUE_TEMPLATE/event.yml`: the event form.
- `.github/workflows/events.yml` runs `.github/scripts/build_events.py` on issue changes and every 3 hours. It rebuilds `events.json` from open issues labelled `event` by allowed authors (`ALLOWED_AUTHORS` in the workflow), resizes flyers to `flyers/1.jpg` … `6.jpg` in board order (cached in `flyers/cache/`), comments the status on the issue, commits as github-actions[bot] and asks Pages to rebuild.
- `events.json`: `events[]` with `title`, `group`, `startUnix`/`endUnix` (UTC seconds), `world`, `worldId`, `instanceId`, `link`, `about`, `flyer` (path relative to this folder, or empty).
- VRChat limits: one string or image download every 5 s per world, images 2048 px max, URLs must be fixed at upload (`*.github.io` is a trusted domain).
