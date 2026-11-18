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

- 16:20 GMT: Issue 09 b3: first 9 web-checked Hertfordshire firms (3 hand-rejected)

- 17:08 GMT: Issue 09 b4: +5 web-checked Hertfordshire firms (3 hand-rejected)

## 13 Nov 2026, 17:15 GMT: Issue 09 finished (issues/2026-11-13-b/)
Areas added, measured from Poole to each area's official centre point: Bridgend 91.6 mi, Merthyr Tydfil 93.0 mi, Neath Port Talbot 99.6 mi, Hertfordshire 105.7 mi.
Discovery: active only, 9 SICs (incl. 77320 plant hire, 02100/02200 forestry, 42210 utility works), 15-page limit. The deepest search reached page 8, so nothing was capped. 9 searches that timed out were rerun (the LU6 43999 page-3 retry also succeeded). No CF14 8LH default-address companies are in any county file.
Web-checks (each was a hand-check of what the site checker accepted): Bridgend 2 (all 24 trade-named leads probed), Merthyr Tydfil 3 (30), Neath Port Talbot 2 (49), Hertfordshire 14 from 2 batches of leads (450 of the trade-named leads probed; 6 hand-rejected: out-of-area sites, a skip hire firm, builders and a consultancy).
Commits: e7bf339, 547d2d4, c6cc569, 089810a, plus this run-log commit.
Code: build_issue.py --edition b (second issue on the same date; archive links by issue_key); publish.sh TF_ISSUE=<key> and a URL check of all 32 areas; go_enrich.py OFFSET for batched passes.
All 32 cover stars verified in-area (work/hero_audit.json). Desktop and mobile QC screenshots are clean (no overflow).
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
| Surrey | 2,379 | 74 | 0 | 1ST Advanced Landscapes (GU26, site postcode GU26 6SL) |
| Oxfordshire | 920 | 28 | 0 | 007 Groundworks Solutions (OX25, site postcode OX25 1AG) |
| Cornwall | 611 | 27 | 0 | Alpine Decking (TR5, site postcode TR5 0XQ) |
| Buckinghamshire | 1,447 | 37 | 0 | Alderbourne Landscapes (HP15, site postcode HP15 7JJ) |
| Greater London | 14,341 | 35 | 0 | 365 Gardening (E4, site postcode E4 9QR) |
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
| Caerphilly | 221 | 1 | 0 | Big & Small Groundcare (CF83, site postcode CF83 8HL) |
| Rhondda Cynon Taf | 298 | 8 | 0 | C2 Groundworks (CF39, site postcode CF39 8ER) |
| Blaenau Gwent | 59 | 3 | 0 | Arbor Care South Wales (NP23, registered office) |
| Bridgend | 179 | 2 | 0 | Archstone Masonry (CF36, site postcode CF36 3LN) |
| Merthyr Tydfil | 81 | 3 | 0 | Construction Force (CF48, site postcode CF48 4DR) |
| Neath Port Talbot | 190 | 2 | 0 | A Pro Tree & Landscaping (SA11, registered office) |
| Hertfordshire | 3,013 | 14 | 0 | Elliotts Drainage (SG2, registered office) |
| **Total (32 areas)** | 44,978 | 1,574 | 12,008 | |


Site: 44,978 listed trading (1,574 web-checked, 43,404 CH-only leads); 12,008 not in business (unchanged).

- 17:10 GMT: Issue 09 wrap-up: run log (distances, web-check results, final figures)

## 17 Nov 2026 — page speed (Pete: "go")

Baseline (live f4b3cad, headless Chrome, throttled 4G = 150 ms RTT / 1.6 Mbps down / 750 kbps up, cold cache, median of 3; tools/perf_measure.py; "map usable" = tiles + bubbles/pins drawn, no spinner, map scrolled into view / "Show map" pressed on mobile):

| Page | Desktop bytes | Desktop map usable | Mobile bytes | Mobile map usable |
|---|---|---|---|---|
| Home | 1,769,418 | 9.96 s | 1,620,381 | 9.27 s |
| Dorset | 578,172 | 3.31 s | 319,530 | 2.33 s |
| Greater London | 1,121,916 | 6.60 s | 642,731 | 4.03 s |

Home: data/pins.json alone is 1,292,390 bytes gzipped (44k pins). The search index (data/index.json) was already loaded only when search/filters are used.

Approach: tools/mapdata.py runs the page's own Leaflet 1.9.4 + markercluster 1.5.3 (vendored in tools/vendor, same options) in headless Chrome at build time and saves the bubble tree for zooms 0–10 per page and per trade area (data/map/<all|area>.json, counties/<slug>/data/map/). The page rebuilds that tree inside a real MarkerClusterGroup, so the bubbles, sizes, glow, animations and click-to-split are markercluster's own. Past zoom 10 real pins load per county (Greater London per part) from data/pins/<unit>.json (lean rows, 5-dp coordinates) and cluster live exactly as before. tools/mapwrite.py writes all of this; build_issue.py calls it after the data files. data/pins.json is still written for older issue pages.

Checks before publishing: pixel compare old (f4b3cad) vs new on 6 pages × desktop/mobile × 12 map states (fit, zoom 7–15, back to 9): 132 screenshots, all identical except a few 1-pixel shifts of single bubbles/pins (5-dp rounding) and OSM tile re-renders. Same clicks on old and new (6 bubble clicks across the zoom-10/11 handoff, pin popup, zoom out, search, clear, area chip, Show on map): same zoom, centre, popup and highlight.

- 11:07 GMT: Page speed 1/2: lean per-county pin files and prebuilt map bubbles (data only; pages unchanged)

- 11:09 GMT: Page speed 2/2: home, issue and county pages open with prebuilt bubbles; pins load per county past zoom 10

### After (live b9187e0, measured 11:53–12:03 GMT, same tool and settings as the baseline: throttled 4G, cold cache, median of 3)

| Page | Device | Bytes before | Bytes after | Map usable before | Map usable after |
|---|---|---:|---:|---:|---:|
| Home | desktop | 1,769,418 | 504,510 | 9.96 s | 2.18 s |
| Home | mobile | 1,620,381 | 355,334 | 9.27 s | 2.13 s |
| Dorset | desktop | 578,172 | 535,721 | 3.31 s | 1.98 s |
| Dorset | mobile | 319,530 | 277,051 | 2.33 s | 1.44 s |
| Greater London | desktop | 1,121,916 | 793,414 | 6.60 s | 2.51 s |
| Greater London | mobile | 642,731 | 297,718 | 4.03 s | 2.10 s |

- Home: the map's own data is now data/map/all.json, 21.6 KB gzipped (was data/pins.json, 1,292 KB). Most remaining bytes are OpenStreetMap tiles and Leaflet, which did not change.
- Dorset: few bytes saved (its pins were only 48 KB). The gain is time: no live clustering of all pins at load.
- Search index: still loads only on first use of search. It now starts when the search box is focused, with the "Loading search index…" spinner.
- Pin data: per-county files, 3.51 MB raw / 1.08 MB gz in total (was 5.18 MB / 1.29 MB in one file). They load only past zoom 10, for the counties in view.
- Trade-offs: (1) bubbles or pins can move 1 pixel at rare spots, from rounding coordinates to 5 decimals (about 1 m). (2) Past zoom 10, a pan into a new county shows the spinner while that county's pins load. (3) Single pins at zoom 10 and below get their name tooltip and popup once their county file loads (a fraction of a second on hover or click). (4) A search, or another filter, loads every county's pins, the same amount the old page loaded. (5) With an area filter on, the highlighted firm outside that area shows as its own pin at bubble zooms. The old map folded it into a nearby bubble. A refinement is parked locally (work/speed/page_curx_wip.html), not published.

- 12:03 GMT: Page speed: run log with before/after measurements

### 17 Nov 2026 — highlighted firm under an area filter (trade-off 5; Pete: "yes please")
- Old map (f4b3cad): when an area filter hides the highlighted firm, it stays in the clustered set, so at the bubble zooms it folds into a nearby bubble (that bubble's count goes up by 1).
- Fix: in that one case the page clusters live pins (filtered firms plus the highlighted one) with the same markercluster code, as the old page did. This loads every county's pin file (1.08 MB gz), the same as a search does. The separate-pin overlay from b9187e0 is removed. Page loads and all other paths are unchanged. The parked draft (work/speed/page_curx_wip.html) was replaced by this.
- Tested against f4b3cad with the same clicks (6 bubble clicks across the zoom 10/11 handoff, pin popup, zoom out, search, clear, area chip, then zoom in 1/2/4 and out 3/5 with the area on, Show on map) on home, Greater London and Dorset, desktop and mobile: 6 runs, 17–19 steps each. Zoom, centre, bubble/pin counts, popup and highlight were the same at every step. The only exception was the known home-desktop out3 step: 57 vs 55 pins in the DOM, all off-screen; its screenshot is identical. Screenshots matched except low-level OSM tile seams/re-renders (max channel difference ≤ 59 of 255). One GL desktop pair was caught mid-tile-load; its markers were identical. Home desktop "area" step: 852 px different before, 0 px now.

- 13:32 GMT: Map: highlighted firm folds into nearby bubbles under an area filter, as before
- Live after ab940e2 (same tool/settings, median of 3; bytes / map usable): Home desktop 504,090 / 2.12 s; Home mobile 355,072 / 2.15 s; Dorset desktop 535,568 / 1.93 s; Dorset mobile 276,680 / 1.45 s; Greater London desktop 776,770 / 2.45 s; Greater London mobile 297,371 / 2.11 s. Same as ec0ca24's figures within run-to-run noise, so no regression. All 36 live URL checks returned 200.

- 13:45 GMT: Run log: area-filter highlight fix tested and measured

## 17 Nov 2026, 14:15 GMT: Issue 10 started: next four closest areas (Pete: "Go")
Measured as before: straight-line distance from Poole (50.715, -1.9872) to each area's official centre point (ONS principal-area centroid for Swansea; ceremonial-county centroids for England), skipping the 32 live areas (work/next_areas_distances.json):
- Swansea: 107.7 mi
- Bedfordshire: 114.4 mi
- Kent: 122.3 mi
- West Midlands: 122.9 mi
(Next after these: Carmarthenshire 126.0, Powys 128.9.)
Setup: counties.json (Swansea added; all four in_progress), county_of rules, DIST2CTY (Medway → Kent; Bedford/Central Bedfordshire/Luton → Bedfordshire; the seven met districts → West Midlands), NEWCTY, and publish.sh URL check for 36 areas.
Discovery: active only; SIC 43120 43999 81300 42110 43110 02100 02200 77320 42210; up to 30 pages per search (any search that fills its last page or times out is rerun); every postcode district of each area (work/log_10_*.txt). CF14 8LH default-address companies are excluded (no geocode).
- 14:47 GMT: discovery done for all four (1,248 searches with results; deepest page 12 of 30 (DA1 43999), so nothing capped; 0 CF14 8LH rows). 29 searches that errored are being rerun.
- 14:55 GMT: build 10a: Swansea 267 listed (4 web-checked), Bedfordshire 1,485, Kent 4,458, West Midlands 4,063. The new border searches also found active firms registered in live areas: Greater London +122, Buckinghamshire +52, Warwickshire +16, Surrey +11, Worcestershire +8, Somerset +1. All 36 cover stars are in-area (work/hero_audit.json). Duplicate phone +447561109141 (Gaia Landscapes and Henley Gardeners, both SP1) dates from Issue 02 and is still open.

- 14:51 GMT: Issue 10: Swansea, Bedfordshire, Kent and West Midlands added (active only, full SIC set); first Swansea web-checks
- 16:05 GMT: build 10b: the 29 retried searches all succeeded (+248 rows). Bedfordshire web-check: 285 trade-named leads, 277 own-site domains probed, 28 accepted by the checker, 26 kept after hand-check (dropped Midlands Steel Decking: structural steel floor decking; Forestry Fuels: firewood supply). Bedfordshire 1,520 listed (26 checked), cover star Absolute Paving (LU1, registered office, in-area). Kent 4,486, West Midlands 4,065 (web-checks running).

- 16:01 GMT: Issue 10 b2: Bedfordshire first 26 web-checked firms; retried searches
- 16:15 GMT: build 10c: Kent web-check batch 1 (450 trade-named leads; 238 with a live own-site domain; the first ~130 probed domains used): 17 accepted, all kept after hand-check.

- 16:07 GMT: Issue 10 b3: Kent first 17 web-checked firms
- 16:22 GMT: build 10d: West Midlands web-check batch 1 (450 trade-named leads; 197 with a live own-site domain; first ~240 probed domains used): 19 accepted, 17 kept (dropped Elite Playgrounds: playground equipment; Cotswold Trees: online tree supplier).

- 16:13 GMT: Issue 10 b4: West Midlands first 17 web-checked firms
- 16:14 GMT: build 10e: Kent web-check batch 2 (all 391 probed domains): 42 more accepted, 38 kept (dropped Surface Renew: interior worktop/bath repair; Trees4Good: tree-planting investment; KTM Garden & Grounds: works in North Wales only; Indipave: paving-stone supplier). Kent now has 55 checked firms.

- 16:20 GMT: Issue 10 b5: Kent +38 web-checked firms (55 in all)
- 16:21 GMT: build 10f: West Midlands web-check batch 2 (all 393 probed domains): 12 more accepted, 11 kept (dropped The Balcony Gardener: small-space garden designer working in London). West Midlands now has 28 checked firms.

- 16:26 GMT: Issue 10 b6: West Midlands +11 web-checked firms (28 in all)

## 17 Nov 2026, 16:30 GMT: Issue 10 wrap-up
Distances from Poole (centroid): Swansea 107.7 mi, Bedfordshire 114.4 mi, Kent 122.3 mi, West Midlands 122.9 mi. Next by distance: Carmarthenshire 126.0 mi, Powys 128.9 mi.
Discovery: active only, full SIC set, 1,262 searches with results, deepest page 12 of 30 (none capped), 29 retries all succeeded, 0 CF14 8LH default-address rows.
Web-checks: all leads probed in Swansea (52) and the first 450 by rank in Kent (391 domains) and West Midlands (393). Hand-rejected 11 out-of-scope firms (added to go_reject.json).
QC (16:28 GMT, local build = live 5e3e7f2): 36/36 cover stars inside their own area (work/hero_audit.json). 12 desktop+mobile shots (home, issue, 4 new areas) in work/qc10: no overflow, no JS errors, Counties menu lists all 4 new areas, bubbles total the listed count (55,531 home; 267/1,520/4,486/4,065 per area).
Page speed (throttled 4G, cold, median of 3; work/perf_after_i10.json): home desktop 2.33 s map usable (was 2.12 s), home mobile 2.05 s, Dorset 1.96/1.47 s, Greater London 2.52/2.11 s, Kent 1.33/1.48 s. Home bubbles file 24.3 KB gz (was 21.6). No meaningful regression.
Border additions to live areas from the new searches: Greater London +122, Buckinghamshire +52, Warwickshire +16, Surrey +11, Worcestershire +8, Somerset +1 (all active, in-area).
Commits: 146f7ae, 5d42dd0, 6937bfa, bf53785, 4336ea4, 5e3e7f2.

| # | Area | Listed | Checked | Not in business | Cover star (in area) |
|---|---|---:|---:|---:|---|
| 1 | Dorset | 1,832 | 192 | 1,840 | D.S. Waker Driveways & Patios (BH17, yes) |
| 2 | Hampshire | 4,616 | 344 | 4,611 | Arbor Venture Tree Care (SO41, yes) |
| 3 | Wiltshire | 1,551 | 135 | 1,326 | Acer Tree Surgeons (BA13, yes) |
| 4 | Somerset | 1,938 | 142 | 1,607 | Becks Tree and Landscape (BA2, yes) |
| 5 | Devon | 1,449 | 157 | 1,254 | A2B Fencing Solutions (PL6, yes) |
| 6 | Isle of Wight | 146 | 22 | 110 | Dixcey Landscapes (PO38, yes) |
| 7 | Bristol | 542 | 60 | 553 | Green Planet Tree Services (BS13, yes) |
| 8 | Berkshire | 688 | 79 | 706 | Evolution Tree Surgery (RG19, yes) |
| 9 | West Sussex | 1,508 | 44 | 0 | Above All Landscaping (PO20, yes) |
| 10 | Gloucestershire | 1,274 | 47 | 0 | Anderson Norman Landscapes (GL10, yes) |
| 11 | Surrey | 2,390 | 74 | 0 | 1ST Advanced Landscapes (GU26, yes) |
| 12 | Oxfordshire | 920 | 28 | 0 | 007 Groundworks Solutions (OX25, yes) |
| 13 | Cornwall | 611 | 27 | 0 | Alpine Decking (TR5, yes) |
| 14 | Buckinghamshire | 1,504 | 37 | 0 | Alderbourne Landscapes (HP15, yes) |
| 15 | Greater London | 14,463 | 35 | 0 | 365 Gardening (E4, yes) |
| 16 | East Sussex | 1,176 | 34 | 0 | A.L.M Tree Care (TN39, yes) |
| 17 | Monmouthshire | 203 | 2 | 0 | Gardenology Group UK (NP7, yes) |
| 18 | Newport | 210 | 6 | 0 | Acw Draincare (NP20, yes) |
| 19 | Cardiff | 386 | 8 | 0 | Caerdydd Groundworks (CF24, yes) |
| 20 | Vale of Glamorgan | 161 | 5 | 0 | Ceejay Landscapes (CF35, yes) |
| 21 | Herefordshire | 286 | 6 | 0 | Fix My Garden (HR8, yes) |
| 22 | Worcestershire | 974 | 14 | 0 | Arc Ground Care (DY10, yes) |
| 23 | Warwickshire | 876 | 24 | 0 | Advance Tree Care (CV10, yes) |
| 24 | Northamptonshire | 1,324 | 15 | 0 | AD Landscapes & Maintenance (NN12, yes) |
| 25 | Torfaen | 124 | 4 | 0 | DT Landscapes & Tree Services (NP4, yes) |
| 26 | Caerphilly | 221 | 1 | 0 | Big & Small Groundcare (CF83, yes) |
| 27 | Rhondda Cynon Taf | 298 | 8 | 0 | C2 Groundworks (CF39, yes) |
| 28 | Blaenau Gwent | 59 | 3 | 0 | Arbor Care South Wales (NP23, yes) |
| 29 | Bridgend | 179 | 2 | 0 | Archstone Masonry (CF36, yes) |
| 30 | Merthyr Tydfil | 81 | 3 | 0 | Construction Force (CF48, yes) |
| 31 | Neath Port Talbot | 190 | 2 | 0 | A Pro Tree & Landscaping (SA11, yes) |
| 32 | Hertfordshire | 3,013 | 14 | 0 | Elliotts Drainage (SG2, yes) |
| 33 | Swansea | 267 | 4 | 0 | Algar Groundworks (SA4, yes) |
| 34 | Bedfordshire | 1,520 | 26 | 0 | Absolute Paving (LU1, yes) |
| 35 | Kent | 4,486 | 55 | 0 | 1ST County Fencing (DA1, yes) |
| 36 | West Midlands | 4,065 | 28 | 1 | A K Lawnscapes (B90, yes) |
| | **Total (36)** | **55,531** | **1,687** | **12,008** | |


- 16:29 GMT: Issue 10: wrap-up notes (QC, speed, per-area table)

## 18 Nov 2026, 08:44 GMT: Issue 11 started: next four closest areas (Pete: "yes, let's do some more now")
Measured as before: straight-line distance from Poole (50.715, -1.9872) to each area's official centre point (ONS principal-area centroids for Wales; ceremonial-county centroids for England), skipping the 36 live areas (work/next_areas_distances.json, rechecked by haversine today):
- Carmarthenshire: 126.0 mi
- Powys: 128.9 mi
- Essex: 132.0 mi
- Shropshire: 135.9 mi
(Next after these: Cambridgeshire 137.1, Ceredigion 138.1.)
Setup: counties.json (Carmarthenshire and Powys added, Essex and Shropshire switched on; all four in_progress, orders 37-40), county_of rules, DIST2CTY (Southend-on-Sea and Thurrock → Essex; Telford and Wrekin → Shropshire), NEWCTY, and the publish.sh URL check for 40 areas.
Discovery: active only; SIC 43120 43999 81300 42110 43110 02100 02200 77320 42210; up to 30 pages per search; every postcode district touching each area (postcodes.io outcode district lists, work/i11_outcodes.json: Carmarthenshire 22, Powys 29, Essex 78, Shropshire 44; 164 unique). CF14 8LH default-address companies are excluded.
- 09:31 GMT: discovery done for all four (922 searches with results; deepest page 10 of 30 (SS9 43999), so nothing capped; 0 CF14 8LH rows). 18 searches that errored were rerun (+257 rows); the 3 that errored again were rerun once more and all succeeded (IG10 43999 +109). Web-checks: Powys 43 trade-named leads, 38 probed, 2 accepted (Beacons Tree Services LD3, D.R.V Trees SY20); Carmarthenshire 67 leads, 43 probed, 5 accepted (Tas Plant Hire, Keltic Grounds Wales, Gower Plant Hire, M Plant Hire, A Thomas Plant Hire), all kept after hand-check. Shropshire web-check running.
- 09:33 GMT: build 11a: Carmarthenshire 246 listed (5 checked, cover star A Thomas Plant Hire SA39), Powys 192 (2 checked, Beacons Tree Services LD3), Essex 5,166 and Shropshire 721 (web-checks pending; cover stars are in-area Companies House leads for now). Site 40 areas, 62,029 listed, 1,694 checked, 12,008 not in business. All 40 cover stars in-area. Border additions from the new searches: Greater London +155, Herefordshire +13, Worcestershire +6, Hertfordshire +1. Two existing leads moved area because Companies House now shows a new registered office (not deleted): Green Hat Solutions BH21 → CM14 (Dorset → Essex), Strongpro Construction Repair Services TQ12 → LD3 (Devon → Powys).

- 09:34 GMT: Issue 11 b1 publish attempt (refused, see next line)
- 09:35 GMT: first publish attempt refused by sync_site.py: index_offline.html is now 48.7 MB (guard is 45 MB; it was 44.1 MB at Issue 10). Added a TF_SKIP_OFFLINE=1 switch so the live offline page stays at its Issue 10 copy for now; everything else publishes. Open issue for Pete: the offline page needs slimming (60,335 Companies House leads carry 14 MB of source records and 5 MB of score breakdowns).

- 09:35 GMT: Issue 11 b1: Carmarthenshire, Powys, Essex and Shropshire added (active only, full SIC set); first Welsh web-checks
- 09:41 GMT: build 11b: Shropshire web-check (170 trade-named leads, 116 own-site domains probed): 17 accepted, all kept after hand-check (Hamer Forestry's SY15 6BH registered office geocodes to Shropshire). Shropshire 721 listed, 17 checked, cover star Ap Precision Groundworks (DY14, in-area). Essex web-check running.

- 09:42 GMT: Issue 11 b2: Shropshire first 17 web-checked firms
- 09:46 GMT: cover check (Carmarthenshire, Powys, Essex, Shropshire at 320/360/390/768/1024/1280 px): no overflow; long names fit. Fixed in tools/page.html: the totals line now uses thousands separators (was "plus 53844 Companies House leads"), and an area with no checked driveway firms leads with its checked-firm count instead of "0 checked driveway firms" (Swansea, Carmarthenshire, Powys). Goes live with the next build.
- 09:59 GMT: build 11c (page fixes only, no data change): big numbers now use thousands separators (cover totals line, stats strip, cover badge, county index); the cover badge shrinks 5- and 6-character numbers so "62,029" and "14,618" stay inside the circle (before, 5-digit totals ran past its edge at 1024-1280 px). Checked at 320/360/390/768/1024/1280 px: no overflow.

- 09:59 GMT: Issue 11 b3: cover fixes (thousands separators, badge fit, no-driveway headline)
- 10:20 GMT: resumed after interruption; Essex web-check (450 trade-named leads, started 09:37) still in its DNS stage, nothing lost.
- 10:25 GMT: Essex DNS stage done: 251 of 450 leads have a live own-site domain (446 domains to probe; 16 DNS lookups failed and were not cached).
- 10:38 GMT: build 11d: Essex web-check batch 1 (first ~200 of 446 probed domains): 18 accepted, 16 kept (dropped Composite Decking World: online decking shop; Greenacre Arboriculture: tree-survey consultancy). Essex 5,166 listed, 16 checked, cover star Bell Fencing (CM7, site postcode CM7 4AR, in-area).

- 10:38 GMT: Issue 11 b4: Essex first 16 web-checked firms
