## Changelog

### v2.7.0 (admin) | Server: v1.13.0 | Client: v1.8.0
- Actors tab now syncs from server DB — client actor searches visible in admin with source badge, user badge, scan ID, and source article link
- Publication card shown for actors researched from news articles
- News platform icon (📰) in history
- Actor research generates a proper scan ID

### v2.6.0 (admin) | Server: v1.12.4 | Client: v1.7.0
- Entity DB versioning: semantic versioning (major.minor.patch) shown as badge in Entity Database tab
- Patch auto-increments on every save, edit, add, delete, or import
- Minor/Major bump buttons for intentional restructures
- DB version included in scan IDs: WBT-ADMIN-{date}-{appVer}-{srvVer}-DB{version}-{random}
- Export includes version in filename and JSON; import reads and restores version from file

### v2.5.0 (admin) | Server: v1.12.4 | Client: v1.7.0
- Entity database: Import/Export buttons — download entities as JSON, upload to replace. Entity management no longer requires code changes.
- Entity: Ben Gvir & Smotrich split into two separate entities (id:28 Otzma Yehudit, id:28 Religious Zionism)
- Entity: Israeli Opposition Bloc renamed to Naftali Bennett / Bennett 2026 (Lapid joins his list)
- Entity: Israeli Left / Peace Camp replaced by Yair Golan / The Democrats
- Entity: Gantz updated to reflect diminished opposition role
- Entity: Netanyahu/Likud updated with 2026 election context
- Entity added: Gadi Eisenkot / Yashar! (id:57)
- Entity added: Shas / Aryeh Deri (id:58)
- Entity added: United Torah Judaism / UTJ (id:59)
- Entity added: Israeli Security Establishment / IDF / Shin Bet / Mossad (id:60)
- Entity added: Israeli Business & Tech Sector (id:61)

### v2.4.1 (admin) | Server: v1.12.4 | Client: v1.7.0
- In-app changelog updated with all versions from v1.8.1 through v2.4.0 — was last updated at v1.8.0

### v2.4.0 (admin) | Server: v1.12.4 | Client: v1.7.0
- Added Legal & Disclaimer section to About & Setup tab
- Updated contact email to contact@whosbehindthat.com

### v2.3.1 — bug fix (admin) | Server: v1.12.2 | Client: v1.5.1
- X posts now stored with proper username URL (x.com/username/status/...) instead of /i/status/ format from mobile share sheet

### v2.3.0 (admin) | Server: v1.12.0 | Client: v1.4.0
- Analyze tab: post text now shown below results header
- Analyze tab: scan ID shown prominently with "Scan ID" label
- Analyze tab: "↗ Open post" button next to URL
- History filters: added Search by ID and Search by URL fields
- History filters: Entity match replaced with multi-select with autocomplete — type to search, click to add, tags show selected entities

### v2.2.1 — bug fix (admin) | Server: v1.11.1 | Client: v1.2.1
- Fixed migration for client scans with numeric IDs — now correctly uses usr_XXXX prefix (e.g. WBT-7XB1-...)
- Fixed hashToPrefix to strip usr_ prefix rather than hashing it again
- Back button from analyzed post now returns to history tab instead of looping through analyze→history→external
- Scan ID pushed to URL hash when opening a history entry (#analyze/WBT-ADMIN-...)

### v2.2.0 (admin) | Server: v1.11.0 | Client: v1.2.0
- Scan IDs now include user prefix: WBT-ADMIN-{date}-... for all admin scans
- Retroactive migration: old WBT-{date}-... IDs upgraded to WBT-ADMIN-{date}-..., numeric IDs converted to WBT format
- Scan ID now shown in results header when viewing a post analysis
- Browser back/forward buttons now navigate between tabs within the app

### v2.1.1 — bug fix (admin) | Server: v1.11.0 | Client: v1.0.1
- Fixed all tabs except Analyze being inaccessible — pages were accidentally nested inside page-analyze due to unclosed page-content div

### v2.1.0 (admin) | Server: v1.11.0 | Client: v1.0.1
- Fixed client scan counter not updating from history
- Fixed source/user filters not working on client scans — sync now correctly maps source and deviceId fields
- Fixed oversized alignment dial when replaying history entries
- Browser tab title now shows "Who's Behind That? — Admin"

### v2.0.0 (admin) | Server: v1.11.0 | Client: v1.0.1
- New design: Nunito font, light blue background, navy topbar, rounded cards
- Two scan counters: Admin scans + Client scans (separate tracking)
- History filters: added Source (Admin/Client) and User (usr_XXXX) filters
- Client scans now visible in admin history with source and user badges
- Fixed _cachedSrvVersion bug that caused successful scans to save as failed
- Bottom status bar with live server status, app and server versions

### v1.13.3 — bug fix
- Fixed _cachedSrvVersion is not defined error that caused successful analyses to save as failed
- saveToHistory errors no longer bubble up to trigger failed scan entries

### v1.13.2 — bug fix
- Error messages now shown in persistent copyable banner instead of disappearing toast
- Failed scans saved to history with red styling and error reason
- Error banner clears on new analysis

### v1.13.1 — bug fix
- Fixed duplicate history entries: saveToHistory now deduplicates before inserting
- Filters now retroactive: platform inferred from URL for legacy entries, entity search covers all text fields

### v1.13.0
- Convergent interest detection: hidden shared interests between rival entities shown below results
- History filters: platform, app/server version, entity, date range, score, AI score, alignment type, has comment
- Platform icon shown in each history card
- Platform field stored per scan

### v1.12.3 — bug fix
- Restored original auto-fetch behavior for Instagram

### v1.12.2 — IRELEVANT BUG FIXES!!!

### v1.12.1 — bug fix
- Instagram: text area shown immediately with clear message instead of failed auto-fetch attempt
- Instagram routes directly to manual text analysis on Analyze click

### v1.12.0
- Instagram and Facebook now fetch automatically like X — no more manual text pasting
- Manual text fallback still available if post is private or login-gated

### v1.11.0
- Entity profiles enriched with Hebrew and Arabic political vocabulary
- Key terms: ביביזם, עסקת חטופים, פלישה, ריבונות, אכיפה, מאחזים (Hebrew); مقاومة, محور المقاومة, التطبيع, الاحتلال (Arabic)

### v1.10.2 — bug fix
- Fixed duplicate history entries: sync now uses URL+timestamp as secondary dedup key
- Migration now removes existing numeric-ID duplicates of WBT entries on first load
- Local fullResult preserved when server entry doesn't include it

### v1.10.1 — bug fix
- History cards now fully clickable to open full analysis view
- Comment textarea click is isolated so typing a comment doesn't trigger navigation
- Added "view full analysis →" hint on cards that have a stored result

### v1.10.0
- Fixed duplicate history entries: deduplication now uses scanId as single key
- Entity relationships map: patrons, proxies, coalitions and rivals defined for all 56 entities

### v1.9.0
- Shared history: scans now stored in PostgreSQL and visible to all users
- Scan IDs: every scan gets a unique ID in format WBT-{date}-{appVer}-{srvVer}-{random}
- Version tracking: app and server version logged per scan
- Comments field: free-text comment on every scan, editable, server-synced
- Retroactive migration: existing localStorage scans get IDs, version labels, and empty comment fields
- Removed "Clear all" from history tab
- PostgreSQL setup guide added to About & Setup tab

### v1.8.1 — bug fix
- Fixed secondary alignment never showing: alignment field now mandatory in prompt
- Fixed rival entities both appearing: added explicit rule that criticizing an entity does not count as alignment with them

### v1.8.0
- Primary/secondary alignment split: primary = direct beneficiary, secondary = collateral beneficiary
- Visual distinction: solid vs dashed border
- New entities: Israeli Opposition Bloc, Protest Movement, Hostage Families Forum, Lieberman, Israeli Left, Arab Citizens of Israel

### v1.7.3 — bug fix
- Instagram/Facebook actor research now works: a handle input field appears
  automatically when an Instagram or Facebook URL is detected
- Actor research prompt now correctly triggers after analyzing Instagram posts

### v1.7.2 — bug fix
- Fixed actor research prompt not appearing after analyzing Instagram posts
- Instagram handle now extracted from server's oEmbed author_url, not the post URL

### v1.7.1 — bug fix
- Hardcoded default server URL so app works out of the box on any device
- Users no longer need to manually enter the server URL on first visit

### v1.7.0
- Server version badge added to sidebar below main version
- Fetched live from server health check on load — always reflects what's actually deployed
- Updates automatically when server URL changes

### v1.6.2 — bug fix
- Rebuilt entire JavaScript section from scratch after cascading corruption from prior edits
- Fixed: nav tabs not working, analyze button non-functional, version showing incorrectly
- All 50 entities, actor profiles, history, and analysis functions fully restored and verified

### v1.6.1 — bug fix
- Removed DEMOS data object and runDemo() function (260 lines of dead code from v1.5.0)
- Removed orphaned .demo-chip and .demo-label CSS styles
- Fixed entity database badge hardcoded to "20" — now shows correct count of 50
- Fixed wrong syntax in server file

### v1.6.0
- Actor profiles: Claude researches social media actors via OSINT, cached by handle
- Actors tab: browse, view, and delete all profiled actors
- Entity database expanded from 20 to 50 entities
- Media outlets (Al Jazeera, Al-Manar, Press TV) captured as MO instruments of patron entities

### v1.5.1 — bug fix
- Fixed undefined% alignment score when server response omits pre-computed pct field
- Added NaN guard in showResults to prevent rendering errors on malformed scores

### v1.5.0
- Auto-clear analyze tab when navigating away — URL and results reset automatically
- Removed demo scenario buttons from analyze tab
  
### v1.4.0
- Clickable history: every Post History entry opens the full analysis view
- Reframed from "manipulation detection" to "narrative alignment" — whose agenda does this serve?
- New "What this post leaves out" field on each entity match — the missing context
- Alignment color spectrum: cool blue → purple → amber → red-orange (intensity, not danger)
- Overall dial now shows strongest entity name and alignment score, not "manipulation probability"
- Server prompt updated: Claude now identifies missing context per match

### v1.3.0
- Proxy server: post text now fetched automatically from X, Facebook, Instagram
- API keys moved server-side: Anthropic key stored securely as env variable, never in browser
- Users just paste a URL — no setup or keys required
- Graceful fallback: manual text paste if auto-fetch fails (private/deleted posts)

### v1.2.0
- Reweighted scoring: hidden interest 55%, modus operandi 35%, public narrative 10%
- Updated Claude prompt: explicit manipulation detection philosophy — scores who benefits and how it was built, not just what it says
- UI labels now show dimension weights in entity match cards
- Richer 2–3 sentence "why" explanations citing specific post phrases and hidden interests served
- Demo scores recalculated under new model

### v1.1.0
- AI scoring engine: narrative matching now uses Claude AI (claude-sonnet) to semantically score post text against each entity's public narrative, interest, and modus operandi
- Post history tab: every analysis logged with URL, timestamp, score, and top entity matches
- Scan counter: sidebar shows total scans run and timestamp of last scan
- Version badge: displayed in sidebar, auto-increments with each release
- Post text input: paste area for post content (required due to browser CORS restrictions on social APIs)
- Dual API keys: separate fields for Anthropic (Claude scoring) and Hive (image AI detection)

### v1.0.0
- Initial release: core app, 20-entity Israeli-Palestinian conflict database, demo scenarios, editable entity database, Hive image detection
