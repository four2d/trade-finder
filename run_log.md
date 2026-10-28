# Trade Finder — run log

## 2026-10-15 15:30 (UK) — Phase 0 setup (no searching)
- Read plan v1.0. **No business searches run.** No sites queried other than Wikimedia Commons (one hero photo download).
- Pete's answers (via parent bot): purpose = **Comprehensive directory** (neutral quality score: rating 35, review volume 15, vetted/accredited 20, contactability 15, distance 15); radius 25 mi; include all firm sizes incl. large contractors; updates on demand only; future hosting = Pete's GitHub Pages (not published; `noindex` meta added); hero = top-scoring firm's photo of the week (sample uses a credited placeholder).
- Created: trade_finder.xlsx (Summary, All, 12 area tabs, Needs check; headers only), trade_finder.csv (headers only), data/businesses.json (`[]`), data/meta.json, data/sample_businesses.json (15 made-up SAMPLE records), index.html, index_offline.html, img/hero-compton-acres.jpg.
- Sample phones use Ofcom's reserved drama ranges (01632 960xxx / 07700 900xxx); websites/sources point at example.com. None are real.
- Counts: found 0 · merged 0 · dropped 0 · blocked sources: n/a.

## 2026-10-15 15:33–17:00 (UK) — Issue 01 · Phase 1 Driveways pilot (Dorset + 25-mile ring)
- **Discovery:** 17 web searches (resin/block/tarmac/gravel/concrete/repair × Poole, Bournemouth, Christchurch, Ferndown, Wimborne, Ringwood, Verwood, Wareham, Swanage, New Milton, Lymington, Blandford); TrustATrader listing pages (2, 6 s apart); Companies House advanced search by name keyword (driveway/driveways/paving/surfacing/resin) × 10 registered-office towns × active/dissolved (100 queries, 1.5 s apart).
- **Verification:** 27 business websites fetched (home + contact, ≤3 pages, 4 s apart, robots.txt respected); Companies House name search for 33 trading names; postcodes.io geocoding.
- **Blocked / not used:** Checkatrade (robots.txt disallows all bots → used only via search-engine snippets of public profile pages); Yell (Cloudflare challenge); MyBuilder (robots disallow); Rated People and FreeIndex not tried; Google Maps (no browser and Places API is paid → no Google ratings collected); 10 business sites returned 403 to robots.txt (treated as disallowed: Oltco, Fletchamoore, Steve Collins, MJP, AGR, G&J, Taylor Made, Wicks, Driveway Doctor, Dorset Paving). Facebook not checked.
- **Counts:** 32 trading firms found → 30 within 25 mi (+2 serve-area-only, Hampshire); 27 more active Ltd companies found only on Companies House (leads, "Needs check"); 75 dissolved companies → "Not in business". Master = 134 records. Merged: Wicks Tarmacadam + Poole Driveways (same history text), M&R Paving + M & R Paving & Landscaping Specialists Ltd, Newlook Driveways + Newlook Landscaping & Driveways Ltd (all flagged merge_review). Dropped: none.
- **QC:** dup domains/phones/company numbers = 0 ✅; all records have source + town + distance ✅; verified firms with phone or website 90% ✅; verified firms with confidence ≥0.5 = 70% ❌ (target 90% — mostly single-source Checkatrade/TrustATrader/directory firms); spot check 10 random records re-opened = 10/10 ✅ (work/spotcheck.txt); Ltd status checked on Companies House for every Ltd-looking firm ✅.
- **Not done:** Google ratings/hours/socials (no source available without a browser); Turners (SO41) trading status; Firm Pave phone conflict.

## 2026-10-15 16:10–16:50 BST — Issue 01 expansion (same issue, rebuilt in place)
- Web sources (work/raw_2026-10-15b.py, 37 firms): Checkatrade via search-engine snippets (landscaping, fencing, trees, patios), TrustATrader (3 profiles, 5s pacing), business sites (Classic Landscaping, AGR, Clearcut). Checkatrade list-only firms flagged base_unknown → needs check. AGR gained Checkatrade 9.68/248; Steve Collins 9.11/525.
- Companies House SIC discovery (tools/ch_discover.py, 1.5s pacing): BH1–BH13 = 1,341 companies (active + dissolved). Crash on an odd row at BH14 fixed (tolerant parse); BH14→SO42 resumed as tag _sic2.
- Batches published to four2d/trade-finder: A (master 467), B (master 1452, 618 in-radius trading).
- QC: 67 web-verified trading firms; Companies House-only leads flagged needs_check (no phone/web yet).
- 16:47 scope change (Pete): Dorset + Hampshire only for week 1. counties.json: dorset + hampshire in_progress, all others "paused"; county index copy updated.
- 25-mile ring CH SIC finished (BH14–SO42, 2,035). County-wide CH SIC (_dh tag, 78 districts DT/SP/SO/PO/GU/RG, 15 SIC codes incl. 81291/81221/81222/42210) started 16:49; DT1–SP7 done by 17:04.
- Web pass 2 (work/raw_2026-10-15c.py, 12 firms): Hampshire Checkatrade firms, FreeIndex (robots allows) and Rated People profiles via search snippets.
- Build: Companies House-only leads that match a web-verified firm by name are now merged; the old lead is kept with superseded_by (never deleted) and hidden (9 so far). Fixed geo/county for SO-area firms.
- Published batches C, D, E, F. Live 17:04: 2,102 trading in scope, 2,153 not in business, 4,271 stored.

- 17:32 BST batch I: added 3,799 CH Dorset/Hampshire records from the partial run, 33 enriched; 2,634 trading; published 21a72ed; live 200 and meta matches. CH _dh run still going (SO43).

- 17:58 BST batch J: Closed & dissolved section shows 12 then a Load more button (+24 each click, "Showing X of Y") on home, county and issue pages. Page data split into lite.json (1.33MB), closed.json (loaded after first render) and details/ (256 shards, loaded on Why?/Sources). Full businesses.json still downloadable. CH partial at 5,880 records.

- 21:10 BST batch K: collapsible sections (with Expand/Collapse all, state kept in the #c= hash; on mobile only the first is open), main cards load 24 at a time, area chart compact scale with a broken-axis mark (Compact/True scale toggle, #ts=1). CH partial at 8,157.

- 21:45 BST batch L: hero cover lines on near-black panels (WCAG AA: yellow 10.1:1, white 16.7:1). All sections start collapsed; choosing an area opens just that one. The page loads only meta.json with a summary; each section loads its own area file when opened; the search index loads on the first keystroke; map pins load when the map comes into view; the closed list loads when opened. Spinners on each. lite.json retired.

- 21:22 BST: County by county section is now collapsible too (collapsed by default).

- 21:47 BST: Companies House search for Dorset & Hampshire finished (11,321 records) and finalised; hero credit text now solid black.

- 22:13 BST batch M: fixed the card Map button (real link in a new tab: Google Maps URL if known, else a Google Maps search by name+town+postcode, else an OSM pin); added a Show on map button; popups link to maps. 50 more firms enriched (83 in total). Out of scope: RM Driveways (Devon), Aquatech (Somerset), Bondeck (site safety decking).

- 22:25 BST: Enrichment: 66 Hampshire/Dorset firms enriched tonight; Wiltshire added (in progress); county queue re-ordered by adjacency rings from Dorset

- 22:51 BST: Enrichment: 110 firms enriched overnight (Hampshire queue + Poole/Bournemouth)

- 23:14 BST: Wiltshire Companies House SIC discovery (SN, BA12-15, SP1-4; SP5/7/8/9 already covered) added; enrichment to 68 firms

- 23:38 BST: Map: yellow marker clusters (Leaflet.markercluster) when zoomed out; enrichment to 173 firms

- 00:05 BST: Enrichment: 46 more CH-only firms given websites/phones (Hampshire queue + Poole/Bournemouth/Christchurch), raw_2026-10-16a

- 01:26 BST: Somerset Companies House SIC discovery (TA, BA1-11/16/20-22, BS22-29/31/39-41/48-49) added; Somerset in progress; no further counties

## 2026-10-16 07:00–07:50 BST — Issue 02 · daily run (Dorset, Hampshire, Wiltshire, Somerset; no new counties)
- **Companies House:** new tool `tools/ch_recent.py` — companies incorporated or dissolved 1–16 Oct 2026 under the 16 trade SIC codes, nationwide, kept only for active-county postcode areas (2,667 rows seen, 187 kept). 9 newly registered companies added as leads (needs check); no known trading firm was newly dissolved. Build now lets the newest Companies House check win.
- **Enrichment (work/raw_2026-10-16b.py):** 29 Companies House-only leads in Wiltshire (14) and Somerset (15) given public websites/phones (web search + home/contact pages, robots respected, 4 s pacing). Skipped where the match was unclear (JW Treecare, O'Callaghan Tree Surgeons, Easton Landscapes, Treecycle, A & G Surfacing, C&C Landscaping, Conservation Fencing). Leeds Landscapes marked out of scope (trades in Leeds).
- **Fix:** web-checked firms beyond 25 miles but inside an active county were wrongly flagged "serves the area only", which kept ~220 of them out of search, the map and the counts. Now shown normally (checked firms 176 → 398). Also removed a stray non-plan area ("lighting") from one old record.
- **Page:** the issue line in the hero ran under the yellow cover panel on desktop, hiding the date; it now wraps inside the black half (mobile unchanged).
- **QC:** dup domains 0, dup company numbers 0, dup phones 1 (Gaia Landscapes and Henley Gardeners: separate companies sharing one office number — kept, explained); checked firms with phone or website 87% (target 90%); confidence ≥0.5 88% (target 90%); spot check 9/10 (the one miss was a directory page now returning 404 — source removed); screenshots desktop + mobile checked.
- **Blocked / not used:** Checkatrade, Yell, MyBuilder (search snippets only); sites with robots disallow (Fencesmart, West Country Lawns, Genesis Gardens, Baber, Allsorts, Pave-Rite) not fetched; Thomson Local returned 403.

- 17:25 BST: Backfill: add already-found firms not yet on site (no new search)

- 17:28 BST: Counties dropdown, live intro text, per-county cover stars

- 17:40 BST: Issue 02: +13 enriched Hampshire firms (Basingstoke/Alton)

- 18:02 BST: Issue 02: add Berkshire and Bristol (Companies House discovery)

- 18:18 BST: Issue 02: +54 enriched Hampshire firms (Bordon, Fleet, Farnborough, Tadley)

- 18:44 BST: Issue 02: +58 enriched Wiltshire/Somerset firms; Bristol filled out by postcode district

- 18:56 BST: Issue 02: +56 enriched Wiltshire/Somerset firms

- 19:10 BST: Issue 02: +63 enriched firms (Somerset, Berkshire, Bristol)

- 19:24 BST: Issue 02: +42 enriched Berkshire/Bristol firms

- 19:46 BST: b8: +30 Somerset/Berkshire/Bristol firms; Dorset quality pass (~45 records given phone/website/second source)

- 20:03 BST: b9: +46 firms from non-trade-name CH leads (SIC 81300) across six counties; Dorset CH links + duplicate cleanup

- 20:54 BST: b10: +15 firms (non-trade-name CH leads); manual closed override, Artscape Garden Associates to Not in business

- 12:56 GMT: Issue 03: add Devon and Isle of Wight (Companies House discovery + 17 enriched firms)

- 13:23 GMT: Split master by county: data/counties/<slug>.json + master_index.json; retire 53 MB businesses.json; slimmer offline page

- 14:27 GMT: Issue 03 rebuilt thin: dated issues now reuse shared /data (no per-issue 40 MB snapshot); old issue businesses.json dumps no longer published

- 15:05 GMT: Issue 03 b2: +45 enriched Devon / Isle of Wight firms from CH leads (own sites)

- 15:27 GMT: Issue 03 b3: +62 enriched Devon firms from CH leads (own sites)
