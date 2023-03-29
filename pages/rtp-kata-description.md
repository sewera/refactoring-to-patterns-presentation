---
layout: two-cols
transition: fade
---

# Example: Product Export

```mermaid {scale: 0.7}
flowchart LR
  E(Export XML)
  P1[Product]
  P2[Product]
  P3[Product]
  P4[Product]
  P5[Product]
  O1[Order]
  O2[Order]
  P1 -- buy --> O1
  P2 -- buy --> O1
  P3 -- buy --> O2
  P4 -- stock --> Store
  P5 -- stock --> Store
  subgraph Orders
    OL{{Collect}}
    O1 -.-> OL
    O2 -.-> OL
  end
  OL --> E
  Store --> E
```

::right::

<div class="py-12" />

<v-click>

```xml
<orders>
  <order id="O1">
    <product id="P1" weight="0.5">
    <price currency="USD">
      149.99
    </price>
    Product One
    </product>
    ...
  </order>
  ...
</orders>
```

</v-click>
