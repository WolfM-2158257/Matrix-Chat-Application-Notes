- All the files can be saved to e.g. `app/src/main/java/com/example/ui/theme`
- Colors should be added to `Color.kt`
```kotlin
//Light Theme
val Grey50 = Color(0xFFF8F9FA)
val Grey900 = Color(0xFF202124)
val Grey700 = Color(0xFF5F6368)
val Green50 = Color(0xFFE6F4EA)
val Green100 = Color(0xFFCEEAD6)

//Dark Theme
val White = Color(0xFFFFFFFF)
val Grey100 = Color(0xFFF1F3F4)
val Cyan900 = Color(0xFF007B83)
val Cyan700 = Color(0xFF129EAF)

```
- the `Theme.kt` file holds the information about the theme:
```kotlin
private val LightColorPalette = lightColors(
   background = Green100,
   surface = Green50,
   onSurface = Grey900,
   primary = Grey50,
   onPrimary = Grey900,
   secondary = Grey700
)
private val DarkColorPalette = darkColors(
   background = Cyan900,
   surface = Cyan700,
   onSurface = White,
   primary = Grey900,
   onPrimary = White,
   secondary = Grey100
)

@Composable
fun WoofTheme(darkTheme: Boolean = isSystemInDarkTheme(), content: @Composable () -> Unit) {
   val colors = if (darkTheme) {
       DarkColorPalette
   } else {
       LightColorPalette
   }

   MaterialTheme(
       colors = colors,
       typography = Typography,
       shapes = Shapes,
       content = content
   )
}
```

```kotlin
class MainActivity : ComponentActivity() {
   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
       setContent {
           WoofTheme(darkTheme = false) {
               WoofApp()
           }
       }
   }
}
// using the initialized colors:
LazyColumn(modifier = Modifier.background(MaterialTheme.colors.background))

```
# Reference
- https://developer.android.com/codelabs/basic-android-kotlin-compose-material-theming?continue=https%3A%2F%2Fdeveloper.android.com%2Fcourses%2Fpathways%2Fandroid-basics-compose-unit-3-pathway-3%23codelab-https%3A%2F%2Fdeveloper.android.com%2Fcodelabs%2Fbasic-android-kotlin-compose-material-theming#2
- Icons: https://fonts.google.com/icons?selected=Material+Icons