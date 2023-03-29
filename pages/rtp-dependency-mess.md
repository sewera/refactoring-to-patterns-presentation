---
transition: fade
---

# Problem: Dependency Mess

```mermaid
classDiagram
    direction LR
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
transition: fade
---

# Problem: Dependency Mess

```java {all|8|10|13-14|17,19|21}
public static String exportFull(Collection<Order> orders) {
    StringBuilder xml = new StringBuilder();
    xml.append("<?xml version=\"1.0\" encoding=\"UTF-8\"?>");
    xml.append("<orders>");
    for (Order order : orders) {
        xml.append("<order");
        xml.append(" id='");
        xml.append(order.getId());
        xml.append("'>");
        for (Product product : order.getProducts()) {
            xml.append("<product");
            ...
            if (product.isEvent()) ...
            if (product.getWeight() > 0) ...
            xml.append("<price");
            xml.append(" currency='");
            xml.append(product.getPrice().getCurrency());
            xml.append("'>");
            xml.append(product.getPrice().getAmount());
            xml.append("</price>");
            xml.append(product.getName());
            xml.append("</product>");
            ...
```

---
transition: fade
---

# Goal

```mermaid
classDiagram
    direction LR
    XMLExporter ..> Account
    Account ..> Order
    Order ..> Product
    Product <|-- RegularProduct
    Product <|-- StoreEvent
    RegularProduct ..> Price
    StoreEvent ..> Price
    Store ..> Product
    XMLExporter ..> Store
    class XMLExporter {
        + exportFullXml()
    }
    class Product {
        <<abstract>>
    }
```

---
transition: fade
---

# Goal

```java
public static String exportFull(Account account) {
    return XML_HEADER + account.xml();
}

public static String exportStore(Store store) {
    return XML_HEADER + store.xml();
}
```
