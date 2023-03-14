> [!note]
> The code above uses the `thingUnderTest_TriggerOfTest_ResultOfTest` format to name the test function name:
	- thingUnderTest = gameViewModel
	- TriggerOfTest = CorrectWordGuessed
	- ResultOfTest = ScoreUpdatedAndErrorFlagUnset



# Local Testing ([[AF-UseCase]])
- Make methods in classes public for testing with the `internal` access modifier, and with the `@VisibleForTesting` annotation
- Testing takes place in the `app>src>test` directory
- use the `@Test` annotation for methods that are going to test your classes (with `import org.junit.Test `)
```kotlin
// app>src>test>java>com>tiptime>TipCalculatorTests.kt
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
Run tests:
![[Pasted image 20230310122830.png]]

# Instrumentation Tests (front-end testing)
- Takes place in `app>src>androidTest`
```kotlin
// app>src>androidTest>java>com>tiptime>TipUITests.kt
import androidx.compose.ui.test.junit4.createComposeRule
import org.junit.Rule

class TipUITests {

   @get:Rule
   val composeTestRule = createComposeRule() // used to find nodes

   @Test
	fun calculate_20_percent_tip() {
		composeTestRule.setContent {
			TipTimeTheme {
				Surface (modifier = Modifier.fillMaxSize()){
					TipTimeScreen()
				}
			}
		}
		// find some component, and set input
		composeTestRule.onNodeWithText("Bill Amount")
		  .performTextInput("10")
		composeTestRule.onNodeWithText("Tip (%)").performTextInput("20")
		val expectedTip = NumberFormat.getCurrencyInstance().format(2)
		// check if result is correct
		composeTestRule.onNodeWithText("Tip Amount: $expectedTip").assertExists(
		  "No node with this text was found."
		)
	}
}
```

# Testing Dependencies
```kotlin
plugins {
    ...
}

android {
    ...
}

dependencies {
    ...
    testImplementation 'junit:junit:4.13.2'
}
```

# Types of tests
- Success Test: check for correct successful behavior
- Error Test: check for correct unsuccessful behavior
- Boundary Test:  check if everything is set correctly after some behavior