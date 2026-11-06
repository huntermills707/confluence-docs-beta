# confluence-docs-beta

Twin content repository for the GitHub → Confluence docs-as-code pipeline. It
publishes into the **same** Confluence space (`GHConfDocs`) as
`confluence-docs-alpha`, but under **its own root page**. Publishing is done
by [mark](https://github.com/kovetskiy/mark) from a pinned Docker image — no
custom sync code lives in this repository. Quick facts:

* When a pull request to `main` merges, `mark publish` reconciles
  `docs/**/*.md` with this repository's subtree.
* Every document carries a `title` in YAML front matter; pages are matched by
  title in the space, and mark's page manifest (prefix `beta.sync`, stored in
  Confluence) tracks each file's page across renames and retitles.
* Titles must be unique within the space (this repo uses "Beta …" prefixes).
* The **Sync docs to Confluence** workflow runs on merges to `main` and via
  `workflow_dispatch` (with a `dry_run` input).
* **Validate docs (PR)** checks pull requests (`--compile-only
  --check-links internal`) without Confluence credentials.
* Removed files have their pages **trashed** (reversible), scoped to this
  repository's root page; a run with any failure removes nothing.

## Repository secrets

| Secret | Value |
|---|---|
| `ATLASSIAN_BASE_URL` | `https://jaegermolino.atlassian.net` |
| `ATLASSIAN_USER_EMAIL` | Atlassian account email |
| `ATLASSIAN_API_TOKEN` | Atlassian Cloud API token |
| `CONFLUENCE_SPACE_KEY` | `GHConfDocs` |
| `CONFLUENCE_ROOT_PAGE_ID` | **this repo's own root page id** (not alpha's) |

The root page is only ever the parent of this repository's pages — mark
never writes to it or deletes it.

## Layout

```text
docs/
├── index.md              page for docs/ itself (documentation home)
├── getting-started.md
├── reference/
│   ├── index.md          folder page for reference/
│   └── api.md
└── assets/
    └── pipeline.png

.github/workflows/        thin mark consumers (pinned image tag)
```

Change both workflow pins (`env.MARK_IMAGE`) together to upgrade or roll
back the publisher.
