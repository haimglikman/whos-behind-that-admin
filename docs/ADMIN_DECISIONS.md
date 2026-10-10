# Who's Behind That? — Admin Decisions

Key decisions behind the operator console. Each entry covers the problem, what was chosen, and the result. Version numbers refer to the admin changelog.

---

## 1. Split one app into admin and client
**Admin v2.0.0 · Client v1.0.0**

**Problem:** WBT began as one app that combined analysis with operator tools: entity editing, full history, setup. That isn't something to hand to the public.

**Decision:** Split it into two frontends sharing one server and database. The public client is anonymous and sees only its own data; the admin sees everything. Every scan is tagged with its source (admin or client) and a hashed user ID, so the admin can filter by either.

**Outcome:** A safe public product, plus a console that can watch real usage and judge scan quality across all users.

---

## 2. The entity database as versioned data
**v2.5.0, v2.6.0, v2.10.0, v2.14.2**

**Problem:** The entities (parties, leaders, governments, movements) were hard-coded, while Israeli politics kept shifting: splits, mergers, new parties ahead of the 2026 election.

**Decision:**
- Move entities into data: JSON import/export, then semantic versioning (patch on edit, minor on AI refresh, major on import), with the version recorded in every scan ID.
- Add an AI refresh: Claude with web search reviews every entity and returns only the fields that changed. Batches run with `Promise.allSettled`, so one failure doesn't abort the rest.
- Push every change to the server DB.

**Outcome:** Entities change without code changes, every scan can be traced to the entity version it was scored against, and keeping the database current takes one button.

---

## 3. Make cost visible at every level
**v2.8.0, v2.9.0, v2.23.0–v2.24.0**

**Problem:** Every scan costs AI tokens, and after the v2 engine added a second model (Jev), the cost of each scan was no longer obvious.

**Decision:** Track tokens per scan and in aggregate, with editable price rates. Later, split the totals into Claude and Jev, and show per-scan token counts and the models used, with a model filter in history.

**Outcome:** The cost effect of each engine and model change can be measured directly, including the move from Sonnet batch scoring to Jev + Opus.

---

## 4. Render the Instagram carousel in the browser
**v2.17.0–v2.19.1**

**Problem:** Turning saved clusters into Instagram content (1080×1080 slides) by hand was slow, and a server-side renderer would mean heavy dependencies.

**Decision:** Render the slides with the HTML Canvas API directly in admin, following a JSON design spec, and export them as a ZIP with JSZip. Issues solved along the way:
- **Cross-origin images** (favicons, article thumbnails) blocked export, so images are loaded through a server image proxy (`/proxy-image`). Each image is first drawn on an offscreen canvas; if it would still taint the canvas, it is skipped rather than blocking the export.
- **Long text**: the cluster slide uses a fitting strategy. It tightens spacing first, then shrinks the font down to a minimum, so the full analysis is always shown and never truncated.
- **Hebrew and Arabic headlines** are laid out right-to-left on an offscreen canvas.
- Slides are built from cluster data in the server DB, and generated carousels persist locally so they can be downloaded again.

**Outcome:** One click turns a saved investigation into a ready-to-post carousel, with no server-side rendering stack.

---

## 5. Live introspection instead of hand-maintained lists
**v2.16.0, v2.21.0, v2.26.0**

**Problem:** After several model and service changes, it was hard to tell what was actually running in production: which versions, which models, which services were configured.

**Decision:**
- A Deployed versions panel shows admin, server, entities and every prompt, plus client versions with device counts and last-seen dates. Its data is fetched in parallel.
- A Tools & dependencies section lists every third-party service.
- Since v2.26.0, both lists load live from the server's `/system/info` (which models are in use and which services are configured, with no secrets exposed). Older servers fall back to the built-in list.

**Outcome:** One screen answers "what is running right now?", and the answer comes from the system itself.
