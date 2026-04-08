<p align="center">
  <img src="images/logo_dark_bgbwhite.png" alt="TermBuddy Logo" width="200">
</p>

<h1 align="center">TermBuddy</h1>
<h3 align="center">Buddy Your Terminal. Own Your Workflow.</h3>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/iOS-17.0%2B-blue?logo=apple" alt="iOS 17+"></a>
  <a href="#"><img src="https://img.shields.io/badge/macOS-14.0%2B-blue?logo=apple" alt="macOS 14+"></a>
  <a href="#"><img src="https://img.shields.io/badge/License-Proprietary-lightgrey" alt="License"></a>
</p>

<p align="center">
  <b>Your terminal just became your best buddy.</b><br>
  Manage remote servers from your iPhone or Mac. Chat with your terminal like messaging a friend.
</p>

---

<p align="center">
  <img src="images/hero.png" alt="Welcome to TermBuddy" width="280">
  &nbsp;&nbsp;&nbsp;
  <img src="images/feature_chat.png" alt="Chat with Terminal" width="280">
  &nbsp;&nbsp;&nbsp;
  <img src="images/feature_tasks.png" alt="Manage Tasks" width="280">
</p>

---

## What is TermBuddy?

TermBuddy is a native macOS and iOS app that transforms how you interact with remote servers. Instead of staring at a cold, stateless terminal window, each server session becomes a "Buddy", a persistent, chat-style conversation where:

- Commands are sent as chat messages
- Output appears as reply bubbles
- History is preserved across restarts
- AI assistants can work right alongside you in the same interface

Whether you're a developer managing production servers, a DevOps engineer wrangling multiple environments, or a hobbyist maintaining a home lab, TermBuddy makes server management feel natural and efficient.

## Key Features

### Support SOTA AI
Built-in support for **Claude Code**, **Codex**, and **Gemini CLI**. Ask your AI assistant to write scripts, debug errors, or explain what's happening on your server, all within the same chat interface.

<p align="center">
  <img src="images/feature_platform.png" alt="Available Everywhere" width="300">
</p>

### Direct Connection. No Middleman. Fully Encrypted.
TermBuddy connects your device directly to your server. No intermediate relay, no third-party cloud. In SSH Tunnel mode, all traffic is encrypted through SSH. In Direct Connection mode, traffic is protected by TLS with certificate pinning. Your data never passes through anyone else's servers.

<p align="center">
  <img src="images/feature_security.png" alt="Secure and Reliable" width="300">
</p>

### Set Up in Seconds, Not Hours
Point TermBuddy at your server, enter your SSH credentials, and tap Go. The app installs everything automatically. No manual configuration required.

<p align="center">
  <img src="images/feature_setup.png" alt="Easy Setup" width="300">
</p>

### Built for Real Workflows

| Feature | Description |
|---------|-------------|
| **Multiple Servers & Buddies** | Each Buddy handles a different task on a different server |
| **Persistent History** | Session history survives app restarts and server reboots |
| **Push Notifications** | Get notified when long-running commands finish |
| **File Browser** | Browse, upload, and download files on your server |
| **Real-Time Streaming** | Live output via Server-Sent Events (SSE) |
| **Cross-Platform** | Available on iPhone and Mac with a single subscription |

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

### Adding Your First Server

1. Open TermBuddy and tap the **Servers** tab
2. Tap the **+** (Add Server) button
3. Enter your server's IP address or hostname
4. Enter your SSH username and password, or select an SSH key file
5. Tap **Connect**

TermBuddy will automatically detect, download, install, and start its lightweight server component. No manual steps required.

> **Tip:** Credentials are stored securely in the system Keychain, never in plain text.

> **Recommended:** For servers not on your local network, use Tailscale or another VPN to create a private network.

---

## How It Works

```
+----------------+                      +------------------+
|                |    SSH Encrypted      |                  |
|   iPhone /     | <==================> |  Your Server     |
|   Mac App      |    or TLS (HTTPS)    |  (TermBuddy      |
|                |                      |   Server - Go)   |
+----------------+                      +------------------+
        |                                      |
   No third-party                    Binds to localhost
   servers involved                  (SSH Tunnel mode)
```

1. **Add a Server** - Enter your SSH credentials
2. **Auto-Install** - TermBuddy installs its lightweight Go server automatically
3. **Create Buddies** - Each Buddy is a persistent terminal session
4. **Chat Away** - Send commands, get results, ask AI for help

---

## Security Model

TermBuddy is designed with a "no trust required" security philosophy:

| Aspect | How TermBuddy handles it |
|--------|--------------------------|
| **Credentials** | Stored in system Keychain only. Never sent to any third-party server. |
| **Network traffic** | Travels through your SSH connection (port 22) or TLS with certificate pinning. End-to-end encrypted. |
| **Server exposure** | Server component binds to 127.0.0.1 only. Never exposed to the public internet. |
| **AI API keys** | Stored on your own server, in your server's environment. TermBuddy app never sees them. |
| **Data relay** | No TermBuddy cloud. Your device connects directly to your server. Zero intermediaries. |
| **Server binary** | Runs under your own user account with your own permissions. No root required. |

---

## Troubleshooting

<details>
<summary><b>Cannot connect to server</b></summary>
<br>

- Verify the server IP address or hostname is correct
- Confirm SSH is enabled on the server (`sudo systemctl status sshd`)
- Check that port 22 is not blocked by a firewall
- If using a hostname with underscores, try using the IP address instead
</details>

<details>
<summary><b>Server shows "Offline" after setup</b></summary>
<br>

- Tap the server > Check Server Status to see the specific error
- Check if the process is running: `ps aux | grep termbuddy`
- Check the port is not in use: `lsof -i :8765`
- Try Update Server from the Servers tab
</details>

<details>
<summary><b>Claude Code AI Buddy not working</b></summary>
<br>

- Verify Claude Code is installed on the server: `which claude && claude --version`
- If not installed: `npm install -g @anthropic-ai/claude-code` (requires Node.js 18+)
- Confirm your Anthropic API key is entered correctly in Server Settings > AI Tools
</details>

---

## FAQ

<details>
<summary><b>Does TermBuddy store my SSH credentials on any server?</b></summary>
<br>
All credentials are stored securely in the system Keychain on your device. They are never transmitted to any third-party server.
</details>

<details>
<summary><b>What does the TermBuddy server install on my machine?</b></summary>
<br>
A lightweight Go binary (~15MB) that manages terminal sessions and communicates with the app. It runs under your user account and binds to localhost by default.
</details>

<details>
<summary><b>Do I need to open any ports?</b></summary>
<br>
No. In SSH Tunnel mode, TermBuddy uses your existing SSH connection (port 22). No additional ports need to be opened.
</details>

<details>
<summary><b>Which AI providers are supported?</b></summary>
<br>
Claude Code, Codex, and Gemini CLI. You bring your own API keys. TermBuddy never sees them.
</details>

<details>
<summary><b>Is it available on iPad?</b></summary>
<br>
Currently available on iPhone and Mac. iPad support is on the roadmap.
</details>

<details>
<summary><b>What happens to my data if I cancel my subscription?</b></summary>
<br>
Your data stays on your device and your server. TermBuddy does not store any of your data on its own servers.
</details>

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

## Support

We actively monitor this repository for bug reports and feature requests.

| Channel | Use for |
|---------|---------|
| [Bug Reports](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues/new?labels=bug&template=bug_report.md) | Crashes, errors, incorrect behavior |
| [Feature Requests](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues/new?labels=enhancement&template=feature_request.md) | Ideas, suggestions, improvements |
| [All Issues](https://github.com/ATLAI-TECH/TermBuddy-FeedBack/issues) | Browse existing reports |
| Email | [atlai@atlai.co.uk](mailto:atlai@atlai.co.uk) |

When reporting a bug, please include:
- TermBuddy app version (Settings > About)
- Device model and OS version
- Server OS and architecture (e.g., Ubuntu 22.04, x86_64)
- Steps to reproduce the issue
- Any relevant log output (Settings > Help > View Logs)

---

<p align="center">
  <img src="images/logo_dark_bgbwhite.png" alt="TermBuddy" width="120">
  <br><br>
  <b>Stop wrestling with terminals. Start chatting with them.</b>
  <br>
  <sub>Made with care by <a href="https://github.com/ATLAI-TECH">ATLAI Technology</a></sub>
</p>
