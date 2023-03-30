---
transition: fade
---

# Don't guess

```java
@Builder(setterPrefix = "with")
@AllArgsConstructor(access = PRIVATE)
class Simple {
  private String label;
}
```

```java
var simple = Simple.builder()
  .withLabel("label")
  .build();
```

<!--
People often make their lives harder.

The class will have more properties in the future.
-->

---
transition: fade
---

# Don't guess

```java
@Builder(setterPrefix = "with")
@AllArgsConstructor(access = PRIVATE)
class Simple {
  private String tag;
}
```

```java
var simple = Simple.builder()
  .withTag("label")
  .build();
```

<!--
Prematurely set a direction
-->

---
transition: fade
---

# Don't guess

```java
@AllArgsConstructor
class Simple {
  private String whatever;
}
```

```java
var simple = new Simple("label");
```
