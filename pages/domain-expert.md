---
transition: fade
---

# We've got our domain expert

```java
@AllArgsConstructor
public class Ledger {
    private final List<Order> orders;

    public Money tax() {
        return orders.stream().map(Order::tax).sum();
    }
}
```

---
transition: fade
---

# We've got our domain expert

```java
public class Ledger
```

---
transition: fade
---

# We've got our domain expert

```java
public class Account
```

<!--
On a second thought
-->
