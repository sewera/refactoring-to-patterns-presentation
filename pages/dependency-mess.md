---
transition: fade
---

# Dependency mess

```mermaid {scale: 0.6}
classDiagram
    Product <|-- StoreEvent
    XMLExporter ..> Product
    XMLExporter ..> Store
    XMLExporter ..> Price
    XMLExporter ..> Order
    StoreEvent ..> Store
    Store ..> Product
    Order ..> Product
    Product ..> Price
    XMLExporter ..> TaxCalculator
    TaxCalculator ..> Order
    TaxCalculator ..> Product
    class XMLExporter {
        + exportFullXml()
    }
```

---

# A cleaner goal

```mermaid {scale: 0.6}
classDiagram
    XMLExporter ..> Account
    Account ..> Order
    Order ..> Product
    Product ..> Price
    Product <|-- StoreEvent
    Store ..> Product
    XMLExporter ..> Store
    class XMLExporter {
        + exportFullXml()
    }
```

