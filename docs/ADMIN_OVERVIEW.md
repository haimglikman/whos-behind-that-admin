# Who's Behind That? — Admin

**Doc version:** 1.0.1 · Reflects server v2.6.0 · admin v2.29.0 · client v1.20.0

The operator console for WBT, at `admin.whosbehindthat.com`. It runs the same analysis as the public client, plus everything needed to operate the product: the data from all users, the entity database, AI prompts and models, the FAQ, monitoring, and marketing output.

For the full system (server, scoring engine, database), see the [architecture doc](https://github.com/haimglikman/whos-behind-that-server/blob/main/docs/ARCHITECTURE.md).

**Core principle:** admin sees all data from all clients; a client sees only its own.

## Tabs

| Tab | Purpose |
|---|---|
| Analyze | Scan posts and articles; research authors; manual paste with optional metadata (title, author, image) for blocked sites |
| Post history | Every scan from every user, with filters (user, source, platform, entity, actor, model) and per-scan Claude/Jev tokens and cost |
| Investigate / Clusters | Run investigations and review every saved cluster |
| Actors | All actor and publication research, from all users |
| Entity database | The political actors that posts are scored against: edit, import/export, AI refresh, changelog |
| Prompts | Edit, version, roll back and activate the AI prompts, and choose the model per prompt |
| FAQ | Edit the FAQ the client displays |
| Marketing | Generate Instagram carousels from saved clusters |
| About & Setup | Admin access, deployed versions, usage stats, tools & dependencies, models in use, changelog |

## How it works

- **A single file:** `index.html` with no build step, hosted on GitHub Pages under the custom domain.
- **Admin key:** operator actions and all-user data require the admin key. Admin asks for it once, keeps it only in that browser (never in the public HTML), and attaches it to every request to the WBT server. A rejected key triggers a new prompt, and About & Setup has an Admin access section to change or forget it. Admin requests are exempt from the server's daily quotas.
- **Publishing from admin:** entity, prompt and FAQ changes are pushed to the server DB, and the server and client pick them up without a deploy.
- **Entity versioning:** patch for single edits, minor for an AI refresh, major for an import. The entity version is recorded with every scan.
- **AI entity refresh:** Claude with web search reviews every entity in batches and returns only the fields that changed, so the database follows political developments.
- **Monitoring:**
  - deployed versions of admin, server, entities and every prompt, plus client versions with device counts
  - token usage and cost, split between Claude and Jev
  - the live model and service configuration, from the server's `/system/info`
- **Instagram carousel generator:** renders 1080×1080 slides (hook → posts → cluster → summary) with the HTML Canvas API from saved cluster data, and exports them as a ZIP of JPEGs with JSZip.
