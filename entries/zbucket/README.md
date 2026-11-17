# zbucket

Shared **Metrics** and **Knowledge** for the applications of a workspace.
Define metrics, explore dimensions and comparisons, compose dashboards from
saved queries, follow account and person timelines and conversion funnels
over event data; write and search Markdown knowledge with revisions. Every
backend that reports or reads does so with one integration identity and
explicit permissions.

## What the install makes

- A PostgreSQL 17 database (`db`, 5 GiB, daily backups kept seven days),
  attached as `DATABASE_URL`. The platform's databases carry pgvector,
  which Knowledge uses for semantic search.
- Three processes from the repository's `Procfile`: `web` (the UI and
  API), `worker` (ingestion, retention, indexing) and `funnels` (durable
  funnel runs). Each release migrates the database and imports the
  repository's documentation into Knowledge before it rolls out.

Nothing is asked at install. A **Voyage API key** is optional: with one,
Knowledge indexes documents with Voyage embeddings and searches by meaning;
without one, it searches by text and says so in the UI. The key can be set
later as the config var `VOYAGE_API_KEY`.

## Who gets in

zbucket trusts the platform's sign-in (`ZBUCKET_ACCESS=shpyrd`): the people
admitted to the project enter, and the workspace's administrators are
zbucket's administrators. Keep the project's access **authenticated**, as
installed. A public project would let anyone reach the UI, and integration
credentials are not meant to pass through the sign-in page.

Another project of the workspace reports to zbucket over its internal name,
`http://<slug>.internal`, after `shpyrd allow add project <caller>
--project <slug>`, with a `wh_` credential issued from **Integrations**.
See the [integration guide](https://github.com/shpyrd-io/zbucket/blob/main/docs/integrations.md).

## Build

Buildpacks, Node.js 24 (`BP_NODE_VERSION`), with `npm run build` at build
time. The repository's `.npmrc` installs its bundled design system as a
local package, which `npm ci` honours.
