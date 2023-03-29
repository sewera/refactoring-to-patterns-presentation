---
transition: fade
---

# Simplify your life

```java
public class Price {
    private final double amount;
    private final String currencyCode;
    public Price(double amount, String currencyCode) {
        this.amount = amount;
        this.currencyCode = currencyCode;
    }
    @Override
    public String toString() {
        return "Price{" + amount + '}';
    }
    public String getCurrency() {
        return currencyCode;
    }
    public double getAmount() {
        return amount;
    }
    // stuff
```

---

# Simplify your life

```java
public record Price(double amount, String currencyCode)
```

---
transition: fade
---

# Simplify your life

```java
public class Product {
    protected final String name;
    protected final String id;
    protected final int weight;
    protected final Price price;
    public Product(String name, String id, int weight, Price price) {
        this.name = name;
        this.id = id;
        this.weight = weight;
        this.price = price;
    }
    public String getName() {
        return name;
    }
    public String getId() {
        return id;
    }
    @Override
    public String toString() {
        return "Product{" + name + '}';
    }
    public int getWeight() {
        // stuff
```

---

# Simplify your life

```java
import lombok.*;

@Getter
@ToString
@AllArgsConstructor
public class Product {
```
