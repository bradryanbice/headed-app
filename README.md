# headedapp.com

The public site for [Headed](https://github.com/bradryanbice/headed), a journey-overview companion
app for Apple Maps. Live at <https://headedapp.com>.

**Hugo**, deployed by **Netlify** from `netlify.toml` — the same host as bradbice.com,
playoffsbracket.com, royalrumblestats.com and calaround.app. Build settings live in that file, not
in the Netlify UI: build command, publish directory, `HUGO_VERSION`, redirects and headers are all
committed here, so changing them in the dashboard would be overwritten on the next deploy.

`netlify.toml` mirrors calaround.app, which is the closest sibling — same Hugo version, and no
dart-sass step, because this site's one stylesheet is plain CSS through Hugo's own pipeline rather
than SCSS.

DNS is **Netlify DNS** (nameservers delegated from Namecheap), so the apex and `www` are both
Netlify records. `www` is a domain alias that 301s to the apex via `netlify.toml`.

GitHub Pages is **retired**. The workflow that built and published the Pages artifact, and the
`static/CNAME` that held the custom domain for it, were deleted on 2026-08-29 once Netlify was
confirmed serving. The repo has no `.github/` directory at all now — that workflow was its only
occupant. Netlify is the sole deploy path.

```
hugo server        # local preview
hugo --gc --minify # production build into public/
```

## Layout

| Page | Source | URL |
| --- | --- | --- |
| Landing | `layouts/index.html` | `/` |
| Support | `content/support.md` | `/support/` |
| Privacy Policy | `content/privacy.md` | `/privacy/` |
| Terms of Use | `content/terms.md` | `/terms/` |
| Message sent | `content/thanks.md` | `/thanks/` (unlisted) |

The stylesheet lives in `assets/css/site.css` (Hugo's asset pipeline), **not** `static/` — it is
minified and **fingerprinted**, so the published filename carries a content hash. A changed
stylesheet is therefore a new URL and can never be served stale from cache, which is what lets
`netlify.toml` mark `/css/*` `immutable`. An *unfingerprinted* file published to `/css/` would be a
correctness bug, pinned in visitors' caches for a year. Images stay in `static/` because they don't
change.

`static/assets/img/` holds the app screenshots at native
1320×2868, converted to WebP — they are deliberately *not* downscaled, because the phone renders are
large and crispness was the point.

**The legal pages do not auto-sync.** `docs/privacy.md` and `docs/terms.md` in the private `headed`
repo are the sources of truth; update the copies here when either changes. The published copies drop
the internal "source copy" note the originals carry.

## Contact form

`/support/#contact` is a **Netlify Form**. There is no contact email anywhere on this site, by
design — an address rendered into a page gets scraped.

Three attributes are the entire wiring, and Netlify's post-processing parses the **deployed** HTML to
find them:

| Attribute | Role |
| --- | --- |
| `name="contact"` | names the form in the Netlify dashboard |
| `data-netlify="true"` | opts the form into Netlify's handler |
| `netlify-honeypot="bot-field"` | names the honeypot field |

Two things are easy to break:

- The hidden `<input name="form-name" value="contact">` is what attributes a submission to this
  form. Without it a post is **accepted and filed nowhere** — it looks like it worked.
- **No blank line anywhere inside the raw-HTML block in `support.md`.** A blank line terminates
  Goldmark's HTML block; the indented lines after it then parse as an indented *code* block, and the
  minifier truncates the rest of the page. This bit once already. The form's own HTML comment is
  written as one unbroken run for that reason.

The form only works on Netlify. Any static-only host — GitHub Pages, which this site used to run
on — has no form handler and answers a submission with a 405.

Submissions land in **Netlify → Forms**. Emailing them onward is a dashboard setting
(*Forms → Form notifications → Email notification*), not something this repo configures. The free
tier allows 100 submissions/month.

## Accessibility

The site holds the app's WCAG 2.1 AA floor. Two form values are deliberate and measured — don't
"harmonise" them away:

| Element | Token | Light | Dark | Needs |
| --- | --- | --- | --- | --- |
| Input border | `--ink-3` | 4.17:1 | 4.38:1 | 3:1 (1.4.11, component boundary) |
| `.formnote` | `--ink-2` | 8.12:1 | 8.66:1 | 4.5:1 (14px normal text) |

The decorative `--rule` hairline used elsewhere measures **1.36:1 / 1.21:1** as an input border —
effectively invisible — which is why inputs use `--ink-3` instead. And `--ink-3` on `.formnote` would
be 3.99:1 on light, below the text threshold, which is why that one goes the other way to `--ink-2`.

## Design

Direction B ("Cartographic") from [#24](https://github.com/bradryanbice/headed/issues/24): contour
ground, and the violet route line running down the features section as a spine with each feature
hanging off it as a waypoint. Palette derives from `HeadedDesignSystem` — accent `#5B21B6` light,
`#A78BFA` dark. Light and dark themes both supported.

## The Netlify cutover (done 2026-08-29)

Recorded because it went wrong in an instructive way, and because the same sequence applies to any
future host move.

The site was already Hugo; only the host changed. Netlify reads `netlify.toml`, DNS was delegated
to Netlify DNS, and GitHub Pages was retired afterwards.

**Three failures happened, in this order.** All three would have been invisible if DNS had still
pointed at Pages — the old host would have kept serving while they were sorted out.

1. **`exit code 127: hugo`.** `netlify.toml` had been written but not committed, so `main` — the
   branch Netlify built — did not contain it. Netlify fell back to the dashboard's build command
   and had no `HUGO_VERSION`, so there was no Hugo binary. **`commandOrigin: ui` in the log is the
   diagnostic**: it means the config file was not found in the built commit, not that its contents
   are wrong.
2. **A raw-HTML block silently truncated `/support/`.** See the Contact form section above. The
   build reported success.
3. **The build-skip rule canceled the first production deploy, and the site went down.** `main`
   never moved while the PR was open, so the merge commit's tree was byte-identical to the branch
   tip a deploy preview had already built. Netlify's cached ref pointed at that preview, the rule
   diffed preview against merge, found no change, and skipped — on a site with no published
   production deploy to fall back to. Every route served Netlify's plain-text "no published deploy"
   404. The rule is now disabled; `netlify.toml` carries the full account and the conditions for
   reinstating it.

**The ordering rule worth keeping:** delegate DNS *last*, and only after a real form submission has
landed in the dashboard from the `*.netlify.app` URL. DNS is the step that converts a build bug
into an outage. A build-skip optimisation in particular must never be live during a first
production deploy or a host cutover — it can save seconds and cost the whole site.

**Still open:** the GitHub Pages *site* is deleted from the repo, but if the custom domain is still
set under *Settings → Pages*, `bradryanbice.github.io/headed-app/` keeps 301ing to headedapp.com.
That redirect is currently harmless and arguably useful. Clearing it without disabling Pages
entirely would make that URL serve a stale duplicate of the site instead — the worse of the two
outcomes.
