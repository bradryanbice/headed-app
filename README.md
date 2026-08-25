# Headed — public site

The public site for [Headed](https://github.com/bradryanbice/headed), a journey-overview companion
app for Apple Maps. Served by GitHub Pages at <https://bradryanbice.github.io/headed-app/>.

Only public-facing pages live here — the app's source and internal docs stay in the private
`headed` repo.

| Page | Path | Source of truth |
| --- | --- | --- |
| Landing | `index.md` | this repo |
| Privacy Policy | `privacy.md` → `/privacy` | `docs/privacy.md` in `headed` |
| Terms of Use | `terms.md` → `/terms` | `docs/terms.md` in `headed` |

**The legal pages do not auto-sync.** `docs/privacy.md` and `docs/terms.md` in the private repo are
the sources of truth; when either changes, update the copy here too. The published copies drop the
internal "source copy" note that the private originals carry at the top.

This repo was renamed from `headed-privacy` (2026-08-24) when it grew past hosting just the privacy
policy. Nothing external referenced the old URLs at the time of the rename.

## Still to do (tracked as [#23](https://github.com/bradryanbice/headed/issues/23))

- Feature section with screenshots — copy exists in `docs/app-store-submission-copy.md`, imagery
  exists in the captured App Store screenshot set.
- Download / TestFlight-beta link — blocked until an External TestFlight group exists.
