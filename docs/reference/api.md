---
doc_id: 63c2eaea-7bc7-4655-8062-54798e6cc8a4
title: Beta API Reference
---

# Beta API Reference

## Sync endpoints (conceptual)

```mermaid
sequenceDiagram
    participant GH as GitHub
    participant GA as GitHub Action
    participant CF as Confluence
    GH->>GA: push to main
    GA->>CF: create/update pages
    GA->>CF: trash removed pages
    CF-->>GA: results
```

## Methods

| Method | Purpose |
|---|---|
| `sync.py` | Reconcile pages |
| `render_mermaid.py` | Render diagrams |
| `validate.py` | PR checks |

Back to [Beta Documentation Home](../index.md).
