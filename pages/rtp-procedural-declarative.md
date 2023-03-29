---
transition: fade
---

# Procedural

```java {all|3,6,8|4-6|7}
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
1. Procedural
2. Create and name a tag
3. Create and name a parameter with value
4. Add a value
-->

---
transition: fade
---

# Declarative

```java {all|3|3-4|3-6|3-7|3-8}
public record Price(double amount, Currency currency) {
    public XmlTag xml() {
        return XmlTag.builder()
                .withName("price")
                .withParameter(XmlParameter.of(
                    "currency",
                    currency.toString()))
                .withValue(amount)
                .build();
    }
```
