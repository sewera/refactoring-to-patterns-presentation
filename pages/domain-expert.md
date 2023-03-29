---
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

# Okay, now we've got a _real_ domain expert

```java
public class Account
```
