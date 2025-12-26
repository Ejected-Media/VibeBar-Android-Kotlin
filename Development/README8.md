To get this running, we need to move from UI design to the Android System Level. Because this sits over other apps (like localSq), we use a Foreground Service. This prevents Android from killing the process when you switch apps.

1. The "FloatingService" (The Engine) 
This Kotlin class handles the WindowManager. It translates the "Mac Style" logic into a persistent Android overlay.

```
class MacOverlayService : Service() {
    private lateinit var windowManager: WindowManager
    private lateinit var composeView: ComposeView

    override fun onCreate() {
        super.onCreate()
        windowManager = getSystemService(WINDOW_SERVICE) as WindowManager

        // 1. Layout Params: This makes it sit on top of everything
        val params = WindowManager.LayoutParams(
            WindowManager.LayoutParams.WRAP_CONTENT,
            WindowManager.LayoutParams.WRAP_CONTENT,
            WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY,
            WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE or WindowManager.LayoutParams.FLAG_LAYOUT_IN_SCREEN,
            PixelFormat.TRANSLUCENT
        ).apply {
            gravity = Gravity.TOP or Gravity.CENTER_HORIZONTAL
            y = 50 // Distance from top
        }

        // 2. The Compose "Bridge"
        composeView = ComposeView(this).apply {
            // Needed for Jetpack Compose to work in a Service
            val lifecycleOwner = MyLifecycleOwner()
            lifecycleOwner.performRestore(null)
            lifecycleOwner.handleLifecycleEvent(Lifecycle.Event.ON_CREATE)
            
            setViewTreeLifecycleOwner(lifecycleOwner)
            setViewTreeSavedStateRegistryOwner(lifecycleOwner)
            
            setContent {
                // This is where our Style Switcher lives!
                FloatingBarContainer(viewModel = OverlayViewModel())
            }
        }

        windowManager.addView(composeView, params)
    }

    override fun onDestroy() {
        super.onDestroy()
        windowManager.removeView(composeView)
    }

    override fun onBind(intent: Intent?) = null
}
```


2. Manifest and Permissions 
Since this is a powerful "Draw over other apps" feature, you must explicitly declare it. Without these, the service will crash immediately.

```
<manifest ...>
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_SPECIAL_USE" />

    <application>
        <service 
            android:name=".MacOverlayService"
            android:foregroundServiceType="specialUse"
            android:exported="false" />
    </application>
</manifest>
```


3. Handling Dragging (The "Physics") 
To make it feel like the Motorola Gametime widget, you want to update the WindowManager position as you drag. Inside your Compose Modifier.pointerInput, you call this:

```
fun updateWindowPos(x: Int, y: Int) {
    params.x = x
    params.y = y
    windowManager.updateViewLayout(composeView, params)
}
```

4. Integration Strategy for your Projects 
 * For Shop Oahu: You can create a "Price Monitor" module in the bar. As you browse your shop in the app, the bar shows the margin or stock level in Classic Mac style.
 * For localSq: Use the Glitch Art theme to display raw GPS NMEA sentences (the raw data strings) as they come in, making the "digital" look feel functional.
 * For Phoenix Valley: A temperature/weather sensor module that uses the Cozy theme when it's cool and switches to Glitch (Red/Hot) when it's over 110°F.

Summary of Assets Created 
 * Themes: Classic Mac (90s), Glitch (Cyber), Girly Pop (Holo), Modern (Sonoma).
 * Interaction: Long-press to switch, drag to move.
 * Backend: Android Foreground Service and WindowManager.

Would you like me to generate a simple "Launcher Activity" code block that checks if the "Draw over other apps" permission is granted and opens the settings if it isn't?
