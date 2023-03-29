---
layout: statement
transition: fade
---

<v-click>

## Replace Implicit Tree with

</v-click>

# Composite

<v-after>

from "Refactoring to Patterns"

</v-after>

---
transition: fade
---

# Small steps

```java {8-13,18-23}
public static String exportFullXml(Collection<Order> orders) {
    StringBuilder xml = new StringBuilder();
    ...
    for (Order order : orders) {
        ...
        for (Product product : order.getProducts()) {
            ...
            xml.append("<price");
            xml.append(" currency='");
            xml.append(product.getPrice().currency());
            xml.append("'>");
            xml.append(product.getPrice().amount());
            xml.append("</price>");

public static String exportStore(Store store) {
    ...
    for (Product product : store.getStock()) {
        xml.append("<price");
        xml.append(" currency='");
        xml.append(product.getPrice().currency());
        xml.append("'>");
        xml.append(product.getPrice().amount());
        xml.append("</price>");
```

---
transition: fade
---

# Small steps

```java {3,8|none}
public static String exportFullXml(Collection<Order> orders) {
    ...
    product.getPrice().writeXml(xml);
    ...

public static String exportStore(Store store) {
    ...
    product.getPrice().writeXml(xml);
    ...
```

```java {all|5,7}
public record Price(double amount, Currency currency) {
    public void writeXml(StringBuilder xml) {
        xml.append("<price");
        xml.append(" currency='");
        xml.append(currency);
        xml.append("'>");
        xml.append(amount);
        xml.append("</price>");
    }
```

<!--
That's the whole point in refactoring.
All the tests pass.
-->
