# PairShell

<div align="center">

**The Agentic Coding Environment (ACE) in your pocket.**

[![Official Website](https://img.shields.io/badge/website-pairshell.vercel.app-39e59a?style=flat-square)](https://pairshell.vercel.app)
[![Host CLI](https://img.shields.io/npm/v/pairshell-cli?label=pairshell-cli&color=39e59a&style=flat-square)](https://www.npmjs.com/package/pairshell-cli)
[![Target Android](https://img.shields.io/badge/Android-11%20to%2016%20(API%2030--36)-black?style=flat-square&logo=android)](https://pairshell.vercel.app/download)
[![Developer](https://img.shields.io/badge/developer-Xeyronox-39e59a?style=flat-square)](https://instagram.com/xeyronox)
[![License](https://img.shields.io/badge/license-Proprietary-blue?style=flat-square)](LICENSE)

</div>

---

## What is PairShell?

**PairShell** is a low-latency Android remote terminal designed for controlling coding agents (such as Codex CLI and OpenCode) and host-installed development CLI workflows directly from your Android phone or tablet.

The real pseudo-terminal (PTY) runs on your computer, workstation, or remote VPS. Pair effortlessly via QR code and connect over a user-selected TLS WebSocket tunnel with **zero inbound open ports**.

`
┌─────────────────┐       Outbound TLS WebSocket       ┌──────────────────────┐       Local PTY Engine       ┌─────────────────────┐
│  Android Client │ <────────────────────────────────> │ Relay / TLS Tunnel   │ <──────────────────────────> │ PairShell Host CLI  │
│  (Flutter App)  │    (Cloudflare / ngrok / Tailscale)│ (Zero Inbound Ports) │     (PowerShell 7 / Unix)    │ (Desktop / VPS PTY) │
└─────────────────┘                                    └──────────────────────┘                              └─────────────────────┘
`

---

## Key Highlights

- **Native Host Fidelity**: Real interactive PTY input/output with ANSI 24-bit TrueColor rendering on your Android device.
- **Single-Use Cryptographic Pairing**: High-entropy HMAC-SHA256 challenge pairing with 60-second automatic token expiration and timing-safe verification.
- **Zero Inbound Ports**: Default outbound-only Cloudflare Quick Tunnel auto-provisions on first run. Also supports ngrok, Tailscale Funnel, and Microsoft Dev Tunnels.
- **Hardware & Keyboard Support**: Full accessory row with modifier keys (Ctrl, Alt, Esc, Tab, directional arrows) and predictive back navigation.
- **Persistent Reconnection**: Android Kotlin foreground service maintains session continuity across network handoffs and device sleep.
- **Strict Privacy Invariant**: Zero terminal output, commands, repository paths, or private credentials are ever logged or exported to telemetry.

---

## Quick Start (Host Setup)

### 1. Install the CLI Globally

Install the official host CLI via npm:

`ash
npm install --global pairshell-cli
`

### 2. Start the Host Daemon

Spawn the background daemon, open an encrypted tunnel, and display your pairing QR:

`ash
pairshell start
`

*Cloudflare tunnel dependencies auto-install and verify cryptographically on first run.*

### 3. Pair with Android

Open the PairShell Android app, tap **Add workspace**, and scan the QR code displayed in your terminal, or copy and paste the displayed pairing link.

---

## CLI Command Matrix

| Command | Category | Description |
| :--- | :--- | :--- |
| pairshell start | Lifecycle | Start background host daemon, attach PTY, open tunnel, and print pairing QR |
| pairshell stop | Lifecycle | Gracefully terminate daemon, pseudo-terminals, and child tunnel processes |
| pairshell status | Diagnostics | Show host PID, uptime, tunnel provider health, and authenticated device state |
| pairshell qr | Security | Rotate pairing secret and print a fresh 60s single-use HMAC challenge QR |
| pairshell reload | Config | Hot-swap tunnel provider or shell preference on the fly without dropping session |
| pairshell doctor | Preflight | Audit system runtime: ConPTY, PowerShell 7.6.4+ Core, Unix shells, and network |

---

## Supported Tunnel Providers

PairShell lets you bring your own route:

1. **Cloudflare Quick Tunnel** (--tunnel cloudflare, default): Zero-config, account-free, outbound-only tunnel.
2. **ngrok** (--tunnel ngrok): Native agent relay with your personal authtoken.
3. **Tailscale Funnel** (--tunnel tailscale): Secure tailnet endpoint relay.
4. **Microsoft Dev Tunnels** (--tunnel devtunnel): Azure-authenticated developer tunnel.

Switch providers anytime:

`ash
pairshell reload --tunnel tailscale
`

---

## Security Invariants

- **Host Isolation**: Repository files, environment variables, and PTY processes stay 100% local on your host computer.
- **Timing-Safe HMAC**: Pairing tokens use constant-time comparisons to eliminate timing side-channel attacks.
- **Hashed Device Tokens**: Only salted SHA-256 hashes of authorized Android device tokens are stored host-side.
- **Zero Logging Policy**: Strict architectural invariant prohibiting the recording or exporting of terminal content.

---

## License & Support

Developed and maintained by **Xeyronox** ([@xeyronox](https://instagram.com/xeyronox)).  
Official Distribution: [https://github.com/getxeyronoxz/pairshell-app](https://github.com/getxeyronoxz/pairshell-app)  
Website: [https://pairshell.vercel.app](https://pairshell.vercel.app)  
Email: [xeyronox@outlook.com](mailto:xeyronox@outlook.com)  

Copyright © 2026 Xeyronox. All rights reserved.
