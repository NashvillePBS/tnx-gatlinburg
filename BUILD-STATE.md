# Build state — A Traveler's Guide to Gatlinburg

Built 2026-07-18 from the locked Memphis design system (content-only clone).
All four formats: web guide, home-print itinerary, brochure TIFFs, front SVG.

## Neighbor-towns decision (FOR SHANE'S REVIEW)

Gatlinburg's City List yielded only **6 eligible stops** (<8 threshold), so per the
build rule the guide also pulls **Pigeon Forge** and **Sevierville**: title stays
"to Gatlinburg", the sub and mapLede nod to the Smokies corridor. Neighbor stops:
The Old Mill Square, Titanic Museum, Smoky Mountain Winterfest (Pigeon Forge);
Tennessee Museum of Aviation (Sevierville). Hippensteal's Mountain View Inn is
tagged Gatlinburg in Airtable but its address (4201 Tatem Marr Way, 37876) is
Sevierville-side; kept, between the two towns.

## Records → eligible

- Airtable: 25 Gatlinburg records + 4 neighbor records (Pigeon Forge 3, Sevierville 1) = 29 considered.
- **14 eligible stops** (live tennesseecrossroads.org permalink, deduped, not closed/do-not-publish).
- 4 of the 14 had a live page found by slug probe though the Airtable
  `Wordpress Permalink` field is empty (verified 200): Crockett's Breakfast Camp,
  Tennessee Jed's, Hippensteal's Mountain View Inn, Michael Copas. **Airtable
  permalink fields were NOT written back (write access is lat/lng only) — worth
  backfilling in Airtable later.**

### Excluded (15) and why

| Record | Reason |
|---|---|
| Buckhorn Inn | no live permalink (probe 404) |
| Hippensteal's (2010 Joe Elmore dup) | duplicate place; kept 2021 Laura Faber record |
| Great Smoky Mountains National Park | no permalink (probe 404) |
| Gatlinburg (city record) | no permalink; not a stop |
| Gatlinburg Chamber of Commerce | no permalink (404) |
| Gatlinburg Arts & Crafts Community (Kip Kirby dup) | duplicate of Arts & Crafts Loop record, which has the permalink |
| Arrowmont — First visit (dup) | duplicate; kept "Revisited" record with permalink |
| Ogle's Broom Shop | no permalink (404) |
| Ogle's Chair Shop | no permalink; Website field is garbage ("Ogle's Chair Shop") |
| Smoky Mountain Dulcimers | no permalink (404) |
| Gatlinburg Lights | no permalink (404); Winterfest covers the same story |
| Greenbrier Restaurant | no permalink (404) |
| Lorelei Candles | no permalink (404); no website |
| The Historic Gatlinburg Inn | no permalink (404, several slugs tried) |
| Ripley's Aquarium of the Smokies | no permalink (404) |

No record was excluded as "confidently gone"; none carried Closed/Do-not-publish flags.

## Sections + counts (14 stops)

1. Eat & Drink — 2 (Crockett's, Tennessee Jed's)
2. See & Explore — 6 (SkyBridge, Salt & Pepper Museum, Old Mill Square, Titanic, Aviation Museum, Winterfest·Seasonal)
3. Stay a While — 2 (Mt. LeConte Lodge, Hippensteal's)
4. Makers — 4 (Great Smoky Arts & Crafts Community, Arrowmont, Dinwoodie, Michael Copas)

## Pins / geocoding

- **10 pinned / 4 card-only.** Card-only: Winterfest (region-wide seasonal event —
  EPB-Windows precedent), Mt. LeConte Lodge (hike-in lodge; the street address is the
  Sevierville reservations office — pinning it would mislead), Dinwoodie Metal
  Sculptors (see flags), Michael Copas (no address at all).
- Geocoded 1 record via Nominatim and wrote back to Airtable: **Titanic Museum**
  (recYVtnWsikraojFO → 35.8205643, -83.5789070; Nominatim matched the museum itself).
- All other pins used existing Airtable coordinates; all sanity-checked near (35.71, -83.51) corridor.
- "Old Mill St" address verified against OSM/Nominatim — the street exists at exactly
  the record's coordinates.

## Phones (10 published)

SkyBridge, Tennessee Jed's, Salt & Pepper, Old Mill Square, Titanic, Aviation,
Mt. LeConte (reservations line), Hippensteal's, Arts & Crafts Community (association
office), Arrowmont. All normalized (XXX) XXX-XXXX. Withheld: Dinwoodie (invalid
area code, see flags), Michael Copas (artist/personal), Crockett's + Winterfest
(no phone in record).

## Flags for review

1. **Dinwoodie Metal Sculptors** — record phone "(942) 232-1830" has a non-existent
   US area code (withheld); no website; Web Description says the couple is in
   **Dandridge**, while the address (170 Glades Rd, 37738) looks like a Gatlinburg
   gallery. Gallery's current status unverifiable within allowed network. Card runs
   pin-less and phone-less; consider confirming or cutting before print.
2. **Mt. LeConte Lodge** — listed address/phone are the booking office
   (250 Apple Valley Rd, Sevierville); blurb makes clear the lodge itself is hike-in.
3. **Old Mill Square phone** (865) 806-6002 is from Airtable; pattern looks like a
   mobile number — worth confirming it still rings the Square.
4. **Tennessee Jed's, Hippensteal's, Michael Copas** — Talent field empty in Airtable;
   hosts (Miranda Cohen / Laura Faber / Miranda Cohen) taken from the Web Description text.
5. **Winterfest ZIP/site** — record points at mypigeonforge.com; event spans the
   whole corridor. Card-only, marked Seasonal.
6. 2016 wildfire check: all included Gatlinburg stops are post-fire-verifiable via
   their 2019–2026 segment pages (SkyBridge segment is explicitly about the recovery);
   the only open question is Dinwoodie (flag 1).

## Cover

**Pick:** `brochure/cache/cover-gatlinburg.jpg` — The Old Mill waterwheel, Pigeon Forge
(from old-mill-square.jpg, 1920×1080; crisp true photograph, strong subject, prints
clean at panel size). Caption: "The Old Mill, Pigeon Forge". Note: cover subject is a
neighbor-town stop — flagging since the title says Gatlinburg.
Rejected after viewing: gatlinburg-skybridge.jpg (soft interlaced video still, though
it is the most "Gatlinburg" subject — swap candidate if Shane prefers subject over
sharpness), GatlinburgArtsandCraftsLoop.jpg (cluttered workbench close-up, vendor
label visible), mt-leconte-lodge.jpg (blurry rooftop frame, no subject).

## Build verification

- fetch_mapdata: 1,314 ways cached (one attempt, no retries needed).
- build_brochure.py + export_svg.py ran clean; front/back proofs visually reviewed:
  all 5 main-map pins right of the reserved box column (x ≥ 8.1in), inset "Downtown
  Gatlinburg" holds stops 1–4 & 12 with leader-line displacement working, park label
  in open terrain, back side fits listings in ~4.5 panels with QR/welcome/cover intact.
- Web: http.server :8754 — index.html 200, data/guide.json 200/valid, 14 stops render config.
- **Diff vs tnx-chattanooga system files: IDENTICAL except exactly the 4 permitted
  head lines** (title, meta description, og:title, og:description). No drift.

## Leaks

None. No system file needed modification; all city specifics live in data/guide.json.
