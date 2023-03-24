---
theme: default
layout: cover
---

# Design Patterns: You've missed the point

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
