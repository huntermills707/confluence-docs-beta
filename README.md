# confluence-docs-beta

Twin dummy repository for the GitHub → Confluence docs-as-code proof of
concept. It publishes into the **same** Confluence space (`GHConfDocs`) as
`confluence-docs-alpha`, but under **its own root page**. Each repository
only ever reconciles pages whose `ghdocsync` content property names itself
and that live beneath its own root — cross-repository interference is
impossible by construction.

See the [confluence-docs-alpha README](../confluence-docs-alpha/README.md)
for the full documentation of the sync mechanics; everything applies
identically here. Quick facts:

* Every document carries a stable `doc_id` in its front matter; pages are
  matched by that id, never by title or path.
* Titles must be unique within the space (this repo uses "Beta …" prefixes).
* The **Sync docs to Confluence** workflow runs on pushes to `main` and via
  `workflow_dispatch` (with `dry_run` and `force_delete` inputs).
* **Validate docs (PR)** checks pull requests without credentials.
* Deletions are trashed (reversible), happen last, and are capped at 5 pages
  or 20% of managed pages unless `force_delete` is set.

## Repository secrets

| Secret | Value |
|---|---|
| `ATLASSIAN_BASE_URL` | `https://jaegermolino.atlassian.net` |
| `ATLASSIAN_USER_EMAIL` | Atlassian account email |
| `ATLASSIAN_API_TOKEN` | Atlassian Cloud API token |
| `CONFLUENCE_SPACE_KEY` | `GHConfDocs` |
| `CONFLUENCE_ROOT_PAGE_ID` | **this repo's own root page id** (not alpha's) |

## Layout

```text
docs/
├── index.md              home page
├── getting-started.md
├── reference/
│   ├── _index.md         folder page with stable identity
│   └── api.md
└── assets/
    └── pipeline.png
```
