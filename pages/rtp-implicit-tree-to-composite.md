---
---

# Let's extract some leafs

```java {all|3-8}
public static String exportFullXml(Collection<Order> orders) {
    // ...
    xml.append("<price");
    xml.append(" currency='");
    xml.append(product.getPrice().currency());
    xml.append("'>");
    xml.append(product.getPrice().amount());
    xml.append("</price>");
    // ...
}
```

---

# Let's extract some leafs

```java {19-21}
public static String exportFullXml(Collection<Order> orders) {
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
            xml.append(" id='");
            xml.append(product.getId());
            xml.append("'");
            if (product.isEvent()) {
                xml.append(" stylist='");
                xml.append(stylistFor(product));
                xml.append("'");
                //
                somewhere here
                //
```

<v-click>

and duplicated

</v-click>

---
transition: fade
---

# Let's extract some leafs

```java {3-8}
public static String exportFullXml(Collection<Order> orders) {
    // ...
    xml.append("<price");
    xml.append(" currency='");
    xml.append(product.getPrice().currency());
    xml.append("'>");
    xml.append(product.getPrice().amount());
    xml.append("</price>");
    // ...
}
```

---

# Let's extract some leafs

```java {3|none}
public static String exportFullXml(Collection<Order> orders) {
    // ...
    product.getPrice().writeFullXml(xml);
    // ...
}
```

```java {3-8|all|5,7}
public record Price(double amount, Currency currency) {
    public void writeFullXml(StringBuilder xml) {
        xml.append("<price");
        xml.append(" currency='");
        xml.append(currency);
        xml.append("'>");
        xml.append(amount);
        xml.append("</price>");
    }
```

<v-click>

Easy!

</v-click>

<!--
That's the whole point in refactoring.
All the tests pass.
-->
