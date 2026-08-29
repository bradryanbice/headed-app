---
kicker: "Legal"
title: "Privacy Policy"
description: "What Headed collects, where it stays, and exactly what each outside service receives."
---
**Last updated:** August 24, 2026

Headed is a journey-overview companion for driving: it shows your whole route, where you are on
it, and what's nearby, then hands off to Apple Maps for turn-by-turn navigation. This policy
explains what information Headed uses, where it lives, and who it's shared with.

## The short version

- **No account, no login, no user-generated content.**
- **No analytics, no ad tracking, and no third-party SDKs bundled in the app.** The two outside
  services Headed talks to (below) are plain HTTPS requests, not embedded tracking libraries.
- **Nothing is uploaded to a server Headed controls** — there isn't one. Everything Headed
  remembers about you lives on your device only.
- **Uninstalling the app deletes everything.**

## Information Headed collects, and why

**Precise location.** Used while the app is open to calculate your route, show your live progress
along it, and find things nearby (parking, food, gas, EV charging). Location access is optional —
you can still search for and view a destination manually without granting it.

**Destinations you search for or route to.** Needed to plan and display your route.

**Saved places.** If you set a Home, Work, or other custom saved place, that address is stored so
you can start a route to it quickly.

**Recent destinations.** The last 10 destinations you've successfully routed to, so they're easy
to pick again. Older entries are automatically removed once you pass 10.

**Preferred brands.** If you set preferred brands for Food, Gas, or EV charging in Settings, those
names are stored so Headed can prioritize them in search results.

**Trip snapshot for crash recovery.** While you're actively routed somewhere, Headed keeps a small
record of your destination and progress so that if the app is closed or the phone restarts, your
trip can resume. This snapshot expires automatically after 12 hours.

**App preferences.** Settings you choose — map layers, units, avoidance preferences, and similar —
so the app remembers your choices between sessions.

None of the above requires or creates an account. It's all tied to your device, not to an identity
Headed maintains.

## Where this information lives

Everything above is stored **only on your device**, using standard iOS local storage (the same
mechanisms any iOS app uses to remember your settings). Headed has no backend server, so there is
nothing to upload it to. It is never sold, and it is never used for advertising.

## Who Headed shares information with

Headed relies on a few outside services to function. Here's exactly what each one sees:

**Apple (MapKit, WeatherKit, Core Location).** Search queries, route requests, and location are
sent to Apple to calculate routes, search for places, and fetch weather forecasts and alerts. This
is standard MapKit/WeatherKit usage and is covered by
[Apple's own privacy policy](https://www.apple.com/legal/privacy/).

**RainViewer.** When the optional weather radar layer is on, Headed requests precipitation radar
tiles for the area you're viewing. RainViewer sees the map area being requested; it does not
receive your saved places, search history, or any identifying information. See
[RainViewer's privacy policy](https://www.rainviewer.com/privacy.html).

**Open Charge Map.** When searching for EV chargers, Headed sends an approximate location or
bounding box to look up nearby charging stations. Open Charge Map sees that location query; it
does not receive your saved places, search history, or any identifying information. See
[Open Charge Map's license and privacy policy](https://openchargemap.org/about/terms).

Headed reads from both services anonymously — it holds no account with either, and neither
receives anything that identifies you or your device beyond what any web request carries.

Neither RainViewer nor Open Charge Map is a bundled SDK — Headed talks to them the same way a web
browser talks to a website, over plain HTTPS, only when their feature is actively in use.

## How long information is kept, and how to remove it

- **Recent destinations** are capped at 10 and older ones are pruned automatically.
- **The active-trip snapshot** expires automatically after 12 hours.
- **Saved places, preferred brands, and app preferences** persist until you change or clear them
  in Settings, or until you delete the app.
- **Uninstalling Headed deletes all of the above.** There is no server-side copy to separately
  request deletion of, because nothing is ever sent to a Headed-controlled server in the first
  place.

## Location permission

Headed requests location access only to show your position on the route and find nearby places.
It does not request "Always" location access and does not track your location in the background.
You can grant, deny, or revoke location access at any time in your device's Settings app; denying
it does not block you from using Headed — you can still search for and view routes manually.

## Weather and EV features

The weather layer, weather hazard alerts, and EV charging features are scoped to the United States
in this version of the app.

## Children's privacy

Headed is not directed at children and does not knowingly collect information from children. It
has no age gate because it collects no information tied to an identity in the first place.

## Changes to this policy

If this policy changes, the "Last updated" date at the top will change too. Material changes will
be reflected here before they take effect.

## Contact

Questions about this policy or how Headed handles information can be sent through the
[contact form](/support/#contact).


