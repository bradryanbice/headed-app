---
kicker: "Help"
title: "Support"
description: "How to get help with Headed, and answers to the questions that come up most — including why there's no turn-by-turn."
---

Headed has no accounts, no subscriptions, and no support portal. The [contact form](#contact) at the bottom of this page reaches a person directly.

## What to include when something goes wrong

The more of this you have, the faster it gets fixed — but send what you have and don't worry about the rest:

- What you were trying to do, and what happened instead.
- Your iPhone model and iOS version (Settings → General → About).
- Roughly where you were, or what route you were on. A city pair is plenty; please don't send an exact address you'd rather not share.
- A screenshot, if the problem is visible.

## Questions that come up most

### Where's the turn-by-turn navigation?

There isn't any, and that's deliberate. Headed shows you the *whole* trip — your entire route, where you are on it, how far is left, and what's worth stopping for. When you want spoken directions and lane guidance, tap **Open in Apple Maps** and Headed hands the route across, stops included.

Turn-by-turn is Apple Maps' job. Seeing the whole trip is Headed's. Running both is the intended way to use it.

### Why does Headed want my location?

Two reasons, both while the app is open:

1. To work out the route from where you actually are.
2. To track progress along it — distance driven, percent complete, distance left.

Headed asks for "When In Use" only. It never requests background or Always access, and it doesn't follow you when the app is closed. If you decline, you can still search destinations and preview routes; live progress is what stops working.

### A route, distance, or arrival time looks wrong

Routing, place data, and travel times come from Apple Maps' data, the same source Apple Maps itself uses. Headed doesn't compute its own. If a route looks wrong in Headed, it will generally look the same in Apple Maps — and Apple has a **Report an Issue** flow that gets it corrected at the source.

Always follow road signs and conditions over anything on a screen.

### A place is missing, closed, or in the wrong spot

Same answer, with one addition: EV charging data can also come from [Open Charge Map](https://openchargemap.org/), a community-maintained database. Corrections submitted there flow back into the app.

### Weather, hazards, or EV charging aren't showing

Those features are scoped to the **United States** in this version. Weather and severe-weather alerts come from Apple Weather; the precipitation radar layer comes from [RainViewer](https://www.rainviewer.com/). All three need a network connection, and the weather layer has to be switched on in the **Map Layers** panel — the layers button beside the gear, top right.

### I turned something on and can't find it again

Every map layer — Traffic, Weather, Hazards, and Landmarks — lives in one place: the **layers button** in the top-right corner, next to the gear. A dot on that button means at least one layer isn't at its default.

### Can I get my data back after deleting the app?

No, and there's no way around it. Headed has no server, so saved places, recent destinations, and preferences exist only on your device. Deleting the app deletes them, and there's no backup to restore from. That's the trade for having nothing about your trips stored anywhere else.

### Does Headed work outside the United States?

Routing, search, and the map work anywhere Apple Maps does. The weather, hazard, and EV charging features are US-only in this version.

## Reporting a privacy concern

Use the [contact form](#contact) below. The [Privacy Policy](/privacy/) sets out exactly what stays on your device and what each outside service receives.

## Contact {#contact}

Questions, bugs, or something that behaved oddly on a drive — this goes straight to email.

<div class="formwrap">
<!-- Netlify Forms. The three attributes below are the whole wiring: Netlify's
     post-processing parses the DEPLOYED html, finds the form by `name`, and
     starts accepting posts at this same path. `data-netlify` is the documented
     spelling of the bare `netlify` attribute and is valid html5. The hidden
     form-name input is what attributes a submission to this form — without it
     the post is accepted and filed nowhere. bot-field is the honeypot: real
     people never see it, bots fill it, and Netlify silently drops those.
     NOTE: no blank line anywhere inside this block. A blank line ends Goldmark's
     raw-html block, after which the indented continuation lines parse as an
     indented CODE block and the rest of the page is mangled. -->
<form name="contact" method="POST" action="/thanks/" data-netlify="true" netlify-honeypot="bot-field">
  <input type="hidden" name="form-name" value="contact">
  <p class="hp"><label>Leave this field empty <input name="bot-field" tabindex="-1" autocomplete="off"></label></p>
  <div class="field">
    <label for="cf-email">Your email</label>
    <input id="cf-email" type="email" name="email" required autocomplete="email">
  </div>
  <div class="field">
    <label for="cf-subject">Subject</label>
    <input id="cf-subject" type="text" name="subject" required>
  </div>
  <div class="field">
    <label for="cf-message">Message</label>
    <textarea id="cf-message" name="message" required></textarea>
  </div>
  <button class="btn btn-primary" type="submit">Send</button>
  <p class="formnote">Your address is used to reply to you and nothing else. It isn't added to a list, because there is no list.</p>
</form>
</div>

## Legal

- [Privacy Policy](/privacy/)
- [Terms of Use](/terms/)
