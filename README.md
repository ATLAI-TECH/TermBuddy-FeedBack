<p align="center">
  <img src="images/logo.png" alt="TermBuddy Logo" width="160">
</p>

<h1 align="center">TermBuddy</h1>
<h3 align="center">Your Terminal, Reimagined as a Chat</h3>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/iOS-17.0%2B-blue?logo=apple" alt="iOS 17+"></a>
  <a href="#"><img src="https://img.shields.io/badge/macOS-14.0%2B-blue?logo=apple" alt="macOS 14+"></a>
  <a href="#"><img src="https://img.shields.io/badge/License-Proprietary-lightgrey" alt="License"></a>
</p>

<p align="center">
  <b>Manage remote servers like messaging a friend.</b><br>
  Commands become messages. Output becomes replies. Your terminal becomes a Buddy.
</p>

<p align="center">
  <img src="images/hero.png" alt="TermBuddy Hero" width="280">
  &nbsp;&nbsp;
  <img src="images/feature_chat.png" alt="Chat Interface" width="280">
  &nbsp;&nbsp;
  <img src="images/feature_tasks.png" alt="AI Tasks" width="280">
</p>

---

## Table of Contents

- [What is TermBuddy?](#what-is-termbuddy)
- [Key Features](#key-features)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Adding Your First Server](#adding-your-first-server)
  - [Creating a Buddy](#creating-a-buddy)
  - [Sending Commands](#sending-commands)
- [Buddy Types](#buddy-types)
  - [Terminal Buddy](#terminal-buddy)
  - [Claude Code AI Buddy](#claude-code-ai-buddy)
- [File Browser](#file-browser)
- [Server Management](#server-management)
- [Push Notifications](#push-notifications)
- [Security Model](#security-model)
- [Settings & Customization](#settings--customization)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Support](#support)

---

## What is TermBuddy?

TermBuddy is a native macOS and iOS app that transforms how you interact with remote servers. Instead of staring at a cold, stateless terminal window, each server session becomes a **"Buddy"** — a persistent, chat-style conversation where:

- **Commands** are sent as chat messages
- **Output** appears as reply bubbles
- **History** is preserved across restarts
- **AI assistants** can work right alongside you in the same interface

Whether you're a developer managing production servers, a DevOps engineer wrangling multiple environments, or a hobbyist maintaining a home lab — TermBuddy makes server management feel natural and efficient.

---

## Key Features

### 💬 Chat-Style Terminal Interface
Every terminal session looks and feels like a messaging app. Input commands on the right, see output on the left. No more walls of undifferentiated text — each exchange is clearly separated and timestamped. Scroll back through your entire history at any time.

### 🤖 Built-in Claude Code AI Assistant
Create an AI Buddy powered by [Claude Code](https://claude.ai/code) (Anthropic), OpenAI Codex, or Google Gemini. Your AI assistant:
- Reads and writes files on the server
- Runs shell commands
- Streams responses in real-time with full Markdown rendering
- Tracks multi-step plans with a visual progress indicator
- Shows exactly which files and commands it's touching (full transparency)

You supply your own API key — TermBuddy never sees or stores it on any third-party server.

### 🖥️ Native Terminal Emulation
Need raw terminal power? Every Buddy can be opened as a full-featured terminal window powered by **SwiftTerm** — complete ANSI color support, proper PTY handling, resize events, and keyboard shortcuts. No compromises.

### 🔐 Encrypted by Default
All traffic travels through your existing **SSH connection** (port 22). TermBuddy's lightweight server component binds only to `localhost` on your remote machine — it is never exposed to the internet. No additional ports to open, no complex firewall rules.

Alternative **Direct (TLS) mode** is available for advanced setups, with certificate fingerprint pinning for extra security.

### 🌐 Multi-Server, Unified View
Connect to as many servers as you want — production, staging, dev, home lab. All your Buddies from all your servers appear in one unified list. Filter by server, search by name, and see unread message counts at a glance.

### ⚡ Zero-Config Auto-Deployment
Enter your SSH credentials and tap **Connect**. TermBuddy automatically:
1. Detects whether its server component is installed
2. Downloads the correct binary for your server's OS/architecture
3. Installs and starts the service

No SSH-ing in manually, no running scripts, no reading docs.

### 📁 Remote File Browser
Browse your server's file system without leaving the app. Preview text files, configuration files, and logs inline with syntax highlighting. Delete files with confirmation. Toggle hidden files on/off.

### 📶 Offline-First with Instant Load
All message history is cached locally in SQLite. The app loads instantly even with no network connection. Messages sync automatically when connectivity is restored.

### 🔔 Real-Time Push Notifications
Get notified the moment a long-running command completes or an AI task finishes — even when the app is in the background. Notifications are delivered via Server-Sent Events (SSE), not polling, so they arrive instantly.

---

## Getting Started

### Requirements

**Client (your device):**
- iPhone: iOS 17.0 or later
- Mac: macOS 14.0 (Sonoma) or later

**Server (your remote machine):**
- Linux: Ubuntu 18.04+, Debian 9+, CentOS 7+, or any modern distro
- macOS: 12.0 (Monterey) or later
- SSH access enabled (port 22, or a custom port)
- For AI Buddies: Node.js 18+ (to install Claude Code CLI)

---

### Adding Your First Server

1. Open TermBuddy and tap the **Servers** tab (grid icon)
2. Tap the **+** (Add Server) button
3. Enter your server's **IP address or hostname**
   - Tip: If your hostname contains underscores (e.g., `my_server.local`), use the IP address instead — underscores are technically invalid in DNS hostnames and may cause connection failures
   - For local testing, tap **"Use This Computer (127.0.0.1)"**
4. Enter your **SSH username and password**, or select an SSH key file
   - Credentials are stored securely in the system **Keychain** — never in plain text
5. Tap **Connect**

TermBuddy will:
- Resolve DNS and verify SSH reachability
- Authenticate with your credentials
- Detect whether the TermBuddy server component is already installed
- If not installed: automatically download and deploy it for your server's OS and CPU architecture
- Confirm the server is running and healthy

6. Give your server a **name, avatar color**, and tap **Done**

> **Recommended:** For servers not on your local network, use [Tailscale](https://tailscale.com) or another VPN to create a private network. This avoids exposing SSH to the public internet.

---

### Creating a Buddy

A **Buddy** is a persistent session on a server. Think of it as a dedicated chat thread for a specific task or working directory.

1. Tap the **+** button (or press `⌘T` on Mac) in the Buddies/Chats view
2. **Select a server** from your connected servers
3. **Choose a working directory** (or leave blank for the home directory `~`)
4. **Select a Buddy type:**
   - **Terminal** — a full shell session
   - **Claude Code** — AI coding assistant (requires Claude Code CLI on server)
   - **Codex** / **Gemini** — alternative AI engines
5. Give your Buddy a **name, icon, and color**
6. Tap **Create**

Your new Buddy appears in the Chats list, ready to use.

---

### Sending Commands

- Type any shell command in the input bar at the bottom and tap **Send** (or press Return)
- The command appears as a blue message bubble on the right
- Output appears as dark reply bubbles on the left
- For AI Buddies, type a natural language request (e.g., *"Find all TODO comments in the project"* or *"Fix the build error in main.go"*)

**Toolbar actions inside a Buddy:**
| Button | Action |
|--------|--------|
| `+` (bubble) | Start a new conversation (clears visible history, history is still saved) |
| Clock icon | View past conversation history |
| Terminal icon | Open a full native terminal window for this Buddy |
| Folder icon | Open the remote file browser for this server |

---

## Buddy Types

### Terminal Buddy

A Terminal Buddy is a persistent PTY (pseudo-terminal) shell session on your server. It behaves exactly like an SSH terminal but displayed in a chat UI.

**Key behaviors:**
- The shell session persists even if you close the app — long-running processes keep running
- Reconnects automatically when you reopen the Buddy
- Supports full ANSI color codes, cursor movement, and interactive programs (vim, htop, etc.) via the **Open Terminal** button
- Output is captured and stored as searchable chat history

**When to use:** System administration tasks, running scripts, monitoring logs, interactive program execution.

---

### Claude Code AI Buddy

A Claude Code Buddy runs the [Claude Code CLI](https://claude.ai/code) on your server, connected to Anthropic's Claude model via your API key. The AI has access to:
- The full file system within the working directory you selected
- Shell command execution
- File reading, writing, and creation

**Setting up Claude Code:**
1. Install Claude Code on your server:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
   (Requires Node.js 18+)
2. In TermBuddy, go to **Server Settings → AI Tools** and enter your **Anthropic API key**
3. Create a new Buddy and select **Claude Code** as the type

**AI response display:**
- Responses stream in real-time as Markdown-rendered text
- File read/write and bash tool calls are shown as collapsible activity panels so you always know what the AI is doing
- Multi-step plans are shown with a progress checklist
- Token usage statistics can be enabled in Settings

**When to use:** Writing and editing code, debugging errors, exploring an unfamiliar codebase, automating repetitive tasks, generating configuration files.

---

## File Browser

Access the remote file browser by tapping the **Folder** icon in any Buddy's toolbar, or from the **Server Details** screen.

**Features:**
- Navigate directories with breadcrumb trail
- Tap any folder to enter it, tap **↑** to go up one level
- Tap any file to preview it (text files shown with syntax highlighting)
- Toggle hidden files (dotfiles) with the eye icon
- **Delete** a file with the trash icon in the preview panel
- **Copy** file contents to clipboard

**Keyboard shortcuts (Mac):**
- `⌘+` — Zoom in (larger file list text)
- `⌘-` — Zoom out
- `⌘0` — Reset zoom

---

## Server Management

### Viewing Server Status

The **Servers** tab shows all your servers with their current status:
- 🟢 **Online** — Connected and healthy
- 🔴 **Offline** — Unreachable or server component not running
- ⚙️ **Not Installed** — TermBuddy server component needs to be deployed

Tap **Refresh** to manually check all servers. Status is also checked automatically on app launch.

### Updating the Server Component

When a new version of the TermBuddy server binary is available:
1. Go to the **Servers** tab
2. Tap **Check for Updates**
3. If an update is available, tap **Update** next to the server

The update is downloaded and installed automatically — no manual steps required.

### Removing a Server

Long-press (or right-click on Mac) a server → **Delete**. You can choose to:
- **Remove from app only** — Keeps the TermBuddy server component installed on the remote machine
- **Remove completely** — Also uninstalls the TermBuddy server component from the remote machine

---

## Push Notifications

TermBuddy can notify you when a command or AI task completes, even when the app is backgrounded.

**To enable:**
1. Go to **Settings → Notifications**
2. Enable **Push Notifications** globally
3. Enable per-server under **Settings → Notifications → [Server Name] Push**

Notifications are delivered via **Server-Sent Events (SSE)** — a persistent connection from your device to the TermBuddy server component. This means near-instant delivery with no polling delay.

---

## Security Model

TermBuddy is designed with a **"no trust required"** security philosophy:

| Aspect | How TermBuddy handles it |
|--------|--------------------------|
| **Credentials** | Stored in system Keychain only. Never sent to any TermBuddy or third-party server. |
| **Network traffic** | Travels through your SSH connection (port 22) or TLS with certificate pinning. End-to-end encrypted. |
| **Server exposure** | TermBuddy's server component binds to `127.0.0.1` only. Never exposed to the public internet. |
| **AI API keys** | Stored on your own server, in your server's environment. TermBuddy app never sees them. |
| **Data relay** | There is no TermBuddy cloud. Your device connects directly to your server. Zero intermediaries. |
| **Server binary** | The server component runs under your own user account with your own permissions. No root required. |

---

## Settings & Customization

### Appearance
- **Theme:** Light, Dark, or Auto (follows system)
- **Accent Color:** Choose from a palette of colors for UI highlights
- **Font:** Select your preferred UI font

### Terminal
- **Color Scheme:** Choose from multiple terminal color themes
- **Font Size:** Adjust terminal text size
- **Font Family:** Select a monospace font for the terminal

### Notifications
- Enable/disable notifications globally
- Toggle notification sounds
- Enable/disable per-server push notifications independently

### General
- **Language:** English, Chinese (Simplified), Spanish, French, German
- **Logging Level:** Adjust diagnostic log verbosity (for troubleshooting)

### Subscription
- View your trial or subscription status
- Restore previous purchases

---

## Troubleshooting

### Cannot connect to server

**Symptom:** "Cannot connect to [host]:[port]" or timeout on the setup screen.

**Steps:**
1. Verify the server IP address or hostname is correct
2. Confirm SSH is enabled on the server (`sudo systemctl status sshd`)
3. Check that port 22 (or your custom SSH port) is not blocked by a firewall
4. If using a hostname with underscores (e.g., `my_server`), try using the IP address instead — underscores are not valid in DNS hostnames and may cause resolution failures
5. If the server is on a remote network, ensure you're either on a VPN or the server's SSH port is reachable from your current network

---

### Authentication failed

**Symptom:** "Authentication failed" error during setup.

**Steps:**
1. Double-check your username and password
2. If using an SSH key: verify the key file path is correct, and enter the passphrase if the key is encrypted
3. Verify the user account exists on the server: `id your-username`
4. Check SSH server logs on the remote machine: `sudo journalctl -u sshd -n 50`

---

### Server shows "Offline" after setup

**Symptom:** Setup succeeded but the server shows as Offline in the Servers list.

**Steps:**
1. Tap the server → **Check Server Status** to see the specific error
2. SSH into your server manually and check if the process is running:
   ```bash
   ps aux | grep termbuddy
   ```
3. If it's not running, look for the TermBuddy server binary in `~/.termbuddy/` and start it manually to see any error output:
   ```bash
   ~/.termbuddy/termbuddy-server
   ```
4. Check that the port (default: 8765) is not already in use:
   ```bash
   lsof -i :8765
   ```
5. Try **Update Server** from the Servers tab to reinstall the latest server binary

---

### Claude Code AI Buddy not working

**Symptom:** AI Buddy shows an error or Claude Code is not detected.

**Steps:**
1. Verify Claude Code is installed on the **server** (not just your local machine):
   ```bash
   which claude
   claude --version
   ```
2. If not installed, run on the server:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
   (Requires Node.js 18+. Check with `node --version`)
3. Go to **Server Settings → AI Tools** and confirm your Anthropic API key is entered correctly
4. Verify the API key is valid at [console.anthropic.com](https://console.anthropic.com)

---

### Messages not loading / blank chat

**Symptom:** Buddy opens but shows no messages or a loading spinner indefinitely.

**Steps:**
1. Pull to refresh in the chat view
2. Check that the server is Online (Servers tab)
3. Go to **Servers tab → [Server] → Clear Cache**, then reopen the Buddy
4. If the problem persists, delete and recreate the Buddy

---

### App crashes or unexpected behavior

1. Go to **Settings → General → Logging Level** and set it to **Debug**
2. Reproduce the issue
3. Go to **Settings → Help → View Logs** and copy the log
4. [Open a bug report](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues/new?labels=bug&template=bug_report.md) and paste the log

---

## FAQ

<details>
<summary><b>Does TermBuddy store my SSH credentials on any server?</b></summary>
<br>
No. All credentials (passwords, SSH key paths, passphrases) are stored exclusively in the system Keychain on your device (iOS Keychain / macOS Keychain). They are never transmitted to TermBuddy servers, third-party servers, or any other external system.
</details>

<details>
<summary><b>What exactly is installed on my server?</b></summary>
<br>
A single lightweight Go binary (~15 MB) is placed in <code>~/.termbuddy/</code> under your own user account. It manages PTY (terminal) sessions and handles communication with the app. It binds only to <code>127.0.0.1:8765</code> by default — it is never accessible from outside the machine except through your SSH tunnel. No root or sudo privileges are required.
</details>

<details>
<summary><b>Do I need to open any firewall ports?</b></summary>
<br>
No. In the default SSH Tunnel mode, TermBuddy uses your existing SSH connection on port 22. All communication is tunneled through this single connection. No additional ports need to be opened on your server or router.
</details>

<details>
<summary><b>Will my terminal sessions keep running when I close the app?</b></summary>
<br>
Yes. The shell process runs on your server, managed by the TermBuddy server component. Closing the app does not kill the process. When you reopen the Buddy, you reconnect to the same running session. Long-running processes (builds, deployments, data jobs) continue uninterrupted.
</details>

<details>
<summary><b>What AI providers are supported?</b></summary>
<br>
Currently supported:
<ul>
  <li><b>Claude Code</b> (Anthropic) — Primary and most feature-rich integration</li>
  <li><b>Codex</b> (OpenAI) — Legacy support</li>
  <li><b>Gemini</b> (Google) — Legacy support</li>
</ul>
You supply your own API keys. TermBuddy does not charge for AI usage — API costs go directly to the AI provider.
</details>

<details>
<summary><b>Is my data private? Does TermBuddy see my commands or file contents?</b></summary>
<br>
TermBuddy has no cloud backend. Your device communicates directly with your server. TermBuddy (the company) has no access to your commands, output, files, or credentials. The only external network calls the app makes are to the App Store for subscription validation and to GitHub for server binary downloads.
</details>

<details>
<summary><b>What Linux distributions are supported for the server?</b></summary>
<br>
Any modern Linux distribution with glibc 2.17+ should work, including:
<ul>
  <li>Ubuntu 18.04+</li>
  <li>Debian 9+</li>
  <li>CentOS 7+ / RHEL 7+</li>
  <li>Fedora, Arch, Alpine, and others</li>
</ul>
Both x86_64 (amd64) and ARM64 (aarch64) architectures are supported. macOS servers (12.0+) are also supported.
</details>

<details>
<summary><b>Can I use TermBuddy with a server behind NAT (no public IP)?</b></summary>
<br>
Yes. We recommend using <a href="https://tailscale.com">Tailscale</a> or another WireGuard-based VPN to create a private network between your device and server. This is actually the more secure option, as your server's SSH port is never exposed to the public internet.
</details>

<details>
<summary><b>Is there an iPad version?</b></summary>
<br>
TermBuddy for iPhone runs in compatibility mode on iPad. A dedicated iPad version optimized for the larger screen is planned for a future release.
</details>

<details>
<summary><b>What happens to my data if I cancel my subscription?</b></summary>
<br>
Your local message history cache and server configurations are retained on your device. The TermBuddy server component continues running on your server. You will lose access to premium features, but your data is not deleted.
</details>

---

## Support

We actively monitor this repository for bug reports and feature requests.

| Channel | Use for |
|---------|---------|
| [**Bug Reports**](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues/new?labels=bug&template=bug_report.md) | Crashes, errors, incorrect behavior |
| [**Feature Requests**](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues/new?labels=enhancement&template=feature_request.md) | Ideas, suggestions, improvements |
| [**General Discussion**](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/discussions) | Questions, how-tos, community |
| [**All Issues**](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues) | Browse existing reports |

When reporting a bug, please include:
- TermBuddy app version (Settings → About)
- Device model and OS version
- Server OS and architecture (e.g., Ubuntu 22.04, x86_64)
- Steps to reproduce the issue
- Any relevant log output (Settings → Help → View Logs)

---

## Download

<p align="center">
  <a href="#">
    <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
  </a>
  &nbsp;&nbsp;
  <a href="#">
    <img src="https://developer.apple.com/assets/elements/badges/download-on-the-mac-app-store.svg" alt="Download on the Mac App Store" height="50">
  </a>
</p>

---

<p align="center">
  <img src="images/thumb_up.png" alt="TermBuddy" width="100">
  <br><br>
  <b>Stop wrestling with terminals. Start chatting with them.</b>
  <br>
  <sub>Made with care by <a href="https://github.com/ATLAI-TECH">ATLAI Technology</a></sub>
</p>
