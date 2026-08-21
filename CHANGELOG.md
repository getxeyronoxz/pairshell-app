# Changelog — PairShell

All notable changes to PairShell and the pairshell-cli host package are documented in this file.

---

## [0.0.1] - 2026-08-21 (Alpha Release)

### Core & Host CLI (pairshell-cli)
- **Windows ConPTY Runtime**: Direct integration with Windows pseudo-console API using PowerShell 7.6.4+ Core runtime (pwsh.exe) with UTF-8 surrogate pairing.
- **Cross-Platform PTY**: Dynamic POSIX login shell resolution (zsh, ash, ish) on macOS and Linux.
- **Tunnel Lifecycle**: Outbound TLS tunneling adapters with lazy provisioning for Cloudflare Quick Tunnels, ngrok, Tailscale Funnel, and Microsoft Dev Tunnels.
- **Cryptographic Pairing**: HMAC-SHA256 challenge verification with 60-second single-use expiry and constant-time token comparison.
- **State Management**: Zero-leak .pairshell/config.json store with automated .gitignore registration.
- **Health Doctor**: Comprehensive pairshell doctor preflight validator for shell binaries, tunnel health, and filesystem permissions.

### Android Application
- **Target SDK Modernization**: Upgraded to minSdk = 30 (Android 11) through 	argetSdk = 36 / compileSdk = 36 (Android 16).
- **Predictive Back Navigation**: Full migration to Flutter PopScope with keyboard dismissal and gesture isolation.
- **Foreground Reconnection Service**: Kotlin PairshellConnectionService foreground service with exponential backoff and replay buffer checkpoint synchronization.
- **Authentication & Privacy**: Firebase Auth (Google & GitHub OAuth) with account privacy isolation (zero device IDs or terminal data recorded).
- **Terminal Rendering**: 24-bit TrueColor ANSI escape sequence parser with terminal accessory bar (Ctrl, Alt, Tab, Esc, navigation arrows).

### Web Documentation (pairshell-web)
- **Astro Static Architecture**: 11-page high-performance documentation hub deployed on Vercel.
- **Complete SEO Suite**: Structured schema.org JSON-LD data, hreflang tags, OpenGraph previews, and automated SEO assertions.
- **Strict Content Claims**: Zero placeholder claims or misleading mockups.
