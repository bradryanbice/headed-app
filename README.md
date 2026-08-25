# headedapp.com

The public site for [Headed](https://github.com/bradryanbice/headed), a journey-overview companion
app for Apple Maps. Live at <https://headedapp.com>.

**Hugo**, deployed to GitHub Pages by `.github/workflows/hugo.yml`. GitHub Pages only builds Jekyll
natively, so the workflow builds the site and publishes it as a Pages artifact — the repo's
Pages source is set to **GitHub Actions**, not a branch. Changing it back to a branch will break
the deploy.

```
hugo server        # local preview
hugo --gc --minify # production build into public/
```

## Layout

| Page | Source | URL |
| --- | --- | --- |
| Landing | `layouts/index.html` | `/` |
| Privacy Policy | `content/privacy.md` | `/privacy/` |
| Terms of Use | `content/terms.md` | `/terms/` |

`static/CNAME` holds the custom domain. `static/assets/img/` holds the app screenshots at native
1320×2868, converted to WebP — they are deliberately *not* downscaled, because the phone renders
are large and crispness was the point.

**The legal pages do not auto-sync.** `docs/privacy.md` and `docs/terms.md` in the private `headed`
repo are the sources of truth; update the copies here when either changes. The published copies
drop the internal "source copy" note the originals carry.

## Design

Direction B ("Cartographic") from [#24](https://github.com/bradryanbice/headed/issues/24): contour
ground, and the violet route line running down the features section as a spine with each feature
hanging off it as a waypoint. Palette derives from `HeadedDesignSystem` — accent `#5B21B6` light,
`#A78BFA` dark. Light and dark themes both supported.

## Still to do ([#23](https://github.com/bradryanbice/headed/issues/23), [#24](https://github.com/bradryanbice/headed/issues/24))

- Download / TestFlight-beta link — blocked until an External TestFlight group exists.
- A dedicated support section, if the site is to be App Store Connect's Support URL.
- Optional: the dashboard photograph from #24, which would become the hero.
