---
title: Beta API Reference
---

# Beta API Reference

## Sync endpoints (conceptual)

```mermaid
sequenceDiagram
    participant GH as GitHub
    participant GA as GitHub Action
    participant CF as Confluence
    GH->>GA: PR merged to main
    GA->>CF: create/update pages
    GA->>CF: trash removed pages
    CF-->>GA: results
```

## Methods

| Method | Purpose |
|---|---|
| `mark publish` | Render diagrams and publish pages |
| `mark publish --compile-only --check-links internal` | PR validation, no credentials |
| `mark --track-pages` | Track each file's page across renames |

Back to [Beta Documentation Home](../index.md).
