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
