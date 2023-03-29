---
transition: fade
---

# Product Export refactoring kata

```mermaid
flowchart LR
  E(Export XML)
  Product --> Orders
  Product --> Store
  Orders --> E
  Store --> E
```
