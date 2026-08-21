# PairShell

> **Android remote terminal for host-side coding agents and CLI workflows.**

Official Website: [https://pairshell.vercel.app](https://pairshell.vercel.app)  
NPM Package: [pairshell-cli](https://www.npmjs.com/package/pairshell-cli)  
Developer: **Xeyronox** ([@xeyronox](https://instagram.com/xeyronox))

---

## 1. Overview

**PairShell** connects your Android phone directly to a real pseudo-terminal (PTY) running on your computer, workstation, or remote VPS. Your repository, development tools, environment variables, credentials, and coding agents (such as Codex CLI or OpenCode) remain entirely on your host machine.

The Android app acts as a low-latency, high-fidelity control surface, streaming ANSI TrueColor output and sending interactive keyboard input with full modifier support (Ctrl, Alt, Tab, Esc, Arrow keys).

## 2. Key Architecture & Invariants

1. **Local-First Pseudo-Terminal**: Commands and tools run natively on your machine inside a real PTY. Windows uses verified PowerShell 7.6.4+ Core ConPTY; macOS and Linux use native POSIX login shells.
2. **Cryptographic Single-Use Pairing**: Pairing QR codes contain a high-entropy HMAC challenge that expires in 60 seconds. Constant-time comparisons protect against timing attacks.
3. **Strict Privacy Invariant**: Zero terminal content, commands, filesystem paths, or credentials are ever recorded in telemetry or remote storage.
4. **Hashed Bearer Credentials**: Paired Android devices receive revocable bearer tokens stored in Android EncryptedSharedPreferences / KeyStore, with SHA-256 hashes preserved host-side.
5. **Foreground Service Connection**: Android utilizes a dedicated foreground service to maintain session continuity during network transitions and prevent background termination.
6. **Zero Inbound Open Ports**: Default outbound-only Cloudflare Quick Tunnels require no port forwarding, public IP, or account setup.

## 3. Quick Start (Host)

Install the host CLI globally via npm:

`ash
npm install --global pairshell-cli
`

Start the host daemon and display a pairing QR:

`ash
pairshell start
`

Scan the QR code from the PairShell Android app to pair immediately.

### Available CLI Commands

| Command | Purpose |
| :--- | :--- |
| pairshell start | Spawn local host daemon, attach PTY, open tunnel, and print pairing QR |
| pairshell stop | Gracefully terminate daemon, terminals, and tunnel processes |
| pairshell status | Show host PID, uptime, tunnel provider health, and authenticated devices |
| pairshell qr | Rotate pairing token and print a fresh 60s HMAC challenge QR |
| pairshell reload | Hot-swap tunnel provider or shell preference without dropping session |
| pairshell doctor | Preflight audit of ConPTY, PowerShell runtime, Unix shells, and network |

## 4. Supported Tunnel Providers

- **Cloudflare Quick Tunnel** (Default): Account-free, zero-config, outbound-only tunnel. The official platform binary is lazily cached and cryptographically verified before execution.
- **ngrok**: Native agent relay with your personal authtoken (--tunnel ngrok).
- **Tailscale Funnel**: Secure tailnet endpoint relay (--tunnel tailscale).
- **Microsoft Dev Tunnels**: Azure-authenticated developer tunnel (--tunnel devtunnel).

## 5. Security & Vulnerability Reporting

Security is a primary design goal. If you discover a potential vulnerability, please email xeyronox@outlook.com with reproducible details. Never include live session tokens or sensitive infrastructure credentials in public bug reports.

## 6. License

Copyright © 2026 Xeyronox. All rights reserved.  
Proprietary pre-release developer software.
