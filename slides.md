---
theme: default
layout: statement
---

# Design Patterns:
# You've missed the point

---
layout: two-cols
---

# The Book

<img
  class="absolute bottom-2 left-0 w-80"
  src="/img/gamma-1994.jpg"
/>

::right::

<v-clicks>

- very good
- everybody likes it
- maybe not the Singleton
- highly recommend
- 10/10
- very good

</v-clicks>

---
layout: quote
transition: fade
---

# What is a Design Pattern?

> A design pattern is the re-usable form of a solution to a design problem.

— Wikipedia

<v-click>

Solution to a design _problem_

</v-click>

---
layout: quote
---

# What is a _Software_ Design Pattern?

> A **_software_** design pattern is the
> re-usable form of a solution to a **_software_** design problem.

— Previous slide, but with _software_

<v-click>

So we need a _problem_

</v-click>

<!--
Let's see an artist's visualization
of what happens if you don't.
-->

---

# FizzBuzz Enterprise Edition

<v-click>

```java {all|3-21}
public class NoFizzNoBuzzStrategy implements IsEvenlyDivisibleStrategy {
	public boolean isEvenlyDivisible(final int theInteger) {
		if (!NumberIsMultipleOfAnotherNumberVerifier.numberIsMultipleOfAnotherNumber(theInteger,
				NoFizzNoBuzzStrategyConstants.NO_FIZZ_INTEGER_CONSTANT_VALUE)) {
			if (!NumberIsMultipleOfAnotherNumberVerifier.numberIsMultipleOfAnotherNumber(theInteger,
					NoFizzNoBuzzStrategyConstants.NO_BUZZ_INTEGER_CONSTANT_VALUE)) {
				return true;
			} else {
				return false;
			}
		} else if (!NumberIsMultipleOfAnotherNumberVerifier.numberIsMultipleOfAnotherNumber(theInteger,
				NoFizzNoBuzzStrategyConstants.NO_BUZZ_INTEGER_CONSTANT_VALUE)) {
			if (!NumberIsMultipleOfAnotherNumberVerifier.numberIsMultipleOfAnotherNumber(theInteger,
					NoFizzNoBuzzStrategyConstants.NO_FIZZ_INTEGER_CONSTANT_VALUE)) {
				return true;
			} else {
				return false;
			}
		} else {
			return false;
		}
	}
}
```

</v-click>

---

# FizzBuzz Enterprise Edition

```java {3}
public class NoFizzNoBuzzStrategy implements IsEvenlyDivisibleStrategy {
	public boolean isEvenlyDivisible(final int theInteger) {
		return theInteger % 15 != 0;
	}
}
```

---

# FizzBuzz Enterprise Edition

<v-click>

```java
public class FizzBuzzOutputGenerationContextVisitorFactory
```

</v-click>

<v-click>

```java
public interface StringStringReturner
```

</v-click>

---
layout: two-cols
---

# Another Book

<img
  class="absolute bottom-2 left-0 w-80"
  src="/img/beck-2004.jpg"
/>

::right::

<v-clicks>

- also very good
- don't do too much upfront
- many useful ideas
- highly recommend
- 10/10

</v-clicks>

---
layout: statement
---

## Are they mutually exclusive?

---
layout: two-cols
---

# Another one

<img
  class="absolute bottom-2 left-0 w-72"
  src="/img/kerievsky-2004.jpg"
/>

::right::

<v-clicks>

- simple design upfront
- refactor to patterns
- but only when you see the _problem_

</v-clicks>

---

# Example

```java {all|2-22}
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

# Example

```java
public static String exportFull(Account account) {
    return XML_HEADER + account.fullXml();
}
```

---

# Tests first

<v-clicks>

- Approval tests
- Only the external interface

</v-clicks>

<!--
a.k.a. snapshot tests
-->

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

---

# We've got our domain expert

```java
@AllArgsConstructor
public class Ledger {
    private final List<Order> orders;

    public double getTaxInDollars() {
        return orders.stream().mapToDouble(Order::getTaxInDollars).sum();
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
