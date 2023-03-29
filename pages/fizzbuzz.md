---
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

