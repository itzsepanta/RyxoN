<div align="center">

<img src="icon.png" alt="RyxoN" width="110" />

# RyxoN

**A modern, reliable desktop VPN client for Windows**

*Built for clarity, speed, and control — with real exit verification and automatic failover.*

<br>

[![Version](https://img.shields.io/badge/version-1.2.0-7C3AED?style=for-the-badge&logo=semanticrelease&logoColor=white)](#download)
[![Platform](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?style=for-the-badge&logo=windows11&logoColor=white)](#download)
[![Telegram](https://img.shields.io/badge/Telegram-Join%20Channel-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/RyxoStudio)
[![Downloads](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/itzsepanta/5c410d35f0eb048165280ab2276adebc/raw/migmig-vpn-downloads.json)](https://github.com/itzsepanta/RyxoN/releases)

</div>

---

## 📖 Overview

**RyxoN** is a Windows desktop client engineered for **reliability and transparency**.
It connects through your own subscriptions and manual configs, surfaces **real exit information**, and **recovers automatically** when a route fails — no silent drops, no guesswork.

> 🎯 *No telemetry. No bundled servers. Just your configs, working the way they should.*

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🔌 Connectivity

- **Broad protocol support** — `vless://`, `vmess://`, `trojan://`, `ss://`, `hysteria2://`, `wireguard://`, `anytls://`, and `vpn://`
- **Manual configs** — paste share links or import **WireGuard / AmneziaWG** profiles alongside your subscriptions
- **Smart selection** — filter by **country** or **protocol**, or pin a specific node; invalid choices are **rejected**, not ignored
- **Accurate status** — displays the node's *claimed* location **and** the *real* exit country measured through the tunnel. When they differ, **the measurement wins.**

</td>
<td width="50%" valign="top">

### 🛠️ Reliability

- **Health checks** every **20 seconds** with automatic failover when traffic stalls
- **Pinned nodes stay pinned** — manual selections are never silently overridden
- **Background operation** — closing the window minimizes to tray; the tunnel keeps running
- **Tunnel-check engine** — probes over **TCP / TLS / HTTP / WebSocket / UDP / QUIC / DNS** with **A+–F grading** and false-positive detection
- **Server workbench** — test reachability, latency, and throughput; sort results; share node links

</td>
</tr>
<tr>
<td colspan="2" valign="top">

### 🎨 Interface

- Clean, **animated UI** with **light & dark** modes
- **Violet → Pink** brand theme with smooth transitions throughout
- Native Windows 10/11 look & feel

</td>
</tr>
</table>

---

## 📥 Download

<div align="center">

### Latest Release — `v1.2.0`

[![Download for Windows](https://img.shields.io/badge/⬇_Download_for_Windows-RyxoN.exe-7C3AED?style=for-the-badge&logo=windows11&logoColor=white)](https://github.com/itzsepanta/RyxoN/releases/latest)

**Windows 10 / 11 · 64-bit · No installation required — just run the `.exe`**

</div>

> 💡 **Tip:** If Windows SmartScreen shows a warning, click **More info → Run anyway**. The app is safe and open about its behavior.

---

## 🚀 Quick Start

1. **Download** the latest release from the [Releases](https://github.com/itzsepanta/RyxoN/releases) page — or let a running RyxoN update itself.
2. **Launch RyxoN.**
3. **Add a subscription** (paste your share link) or import a **manual config**.
4. **Pick a node** — or let Smart Selection choose the best one.
5. **Connect** and verify your **real exit country** in the status panel. ✅

---

<div align="center">

### If RyxoN helps you, consider starring the repo!

**Made with ❤️ and ☕ by [RyxoStudio](https://ryxo.ir)**

<sub>© 2026 RyxoN · All rights reserved.</sub>
</div>
