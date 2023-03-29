---
transition: fade
---

# FizzBuzz

```py
fizzbuzz(1) == '1'
fizzbuzz(2) == '2'
fizzbuzz(3) == 'Fizz'
fizzbuzz(4) == '4'
fizzbuzz(5) == 'Buzz'
fizzbuzz(6) == 'Fizz'
...
fizzbuzz(14) == '14'
fizzbuzz(15) == 'FizzBuzz'
```

---
transition: fade
---

# FizzBuzz Enterprise Edition

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

---
transition: fade
---

# FizzBuzz Enterprise Edition

```java {3}
public class NoFizzNoBuzzStrategy implements IsEvenlyDivisibleStrategy {
	public boolean isEvenlyDivisible(final int theInteger) {
		return theInteger % 15 != 0;
	}
}
```
