Here is a structured README.md tailored for your project. This will help you organize the repository and keep track of the specific aesthetics and integrations for localSq, Shop Oahu, and Phoenix Valley.

VibeBar Android 📱✨ 
VibeBar is a themeable, floating utility overlay for Android inspired by the ClaudeBar macOS app. It provides real-time system monitoring, AI quota tracking, and project-specific debug data through a highly customizable "Aesthetic Engine."

🎨 Aesthetic Modules 
This project moves beyond standard Material Design by offering four distinct "Vibes":
 * MacOS Classic: A pixel-perfect recreation of the System 7/8/9 "Platinum" interface.
 * Glitch Art: High-contrast neon aesthetics with chromatic aberration and scanlines (Optimized for Phoenix sunlight).
 * Girly Pop: Holographic gradients, Y2K "shimmer" animations, and rounded "bubble" geometry.
 * Modern Glass: A sleek, semi-transparent macOS Sonoma-inspired glassmorphism look.

🛠 Project Integrations 
VibeBar is designed to act as a "Developer HUD" for current active projects:
 * localSq: Real-time GPS/NMEA coordinate monitoring via Broadcast signals.
 * Shop Oahu: Inventory and pricing margin trackers for live retail testing.
 * Phoenix Valley: Environmental sensors and API latency monitors for regional infrastructure.

🚀 Getting Started

1. Permissions 
VibeBar requires the SYSTEM_ALERT_WINDOW permission. Upon first launch, the app will redirect you to:
Settings > Apps > Special App Access > Display over other apps.

2. Development Setup 
 * Clone the repository.
 * Open in Android Studio Ladybug (or newer).
 * Ensure your device/emulator is running Android 12 (API 31) or higher to support RenderEffect blurs for the Modern Glass theme.

3. File Map 
 * /service: Core WindowManager logic and ForegroundService lifecycle.
 * /ui/themes: Individual Composable functions for each aesthetic (Classic, Glitch, etc.).
 * /ui/components: Reusable status pills and animated icons.
 * /receiver: Broadcast logic for project-to-overlay communication.

One final tip for your setup: 
Since you’re using ClaudeBar as inspiration, you might find it helpful to set up a small Python script (running on your dev machine) that pings your phone's IP with your Claude/Copilot quota via the Broadcast system we built. That way, the mobile VibeBar stays perfectly synced with your desktop AI usage!

Would you like me to provide that quick Python "Quota-to-Android" bridge script to complete the loop?
