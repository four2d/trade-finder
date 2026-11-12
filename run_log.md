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

- 15:49 GMT: Issue 03 b4: +48 enriched Devon firms from CH leads (own sites)

- 16:01 GMT: Issue 03 b4: +48 enriched Devon firms from CH leads (own sites)

- 07:46 GMT: Issue 04: +139 enriched firms across all live counties; latest Companies House changes
- **Issue 04 (30 Oct 2026, 07:21–07:50 GMT):** +139 web-verified firms from Companies House leads (own website carrying the company number or local postcode; 75 leads rejected as off-scope, mainly domestic/office cleaners). CH recent incorporations/dissolutions 28–30 Oct added. Yesterday's run never published: its raw file had a header bug (split on "R=[" matched "TR=["), fixed in work/d29/gen_raw30.py; tf-site/.git had lost its refs/ folder, recreated (repo was in sync with origin).
- **QC:** dup domains 0, dup company numbers 0, dup phones 1 (same pre-existing pair); checked firms with phone or website 97%; confidence ≥0.5 98%; spot check 10/10; desktop + mobile screenshots checked. 1,098 checked firms, 12,638 in radius, 11,974 in Not in business.

- 08:02 GMT: Issue 05: +33 web-checked firms across all live counties; latest Companies House changes
- **Issue 05 (4 Nov 2026, 07:20–08:10 GMT):** +33 web-checked firms from Companies House leads (17 prepared on 3 Nov, whose run never finished, plus 16 today), Hampshire, Dorset, Somerset, Berkshire, Bristol, Devon. Own websites found by name-domain lookup and checked on home/contact pages (company number or local postcode on site). 17 off-scope dropped (mostly domestic/office cleaners, plus a treehouse builder). Companies House changes 3–4 Nov added (68 rows kept). Lead crawl now ~2,600 of ~3,400 domains; rest carries over.
- **QC:** dup domains 0, dup company numbers 0, dup phones 1 (same known pair); checked firms with phone or website 97%; confidence ≥0.5 98%; spot check 10/10; desktop + mobile screenshots checked (only a missing favicon 404). 1,131 checked firms, 12,637 in radius, 12,008 in Not in business.

- 14:22 GMT: Issue 06: add West Sussex and Surrey (Companies House active-only discovery + 54 web-checked firms)

- 14:46 GMT: Issue 06 b2: +62 web-checked Surrey firms from Companies House active leads (own sites)

- **Issue 06 (10 Nov 2026, 13:10–14:45 GMT): West Sussex + Surrey added (Pete).** Companies House SIC discovery (43120 43999 81300 42110 43110 02200, 3 pages) over 38 West Sussex and 53 Surrey postcode districts (checked against postcodes.io outcodes), **active companies only** (`ch_discover.py --status active`); county by the registered office's actual council area (postcodes.io admin_county), not postcode area. **Pete rule 10 Nov 2026: no new dissolved/closed CH records are added anywhere** (build_issue.py skips any dissolved CH row not already in the master); existing Not in business records untouched (12,008, unchanged). New raw postcode rules in `county_of` for Surrey/West Sussex districts; an explicit `county` on a raw record wins for these two. County pages with no checked firm now fall back to that county's own best lead for the cover, never another county's.
  - West Sussex: 1,506 listed (43 web-checked), 0 not in business. Cover star Above All Landscaping (Chichester, PO20).
  - Surrey: 2,355 listed (74 web-checked), 0 not in business. Cover star on page: AKS Groundwork (Godalming, GU8) (meta: 1ST Advanced Landscapes, Hindhead; same score 19, both Surrey).
  - Enrichment: 116 firms (raw_2026-11-10a.py 54, raw_2026-11-10b.py 62) via name→domain DNS lookup + own home/contact pages (robots.txt respected, ~4 s/page); accepted only if the site shows the CH company number (46) or a postcode in the registered-office district (70). 110 with phone. Rejected: redirects to other domains, parked sites, placeholder phone numbers, demolition/out-of-scope names. Spot check 10/10.
  - Spill-over active CH leads (geo Hampshire/Berkshire) also added: Hampshire 4,597→4,618, Berkshire 621→632.
  - QC: dup domains 0, dup company numbers 0, dup phones 1 (known Gaia/Henley shared office). Checked firms 1,247: phone/website 98%, confidence ≥0.5 98%. In range 16,529. Largest file 17.6 MB (hampshire.json). Live 200: home, archive, issue 2026-11-10, all county pages incl. west-sussex + surrey. Counties dropdown lists both. No JS errors (one transient 404 on first load, not reproducible).
  - Commits: e88f4f6 (Issue 06), ebee30a (b2).
  - Note: new counties have no Checkatrade/TrustATrader ratings yet, so the "Top rated" cover line shows "–" and covers score 19; they strengthen as review checks are added.

- 15:32 GMT: Issue 06 fixes: singular/plural count labels, honest Top scored fallback where nothing is rated, deterministic cover-star tie-break

- **Issue 06 fixes (10 Nov 2026, ~15:50 GMT, commit c443028, Pete approved):** (1) singular/plural on every count label: cover lines ("1 checked driveway firm", "N checked firm(s)", "Companies House lead(s)"), review counts on cards ("1 Google review"), the cover bubble unit (TRADE/TRADES), archive header ("6 issues so far · N firms") and archive cards; existing helpers already handled business(es)/county(ies)/firm is/are. (2) "Top rated" when a county has no rated firm: shows "Top scored · no ratings yet" / "19/100 Chichester" / "<firm> · score, not a rating" from the build's top-scoring checked firm (same .cl/.k/.t/em classes; no invented ratings); the block is omitted if there is no checked firm. (3) One cover-star rule `hero_key()` in build_issue.py for home, county and issue covers and the Top scored fallback: score, then verification signals (distinct source types + review platform + Companies House), then phone and website, then phone or website, then name A–Z, then id; pages only render meta.hero. Effect: Bristol cover moved from Arb Tree Works to Green Planet Tree Services (both 23; Green Planet has Checkatrade + Which?). Surrey: 1ST Advanced Landscapes (page and JSON agree; the earlier AKS Groundwork view was GitHub Pages serving the first batch). Screenshots desktop+mobile West Sussex, Surrey, Devon checked; no JS errors.

- 16:16 GMT: Issue 06 b3: add Gloucestershire and Oxfordshire (active Companies House firms only) + 74 web-checked firms; long county names fit the cover column

- **Issue 06 b3 (10 Nov 2026, 16:15 GMT, commit e32b648): Gloucestershire + Oxfordshire added (Pete).** Active-only CH SIC discovery (same 6 SICs, 3 pages): Gloucestershire GL1–GL20, GL50–GL56 plus South Gloucestershire BS15 BS16 BS30 BS32 BS34–BS37 (ceremonial county: `DIST2CTY` maps south-gloucestershire → gloucestershire); Oxfordshire OX1–OX5, OX7, OX9–OX18, OX20, OX25–OX29, OX33, OX39, OX44, OX49, RG8, RG9, SN7 (districts checked in `work/go_outcodes.json`). Raw postcode rules: GL → gloucestershire; OX/RG9/SN7 → oxfordshire (one GL12 firm moved from Dorset). No new closed/dissolved records (Not in business still 12,008).
  - Gloucestershire: 1,232 listed, 47 web-checked, 0 not in business. Cover star Anderson Norman Landscapes (Stonehouse, GL10).
  - Oxfordshire: 919 listed, 28 web-checked, 0 not in business. Cover star 007 Groundworks Solutions (Bicester, OX25).
  - Enrichment: raw_2026-11-10c.py (46 Glos: 22 company number on site, 24 district postcode) and raw_2026-11-10d.py (28 Oxon: 13 / 15); 73 with phone. Spot check 10/10. Scripts `work/go_enrich.py`, `work/go_make_raw.py`. Greentrees Surfacing hand-fixed to surfacing (name contains "trees").
  - Spill-over active leads: Wiltshire 1,545→1,551, Berkshire 632→642; Bristol 507→505 (2 leads superseded by checked South Glos firms, kept in master).
  - Page fix: long county names (Gloucestershire, Isle of Wight) are fitted to the cover column (`tfFitCounty`, shrinks only when the line would overflow; others unchanged).
  - QC: dup domains 0 / CH 0 / phones 1 (known). Checked 1,321: phone/website 98%, confidence ≥0.5 98%. In range 18,693; master 34,324 records. Live 200 on home, archive, issue, all 12 county pages; dropdown lists both; desktop+mobile screenshots (Gloucestershire, Oxfordshire, Isle of Wight, West Sussex) checked; no JS errors except the missing favicon.ico.

- 12:37 GMT: Issue 07: add Cornwall, Buckinghamshire and East Sussex (active Companies House firms only) + 19 web-checked Cornwall firms; cover and bubble fit long names

- 13:07 GMT: Issue 07 update: add Greater London (12,471 active Companies House firms, split by postcode area) + 34 East Sussex and 33 Buckinghamshire web-checked firms; faster XLSX; cleaner London towns

- 13:38 GMT: Issue 07 b2: +35 web-checked Greater London firms (own site shows company number or registered-office postcode district; 5 hand-rejected)

- 13:55 GMT: Issue 07 b3: +8 web-checked Cornwall firms (wider trade-name net, hand-checked; 5 rejected)

- 14:07 GMT: Issue 07 b4: +5 web-checked Buckinghamshire firms (wider trade-name net, hand-checked; 9 rejected)

- 14:12 GMT: Issue 07 b5: Greater London central districts (EC/WC/W1/SW1 sub-districts, N1C, NW1W, E1W) discovered; London now 14,288 active firms

- 14:17 GMT: Issue 07 b6: maps open fitted to every plotted firm (home/issue: all 16 live counties; county pages: their own firms), outlier-safe bounds computed at build; clusters unchanged

- 14:46 GMT: Issue 07 b7: add Monmouthshire, Newport, Cardiff and Vale of Glamorgan (active Companies House firms only; 840 listed); maps include them

- 15:01 GMT: Issue 07 b8: +7 web-checked Cardiff firms (2 hand-rejected)

- 15:11 GMT: Issue 07 b9: +5 web-checked Newport and +2 Monmouthshire firms (2 hand-rejected)

- 15:16 GMT: Issue 07 b10: +5 web-checked Vale of Glamorgan firms; final QC
