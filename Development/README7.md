To tie all these aesthetics together, we need a high-end Interaction Layer. On Android, since this is a floating widget, a simple tap usually toggles information, while a long-press is the perfect gesture to trigger a "Style Switcher" (much like changing your wallpaper on a phone).

Here is how we can implement the Radial/Theme Selector and the logic to manage these four distinct styles.

1. The Theme Orchestrator 
We’ll use a ViewModel to hold the state. This ensures that whether you are working in localSq or Shop Oahu, the bar remembers which "vibe" you’ve selected.

```
enum class WidgetStyle {
    CLASSIC_MAC, GLITCH, GIRLY_POP, MODERN_GLASS
}

class OverlayViewModel : ViewModel() {
    var currentStyle by mutableStateOf(WidgetStyle.MODERN_GLASS)
    
    fun toggleStyle(style: WidgetStyle) {
        currentStyle = style
    }
}
```


2. The Interaction: Long-Press for Theme Menu 
We can use a Box with a combinedClickable modifier. When you long-press the floating bar, it will show a small popup menu with icons representing each aesthetic.

```
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun FloatingBarContainer(viewModel: OverlayViewModel) {
    var showMenu by remember { mutableStateOf(false) }

    Box(
        modifier = Modifier
            .combinedClickable(
                onClick = { /* Toggle collapsed/expanded info */ },
                onLongClick = { showMenu = true }
            )
    ) {
        // Render the active aesthetic
        when (viewModel.currentStyle) {
            WidgetStyle.CLASSIC_MAC -> ClassicMacContainer { BarContent() }
            WidgetStyle.GLITCH -> GlitchContainer { BarContent() }
            WidgetStyle.GIRLY_POP -> GirlyPopContainer { BarContent() }
            WidgetStyle.MODERN_GLASS -> MacStyleMenuBar()
        }

        // Theme Switcher Popup
        if (showMenu) {
            ThemePopup(
                onStyleSelected = {
                    viewModel.toggleStyle(it)
                    showMenu = false
                },
                onDismiss = { showMenu = false }
            )
        }
    }
}
```


3. Visualizing the Project Layers 
Since this app functions as an overlay, it operates on a different layer than your standard activities.

4. Why this matters for your 2025 Projects 
 * Phoenix Valley: You could set the Glitch Art theme to trigger automatically if the app detects a "Heat Warning" or high server latency in the valley's infrastructure.
 * Shop Oahu: Use the Girly Pop or Modern Glass theme to match the vibrant, aesthetic-heavy retail environment of the island.
 * localSq: Use the Classic MacOS theme for a "Data-Only" mode that stays out of the way while you're mapping local coordinates.

5. Final Touch: The "Cozy" Aesthetic 
Since we haven't detailed the Cozy style yet, we can define it as the "Neutral" option. It uses Warm Creams (#FFFDD0), Sage Greens, and Squircle shapes (somewhere between a square and a circle) with a very soft "inner glow" rather than a hard shadow.
Would you like me to provide the full Service code now, so you can actually run this as a floating window on an Android emulator or device?
