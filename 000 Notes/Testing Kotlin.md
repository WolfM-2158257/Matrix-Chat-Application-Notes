# Local Testing ([[AF-UseCase]])
- Make methods in classes public for testing with the `internal` access modifier, and with the `@VisibleForTesting` annotation
- Testing takes place in the `app>src>test>java>com>example>PACKAGETOTESTHERE` directory
- use the `@Test` annotation for methods that are going to test your classes (with `import org.junit.Test `)
```kotlin
import org.junit.Test

class TipCalculatorTests {

   @Test
   fun calculate_20_percent_tip_no_roundup() {
	   val amount = 10.00
	   val tipPercent = 20.00
	   val expectedTip = NumberFormat.getCurrencyInstance().format(2)
	   val actualTip = calculateTip(amount = amount, tipPercent = tipPercent, false)
	   // actual test:
	   assertEquals(expectedTip, actualTip)
	   
   }
}
```
 Assertions:
-   `assertEquals()`
-   `assertNotEquals()`
-   `assertTrue()`
-   `assertFalse()`
-   `assertNull()`
-   `assertNotNull()`
-   `assertThat()`
