---
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
