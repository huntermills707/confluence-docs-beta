---
title: Beta Documentation Home
---

# Welcome to the Beta documentation

This is the second dummy repository in the docs-as-code proof of concept. It
publishes into the *same* Confluence space as `confluence-docs-alpha`, but
under its own root page — the two repositories can never modify or delete
each other's pages.

## Publishing pipeline

```mermaid
flowchart LR
    S[Mermaid source in Markdown] --> R[mark renders the diagram]
    R --> U[Uploaded as page attachment]
    U --> P[Confluence page shows diagram]
```

## Reading order

1. [Beta Getting Started](getting-started.md) — setup basics.
2. [Beta API Reference](reference/api.md) — endpoints and examples.

## Screenshot

![Beta pipeline overview](assets/pipeline.png)

## External link

- [GitHub Actions documentation](https://docs.github.com/en/actions)

## Isolation rules

- Each repository keeps its own page manifest in Confluence, so it only ever
  recognises pages it published itself.
- A repository only ever publishes beneath its own root page.
- Deletions are limited to tracked pages beneath that root.
