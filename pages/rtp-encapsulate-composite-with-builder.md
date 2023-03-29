---
layout: statement
transition: fade
---

<v-click>

## Encapsulate Composite with

</v-click>

# Builder

<v-after>

from "Refactoring to Patterns"

</v-after>

---

# Delegate the procedure

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

<v-click>

```xml
<name parameter="parameter value">
    value
</name>
```

</v-click>

---
transition: fade
---

# Don't break the interface... just yet

```java {all|3-7|8}
public record Price(double amount, Currency currency) {
    public void writeXml(StringBuilder xml) {
        var tag = XmlTag.builder()
                .withName("price")
                .withParameter(XmlParameter.of("currency", currency.toString()))
                .withValue(amount)
                .build();
        xml.append(tag);
    }
```

---

# Simplify the interface

```java
public record Price(double amount, Currency currency) {
    public XmlTag xml() {
        return XmlTag.builder()
                .withName("price")
                .withParameter(XmlParameter.of("currency", currency.toString()))
                .withValue(amount)
                .build();
    }
```

