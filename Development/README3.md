To achieve that premium macOS "Glassmorphism" look on Android, we need to combine a semi-transparent surface, a subtle border, and—where supported—a background blur.

Here is the Jetpack Compose implementation for the floating pill.

1. The Glassmorphism Container 
This component creates the sleek, pill-shaped aesthetic of the macOS menu bar.

```
@Composable
fun MacStyleMenuBar() {
    Surface(
        modifier = Modifier
            .padding(8.dp)
            .wrapContentSize(),
        shape = RoundedCornerShape(24.dp), // Pill shape
        color = Color.White.copy(alpha = 0.15f), // Transparent white
        border = BorderStroke(0.5.dp, Color.White.copy(alpha = 0.3f)) // Thin "retina" border
    ) {
        Row(
            modifier = Modifier
                .padding(horizontal = 16.dp, vertical = 8.dp),
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.spacedBy(12.dp)
        ) {
            // ClaudeBar-style Quota Indicator
            QuotaIndicator(label = "Claude", percent = 0.85f, color = Color(0xFF4CAF50))
            
            VerticalDivider()
            
            // System Status (Example for localSq or Shop Oahu testing)
            StatusIcon(Icons.Default.Dns, "API: OK", Color.Cyan)
            StatusIcon(Icons.Default.SdStorage, "DB: 12MB", Color.White)
        }
    }
}
```

2. Handling the "Floating" Physics 
To make it feel like the Motorola Gametime widget, the user needs to be able to drag it. You can wrap the MacStyleMenuBar in a draggable modifier that updates the WindowManager params:

```
@Composable
fun DraggableOverlay(onDrag: (Float, Float) -> Unit) {
    var offsetX by remember { mutableStateOf(0f) }
    var offsetY by remember { mutableStateOf(0f) }

    Box(
        modifier = Modifier
            .offset { IntOffset(offsetX.roundToInt(), offsetY.roundToInt()) }
            .pointerInput(Unit) {
                detectDragGestures { change, dragAmount ->
                    change.consume()
                    offsetX += dragAmount.x
                    offsetY += dragAmount.y
                    onDrag(offsetX, offsetY) // Sync with WindowManager
                }
            }
    ) {
        MacStyleMenuBar()
    }
}
```

3. Key Aesthetic Details 
 * Background Blur: Android 12 (API 31) introduced RenderEffect. You can apply a blur to the window itself using window.setBackgroundBlurRadius(30). This is what truly gives it the macOS "Vibrant" look.
 * Typography: Use a clean Sans-Serif font (like Inter or Roboto) at a small weight (10sp to 12sp) to mimic the high-density information display of ClaudeBar.
Integrating with your Projects
Since you are working on localSq and Shop Oahu, we could set up "App Hooks." When one of those apps is in the foreground, the bar could automatically change its icons to show specific debug info for that project (e.g., current location coordinates for localSq).
Would you like me to show you how to detect which of your apps is currently in the foreground so the bar can switch its context automatically?
