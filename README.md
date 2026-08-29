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

The old GitHub Pages deploy (`.github/workflows/hugo.yml`, plus `static/CNAME`) is **still in place
on purpose** — see the cutover checklist below. It comes out once headedapp.com is confirmed
serving from Netlify, not before.

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

`static/CNAME` holds the custom domain **for GitHub Pages only** — Netlify takes the domain from its
own settings and ignores this file. `static/assets/img/` holds the app screenshots at native
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

The form **cannot work on GitHub Pages** — Pages is static-only with no form handler, so a submission
405s. It only works once Netlify is serving.

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

## Netlify cutover checklist

In this order. Steps 1–3 are safe and reversible; DNS is the point of no easy return.

1. **Create the Netlify site** from this repo. It reads `netlify.toml`, so there is nothing to
   configure in the UI.
2. **Verify on the `*.netlify.app` URL before touching DNS** — all five pages, and **submit the
   contact form for real**. A submission must appear under *Forms*. This is the only way to confirm
   Netlify detected the form; the markup looking right proves nothing.
3. **Set the email notification** (*Forms → Form notifications*), then submit once more and confirm
   the mail arrives.
4. **Add `headedapp.com` and `www.headedapp.com`** as domains on the Netlify site.
5. **Delegate DNS**: point the Namecheap nameservers at Netlify DNS. Wait for the Netlify
   certificate to issue for both hosts.
6. **Verify the live domain**: apex and `www` both 200 over HTTPS, `www` 301s to the apex, and the
   form still works on the real domain.
7. **Only then, retire GitHub Pages**: remove the custom domain in the `headed-app` repo's
   *Settings → Pages*, then delete `.github/workflows/hugo.yml` and `static/CNAME`.

> **The window in between.** Merging the Netlify branch to `main` before step 2 publishes the form
> to the *GitHub Pages* site, where it renders but 405s on submit. The site has no traffic yet, so
> this is cosmetic — but don't leave it sitting there.

> **`bradryanbice.github.io/headed-app/*` stops redirecting** once the Pages custom domain is
> removed in step 7. Those URLs currently 301 to headedapp.com. Nothing external references them
> (the domain cutover happened before any release), but it is a real change, not a no-op.
