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

### 12 Nov 2026 summary (Issue 07, commits 2d3716e → 63a4b92)
- Greater London: 14,288 active Companies House firms, master split into greater-london--{central,east,north,south,west}.json (largest 6.1 MB). Central was only 5 KB because the first pass searched "EC1", "W1", "SW1" and so on, and Companies House's address search matches whole tokens, so suffixed districts (EC1A, W1G, SW1P…) returned nothing. Fixed with a targeted active-only pass over 60 central sub-districts (+1,761 firms; central file now about 3 MB). 35 web-checked London firms (5 hand-rejected).
- Enrichment: +8 Cornwall, +38 Bucks, +34 East Sussex, +35 London, +7 Cardiff, +5 Newport, +2 Monmouthshire, +5 Vale of Glamorgan (each one hand-checked; rejects are in work/go_reject.json).
- Wales: Monmouthshire, Newport, Cardiff and Vale of Glamorgan added (31 NP/CF districts, active only, county from the postcodes.io admin_district). 189 "Companies House Default Address" (CF14 8LH) companies were left out because they don't geocode and aren't really based there.
- Maps: the initial view now fits every plotted firm (meta.bounds, worked out at build time per page; per-county 0.5–99.5 percentile box +15% margin, so outlier geocodes are ignored). County pages fit their own area, and the radius circle is used only as a fallback.
- Speed: building the XLSX was quadratic (ws.max_row inside the loop), so a full build now takes about 2 min instead of more than 15. go_enrich DNS-over-HTTPS has retries and a shared cache (work/dns_cache.json). Street-like or postal-county "towns" fall back to the borough.

- 10:24 GMT: Issue 08: county cover lines use county figures; cover stars must be verified inside their own area (all 20 pass; precise site/registered postcode check)

- 10:39 GMT: Issue 08 b2: add Herefordshire, Worcestershire, Warwickshire and Northamptonshire (3,435 active Companies House firms); maps and Counties menu include them

- 10:54 GMT: Issue 08 b3: +6 web-checked Herefordshire firms (5 hand-rejected; 1 moved to Worcestershire)

- 11:19 GMT: Issue 08 b4: +14 web-checked Worcestershire firms (3 hand-rejected); Garden Inspiration kept in Herefordshire (site postcode WR13 6QW is Colwall)

### 13 Nov 2026: next four closest areas (Pete approved)
Distance from Poole (50.715, -1.9872) to each area's centroid. Source: ONS Counties and Unitary Authorities (Dec 2024) boundary LAT/LONG; ceremonial counties use the area-weighted mean of their parts. Candidates were areas not on the site yet (paused English counties plus Welsh principal areas).
1. Torfaen (Wales): 82.1 mi
2. Caerphilly (Wales): 83.2 mi
3. Rhondda Cynon Taf (Wales): 88.0 mi
4. Blaenau Gwent (Wales): 88.5 mi
Next after those: Bridgend 91.6, Merthyr Tydfil 93.0, Neath Port Talbot 99.6, Hertfordshire 105.7, Swansea 107.7, Bedfordshire 114.4, Kent 122.3, West Midlands 122.9 (full list in work/next_areas_distances.json).

- 11:43 GMT: Issue 08: Warwickshire first 24 web-checked firms; Cardiff/Newport/Vale/Monmouthshire completeness pass (+CF14 uncapped, forestry/plant/drainage SICs)

- 12:09 GMT: Issue 08: Torfaen, Caerphilly, Rhondda Cynon Taf, Blaenau Gwent added (active only); Bristol completeness pass (+37); Cardiff/Newport web-check

- 12:15 GMT: Issue 08: Northamptonshire first 15 web-checked firms; Torfaen first 4; retried timed-out Welsh/BS16 searches

- 12:29 GMT: Issue 08: first web-checked Caerphilly (1), Rhondda Cynon Taf (8), Blaenau Gwent (3) firms

- 12:31 GMT: Issue 08: first web-checked Caerphilly (1), Rhondda Cynon Taf (8), Blaenau Gwent (3) firms

## 13 Nov 2026, 12:50 GMT: Issue 08 wrap-up (Midlands four, Welsh/Bristol completeness audit, next four Welsh areas)
Commits today on four2d/trade-finder: cbb37de (county cover figures + in-area cover stars), 8e80cac (Midlands four discovery), 5ad2b3c (+6 Herefordshire checked), 5523bda (+14 Worcestershire), c75a49f (+24 Warwickshire; Welsh completeness pass), a4c0ac1 (Torfaen, Caerphilly, RCT, Blaenau Gwent added; Bristol pass), 77da684 (+15 Northamptonshire, +4 Torfaen, retried timed-out searches), c4ddfde (+1 Caerphilly, +8 RCT, +3 Blaenau Gwent).
Next four picked by centroid distance from Poole (ONS county/UA centroids, areas not yet on the site): Torfaen 82.1 mi, Caerphilly 83.2 mi, Rhondda Cynon Taf 88.0 mi, Blaenau Gwent 88.5 mi.

Completeness audit (listed trading before -> after; web-checked before -> after):
- Cardiff 322 -> 386 (+64); checked 7 -> 8. Cause: the CF14 searches hit the 3-page (60-result) cap because CF14 holds the Companies House default address (CF14 8LH), so the capped pages were filled with default-address companies. CF14 43999/81300 rerun to 15 pages gave +43. SICs 77320 plant hire with operator, 02100 forestry and 42210 utility works were never searched: +21. 215 default-address companies were found (no real office); the trade-named ones had 43 candidate websites checked, and none showed a company number plus a trading postcode in the area, so none were added.
- Newport 192 -> 210 (+18); checked 5 -> 6. Cause: missing SICs (77320 +16, 42210 +2). The NP19/NP20/NP44 43999 cap reruns found nothing new.
- Vale of Glamorgan 147 -> 161 (+14); checked 5. Cause: missing SICs (02100 forestry +6, 77320 +7, 42210 +1). The CF62 forestry search that timed out was retried (+1 of the 6).
- Monmouthshire 179 -> 203 (+24); checked 2. Cause: missing SICs (77320 +15, 02100 +9). The NP16 cap rerun found nothing new.
- Bristol 505 -> 542 (+37); checked 58 -> 60. Cause: missing SICs (77320 +21, 02100 +12, 42110/42210 +2) plus the BS7 43999 page cap (+1); BS16 timeouts retried. 37 Bristol-postcode firms are filed under Somerset (26) and Gloucestershire (11) because their registered offices geocode to North Somerset/South Glos (admin boundary, correct).
All 28 cover stars verified inside their own area (work/hero_audit.json). Site: 41,442 listed trading (1,553 web-checked, 39,889 CH-only leads), 12,008 not in business (unchanged).
| Area | Listed (trading) | Web-checked | Not in business | Cover star |
|---|---:|---:|---:|---|
| Dorset | 1,832 | 192 | 1,841 | D.S. Waker Driveways & Patios (BH17, registered office) |
| Hampshire | 4,616 | 344 | 4,611 | Arbor Venture Tree Care (SO41, registered office) |
| Wiltshire | 1,551 | 135 | 1,326 | Acer Tree Surgeons (BA13, registered office) |
| Somerset | 1,937 | 142 | 1,607 | Becks Tree and Landscape (BA2, registered office) |
| Devon | 1,449 | 157 | 1,254 | A2B Fencing Solutions (PL6, registered office) |
| Isle of Wight | 146 | 22 | 110 | Dixcey Landscapes (PO38, registered office) |
| Bristol | 542 | 60 | 553 | Green Planet Tree Services (BS13, registered office) |
| Berkshire | 688 | 79 | 706 | Evolution Tree Surgery (RG19, registered office) |
| West Sussex | 1,508 | 44 | 0 | Above All Landscaping (PO20, site postcode PO20 8JQ) |
| Gloucestershire | 1,274 | 47 | 0 | Anderson Norman Landscapes (GL10, registered office) |
| Surrey | 2,380 | 74 | 0 | 1ST Advanced Landscapes (GU26, site postcode GU26 6SL) |
| Oxfordshire | 920 | 28 | 0 | 007 Groundworks Solutions (OX25, site postcode OX25 1AG) |
| Cornwall | 611 | 27 | 0 | Alpine Decking (TR5, site postcode TR5 0XQ) |
| Buckinghamshire | 1,429 | 37 | 0 | Alderbourne Landscapes (HP15, site postcode HP15 7JJ) |
| Greater London | 14,288 | 35 | 0 | 365 Gardening (E4, site postcode E4 9QR) |
| East Sussex | 1,176 | 34 | 0 | A.L.M Tree Care (TN39, registered office) |
| Monmouthshire | 203 | 2 | 0 | Gardenology Group UK (NP7, site postcode NP7 6PE) |
| Newport | 210 | 6 | 0 | Acw Draincare (NP20, site postcode NP20 3BX) |
| Cardiff | 386 | 8 | 0 | Caerdydd Groundworks (CF24, site postcode CF24 5PJ) |
| Vale of Glamorgan | 161 | 5 | 0 | Ceejay Landscapes (CF35, site postcode CF35 5DR) |
| Herefordshire | 286 | 6 | 0 | Fix My Garden (HR8, registered office) |
| Worcestershire | 966 | 14 | 0 | Arc Ground Care (DY10, site postcode DY10 4HD) |
| Warwickshire | 860 | 24 | 0 | Advance Tree Care (CV10, site postcode CV10 0TB) |
| Northamptonshire | 1,324 | 15 | 0 | AD Landscapes & Maintenance (NN12, site postcode NN12 8EU) |
| Torfaen | 124 | 4 | 0 | DT Landscapes & Tree Services (NP4, registered office) |
| Caerphilly | 219 | 1 | 0 | Big & Small Groundcare (CF83, site postcode CF83 8HL) |
| Rhondda Cynon Taf | 297 | 8 | 0 | C2 Groundworks (CF39, site postcode CF39 8ER) |
| Blaenau Gwent | 59 | 3 | 0 | Arbor Care South Wales (NP23, registered office) |
| **Total (28 areas)** | 41,442 | 1,553 | 12,008 | |


- 12:38 GMT: Issue 08 wrap-up: run log (completeness audit causes, next four distances, final figures)

## 13 Nov 2026, 15:50 GMT: Issue 09 started: next four closest areas (Pete approved)
Measured as before: straight-line distance from Poole to each area's official centre point (ONS county/unitary-authority centroids for Welsh principal areas, ceremonial-county centroids for England), skipping the 28 live areas (work/next_areas_distances.json):
- Bridgend: 91.6 mi
- Merthyr Tydfil: 93.0 mi
- Neath Port Talbot: 99.6 mi
- Hertfordshire: 105.7 mi
(Next after these: Swansea 107.7, Bedfordshire 114.4.)
Discovery: active only; SIC 43120 43999 81300 42110 43110 02100 02200 77320 42210; up to 15 pages (300 results) per search; any search that fills its last page or times out is rerun. CF14 8LH default-address companies are excluded because they have no real office to geocode.
Issue 09 is a same-date edition (issues/2026-11-13-b/), built with the new --edition flag.

- 15:56 GMT: Issue 09: Bridgend, Merthyr Tydfil, Neath Port Talbot and Hertfordshire added (active only, full SIC set); same-date edition support; publish URL check covers all areas

- 16:09 GMT: Issue 09 b2: Hertfordshire full discovery (3,013 active); first web-checked Bridgend, Merthyr Tydfil, Neath Port Talbot firms
