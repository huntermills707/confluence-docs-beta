---
doc_id: d5b15477-25d9-4f06-996a-c684d07816c1
title: Beta Getting Started
---

# Getting Started with Beta

Beta is intentionally boring: it exists to prove **repository isolation**
inside one Confluence space.

## Formatting sample

*This paragraph* has **multiple** ~~styles~~ and `inline code`.

## Checklist

- [x] Create the repository
- [x] Add front matter with doc_ids
- [ ] Merge documentation
- [ ] Verify Confluence sync

## Quoting

> Two repositories, one space, zero interference.

## Command example

```bash
git commit -am "docs: update getting started"
git push origin main
```

See the [Beta API Reference](reference/api.md) next, or return to
[Beta Documentation Home](index.md).
