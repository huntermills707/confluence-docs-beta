# confluence-docs-beta

Twin dummy repository for the GitHub → Confluence docs-as-code proof of
concept. It publishes into the **same** Confluence space (`GHConfDocs`) as
`confluence-docs-alpha`, but under **its own root page**. Each repository
only ever reconciles pages whose `ghdocsync` content property names itself
and that live beneath its own root — cross-repository interference is
impossible by construction.

See the canonical
[`confluence-docs-sync`](https://github.com/huntermills707/confluence-docs-sync)
documentation for the sync mechanics and release process. This repository
contains content and thin workflows pinned to the same tool release as Alpha.
Quick facts:

* Every document carries a stable `doc_id` in its front matter; pages are
  matched by that id, never by title or path.
* Titles must be unique within the space (this repo uses "Beta …" prefixes).
* The **Sync docs to Confluence** workflow runs on pushes to `main` and via
  `workflow_dispatch` (with `dry_run` and `force_delete` inputs).
* **Validate docs (PR)** checks pull requests without Confluence credentials.
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

The tool repository is public and requires no tool-specific checkout
credential.

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

.github/workflows/       thin consumers pinned to v1.0.0 by full commit SHA
```

Change both workflow pins together to upgrade or roll back the tool. Do not
copy sync scripts or dependencies into this repository.
