Https://github.com/tddworks/ClaudeBar

___

The ClaudeBar repository by tddworks is a macOS menu bar application designed to help developers monitor their AI coding assistant usage quotas in real-time.
It is particularly useful for users of Claude Code, GitHub Copilot, Codex, and Gemini who want to avoid hitting rate limits or running out of tokens mid-task.

Key Features 
 * Multi-Provider Support: Tracks quotas for Claude (via Claude CLI), Codex, Gemini, and GitHub Copilot.
 * Live Monitoring: Displays remaining quota percentages directly in the macOS menu bar.
 * Visual Indicators: Uses color-coded status indicators (Green for healthy, Yellow for warning, Red for critical) so you can check your status at a glance.
 * System Notifications: Sends alerts when your quota drops to warning or critical levels.
 * No API Keys Required: For most providers (like Claude), it probes the CLI tools you already have installed rather than requiring separate API authentication.
 * Native Experience: Built with Swift 6 and SwiftUI for a lightweight, native macOS feel.

Technical Profile 
 * Architecture: Follows Clean Architecture/DDD (Domain-Driven Design) principles with a focus on Test-Driven Development (TDD).
 * Requirements: Requires macOS 15.0+ and the relevant CLI tools (e.g., claude CLI) installed on your system.
 * Open Source: The project is open-source and welcomes contributions, maintaining high test coverage as a standard.

Installation 
You can download the latest .dmg or .zip from the GitHub Releases page. Since you are working on projects like localSq and Phoenix Valley, this could be a helpful tool to manage your AI resources while coding.
