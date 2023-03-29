---
---

# Capture the concept, not the process

```java {all|3|5|7|9|12-16}
@Builder(toBuilder = true)
public class XmlTag {
    private final String name;
    @Builder.Default
    private final String value = "";
    @Singular
    private final List<XmlParameter> parameters;
    @Singular
    private final List<XmlTag> children;

    @Override
    public String toString() {
        var xml = new StringBuilder();
        // all the boring stuff
        return xml.toString();
    }
}
```

---
transition: fade
---

# Capture the concept, not the process

```java {all|8}
public record Price(double amount, Currency currency) {
    public void writeFullXml(StringBuilder xml) {
        var tag = XmlTag.builder()
                .withName("price")
                .withParameter(XmlParameter.of("currency", currency.toString()))
                .withValue(amount)
                .build();
        xml.append(tag.toString());
    }
```

---

# Capture the concept, not the process

```java
public record Price(double amount, Currency currency) {
    public XmlTag fullXml() {
        return XmlTag.builder()
                .withName("price")
                .withParameter(XmlParameter.of("currency", currency.toString()))
                .withValue(amount)
                .build();
    }
```

