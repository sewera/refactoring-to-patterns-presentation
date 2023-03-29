---
---

# Dirty

```java
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
            xml.append(" id='");
            xml.append(product.getId());
            xml.append("'");
            if (product.isEvent()) {
                xml.append(" stylist='");
                xml.append(stylistFor(product));
                xml.append("'");
            }

            if (product.getWeight() > 0) {
                // 22 lines more
```

---

# Clean

```java
public static String exportFull(Account account) {
    return XML_HEADER + account.fullXml();
}
```
