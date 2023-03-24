---
theme: default
layout: statement
---

# Design Patterns:
# You've missed the point

<v-click>

## Blazej Sewera

</v-click>

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

# Taxes: don't get this one wrong!

```java {all|3|6,8,11,13|5|10|all}
public class TaxCalculator {
    public static double calculateAddedTax(Collection<Order> orders) {
        double tax = 0.0;
        for (Order order : orders) {
            if (order.date().before(DateUtil.fromIsoDate("2018-01-01T00:00Z")))
                tax += 10;
            else
                tax += 20;
            for (Product product : order.products())
                if (product.isEvent())
                    tax += product.getPrice().getAmountInCurrency("USD") * 0.25;
                else
                    tax += product.getPrice().getAmountInCurrency("USD") * 0.175;
        }
        return tax;
    }
}
```

<span v-click>We need to get it under test</span><b v-click> now.</b>

<!--
1. it can be very expensive
2. here we declare it
3. here we modify it
4. there is a tax change
5. for events tax is different
-->

---

# Testing taxes

```java {all|1-4|5-7|9-10|12-13|16-19}
private void testTaxForOrder(
        boolean isEvent,
        Date date,
        double expectedTax) {
    // given
    var price = 100.00;
    var order = buildOrder(isEvent, date, price);

    // when
    var actual = TaxCalculator.calculateAddedTax(List.of(order));

    // then
    assertThat(actual).isEqualTo(expectedTaxFor100Price);
}

@Test
void testTax_RegularOrderBeforeTaxChange() {
  testTaxForOrder(NOT_EVENT, DATE_BEFORE_TAX_CHANGE, 27.5);
}
```

<v-click>

Check coverage

</v-click>

---

# Less scary taxes

```java {all|1-7|6|10,14|18-20}
abstract class Product {
    Money price;

    abstract double taxRate();

    Money tax() { return price.timesRate(taxRate()); }
}

class RegularProduct {
    double taxRate() { return 0.175; }
}

class StoreEvent {
    double taxRate() { return 0.25; }
}

class Order {
    Money tax() {
        return initialTax() + products.stream().map(Product::tax).sum();
    }
}
```

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

---
layout: statement
---

## Towards a better future!

<v-click>

### or at least a Composite

</v-click>

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

---
layout: statement
---

## That's a little bit better

<v-click>

### can it be even better?

</v-click>

---
layout: statement
---

## Towards a more declarative future

<v-click>

### or at least a Builder

</v-click>

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

---
layout: statement
---

<div class="flex">
    <img
    class="w-100 mx-auto"
    src="/img/its-all-coming-together.jpg"
    />
</div>

---

# It's all coming together

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

# It's all came together

```java
public static String exportFull(Account account) {
    return XML_HEADER + account.fullXml();
}
```

---
layout: statement
---

[www.sewera.dev](https://www.sewera.dev)
