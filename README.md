<div align="center">

<img src="icon.png" alt="RyxoN" width="112" />

# RyxoN

**A desktop VPN client that tells you the truth about your connection.**

*Your own subscriptions and configs, a real exit check, and automatic failover — on Windows and Linux.*

<br />

[![Version](https://img.shields.io/badge/version-1.2.1-7C3AED?style=for-the-badge&logo=semanticrelease&logoColor=white)](#download)
[![Status](https://img.shields.io/badge/status-stable-22C55E?style=for-the-badge)](#)
[![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?style=for-the-badge&logo=windows11&logoColor=white)](#download)
[![Linux](https://img.shields.io/badge/Linux-x64-FCC624?style=for-the-badge&logo=linux&logoColor=black)](#download)
[![Telegram](https://img.shields.io/badge/Telegram-Join%20channel-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/ryxon)

</div>

---

## Overview

RyxoN is a desktop client for the proxies you already have. It reads your
subscriptions and manual configs, connects through the **mihomo** engine, and
then **checks what actually happened** — the exit country is measured through the
tunnel, not read from the node's label. When a route stops carrying traffic it
moves to another one, and it says so instead of going quiet.

No account. No telemetry. No analytics. Your configuration stays on your machine.

<div align="center">

| | |
|:--|:--|
| **Engine** | mihomo (Clash.Meta), built from pinned FlClash sources |
| **Interface** | React 18 · TypeScript · Vite · Tailwind CSS v4 · shadcn/ui |
| **Shell** | Wails v2 (native window, Go backend) |
| **Languages** | English and Persian, with full right-to-left layout |

</div>

---

## Contents

- [Features](#features)
- [Supported protocols](#supported-protocols)
- [Download](#download)
- [Quick start](#quick-start)
- [Build from source](#build-from-source)
- [How it works](#how-it-works)
- [Privacy](#privacy)
- [FAQ](#faq)
- [Community](#community)

---

## Features

### Connectivity

- **Every protocol the engine can carry** — VLESS, VMess, Trojan, Shadowsocks,
  Hysteria2, TUIC, MASQUE, WireGuard, AmneziaWG and AnyTLS, from share links,
  `.conf` files, or a whole subscription document.
- **Subscriptions in the formats panels actually serve** — a list of share links,
  a mihomo/Clash YAML, or a sing-box JSON document. All three are read; the last
  two are converted rather than rejected.
- **Manual configs** — paste a share link or import a WireGuard / AmneziaWG
  profile. They live in their own row in Subscriptions and can be the configs the
  engine connects through.
- **Smart selection** — filter by country or protocol, or pin one node. A pinned
  node is never silently replaced; if it fails, you are told.

### Accuracy

- **The exit country is measured, not claimed.** RyxoN asks an outside service
  which country your traffic appears to come from and compares it with the node's
  own label. When they disagree, the measurement wins.
- **A ping is a measurement.** Each node is sampled three times and reported as
  the **median**, with the **spread** beside it — so the number says how fast the
  node is *and* whether it stays that way.
- **Protocols that do not answer on TCP are not reported as if they did.**
  Hysteria2, TUIC, WireGuard, MASQUE and AmneziaWG are measured through the
  engine, not with a TCP dial that could never succeed.
- **A tunnel check with a grade** — TCP, TLS, HTTP, WebSocket, UDP, QUIC and DNS
  probes, graded **A+ to F**, with false-positive detection.

### Reliability

- **Health checks every 20 seconds**, with automatic failover when traffic stalls.
- **Background operation** — closing the window minimises to the tray and the
  tunnel keeps running.
- **An error is reported once per run**, not on every retry.
- **In-app updates** — RyxoN checks for a newer release, shows the notes, and
  installs it on restart.

### Interface

- **Light and dark themes**, animated transitions, and a native window frame.
- **Bilingual** — English and Persian, with the whole layout mirrored for RTL.
- **A server workbench** — reachability, latency and throughput per node, sortable,
  with share links one click away.
- **Split tunnel** and a **curated ad blocker** that refuses blocked names at the
  DNS stage and drops the connection rather than resetting it.

---

## Supported protocols

| Scheme | Protocol | Transport |
|:--|:--|:--|
| `vless://` | VLESS | TCP, WebSocket, gRPC, HTTP/2, TLS, REALITY |
| `vmess://` | VMess | TCP, WebSocket, gRPC, HTTP/2, TLS |
| `trojan://` | Trojan | TCP, WebSocket, gRPC, TLS |
| `ss://` | Shadowsocks | TCP, UDP |
| `hysteria2://` | Hysteria2 | QUIC |
| `tuic://` | TUIC | QUIC |
| `masque://` | MASQUE | HTTP/3 CONNECT-UDP |
| `wireguard://` | WireGuard | UDP |
| `anytls://` | AnyTLS | TCP, TLS |
| `vpn://` | AmneziaWG | UDP, with obfuscation parameters |

A subscription may also be a **mihomo/Clash YAML** or a **sing-box JSON**
document; both are converted to what the engine runs.

---

## Download

<div align="center">

### Latest release — `v1.2.1`

[![Download](https://img.shields.io/badge/⬇_All_releases-7C3AED?style=for-the-badge&logo=github&logoColor=white)](https://github.com/itzsepanta/RyxoN/releases/latest)

</div>

### Windows 10 / 11

| Asset | Use it when |
|:--|:--|
| `RyxoN.exe` | Normal 64-bit Windows on Intel or AMD. No installation — just run it. |
| The ARM64 archive | Windows on ARM (Snapdragon, Surface Pro X). |

### Linux (x64)

| Asset | Use it when |
|:--|:--|
| `RyxoN-Desktop-…-linux-amd64.AppImage` | Any distribution. `chmod +x` and run — no installation. |
| `RyxoN-Desktop-…-linux-amd64.deb` | Debian 12, Ubuntu 22.04, Mint 21 — WebKitGTK 4.0. |
| `RyxoN-Desktop-…-linux-amd64.rpm` | Fedora 38–39, RHEL 9 — WebKitGTK 4.0. |
| `RyxoN-Desktop-…-linux-amd64-webkit41.deb` | Ubuntu 24.04+, Debian 13, Mint 22 — WebKitGTK 4.1. |
| `RyxoN-Desktop-…-linux-amd64-webkit41.rpm` | Fedora 40+, RHEL 10 — WebKitGTK 4.1. |
| `RyxoN-Desktop-…-linux-amd64.zip` | Portable fallback: unpack and run `./RyxoN`. |

The AppImage carries its own GTK 3 and WebKitGTK libraries. The `.deb` and
`.rpm` use the ones from your distribution, which is why each comes in two
variants — install the one that matches the WebKitGTK your distribution ships.

> **Windows SmartScreen:** the executable is not code-signed, so the first launch
> may show *"Windows protected your PC"*. Choose **More info → Run anyway**. The
> binary is built from this repository by the release workflow; the source is
> here to check.

---

## Quick start

1. **Download** the build for your system from [Releases](https://github.com/itzsepanta/RyxoN/releases).
2. **Launch RyxoN.**
3. **Add a subscription** — paste its address — or import a **manual config**.
4. **Pick a node**, or let smart selection choose one.
5. **Connect**, then read the **real exit country** in the status panel.

---

## Build from source

### Requirements

| | |
|:--|:--|
| Go | 1.25 or newer — the module pins the 1.26.5 toolchain, which Go fetches itself |
| Node.js | 20 or newer |
| Wails CLI | `go install github.com/wailsapp/wails/v2/cmd/wails@latest` |
| Windows | WebView2 runtime (present on Windows 11 and current Windows 10) |
| Linux | `libgtk-3-dev`, `libwebkit2gtk-4.0-dev`, `pkg-config`, `build-essential` |

The engine is not committed. The build fetches the pinned FlClash sources and
compiles mihomo for the target platform into `desktop/cores/`, then embeds it in
the binary.

### Windows

```bash
cd desktop
make deps
make build-windows
```

The executable lands in `desktop/build/bin/RyxoN.exe`.

### Linux

Linux packaging must run on a Linux host — Wails links against GTK and WebKitGTK
with cgo, which cannot be cross-compiled from Windows. On a Linux machine:

```bash
cd desktop
make deps
make package-linux-distros
```

Or, from any host with Docker:

```bash
cd desktop
make package-linux-all-docker
```

The packages are written to `desktop/build/releases/all/`.

The Docker path installs GTK, WebKitGTK, Node and the Wails CLI on every run.
Building the toolchain image once makes later runs much faster:

```bash
docker build -f scripts/linux-builder.Dockerfile -t ryxon-linux-builder:1.2.1 scripts
LINUX_DOCKER_IMAGE=ryxon-linux-builder:1.2.1 make package-linux-all-docker
```

If Docker Hub is not reachable from your network, point the build at a registry
mirror:

```bash
docker build --build-arg BASE_IMAGE=<mirror>/library/golang:1.26.5-bookworm \
  -t ryxon-linux-builder:1.2.1 -f scripts/linux-builder.Dockerfile scripts
```

On a slow connection, the host's Go module cache saves the download that most
often fails — the Wails module:

```bash
GOMOD_CACHE_DIR="$(go env GOMODCACHE)" \
  LINUX_DOCKER_IMAGE=ryxon-linux-builder:1.2.1 make package-linux-all-docker
```

### Tests

```bash
cd desktop
go test ./...                    # backend
npm run build --prefix frontend  # type check and production bundle
```

---

## How it works

```
┌──────────────────────────────┐        ┌──────────────────────────────┐
│  React interface             │        │  Go backend                  │
│  TypeScript · Tailwind v4    │◄──────►│  Wails bindings and events   │
└──────────────────────────────┘        └──────────────┬───────────────┘
                                                       │ named pipe,
                                                       │ length-prefixed JSON
                                        ┌──────────────▼───────────────┐
                                        │  mihomo engine (child)       │
                                        │  proxies, rules, TUN         │
                                        └──────────────────────────────┘
```

The engine runs as a child process and speaks a small framed-JSON protocol over a
named pipe. The interface never talks to it directly: the Go backend owns the
process, the configuration, the health checks and the measurements, and publishes
what it learns as events.

The engine is **mihomo**, built from the FlClash sources pinned in
`desktop/scripts/setup-mihomo-core.sh`. The build refuses to embed a stock mihomo
binary: the pinned core is patched to dial back over the pipe, and a stock build
ignores the endpoint it is handed.

---

## Privacy

- **No telemetry, no analytics, no crash reporting.** Nothing about your usage
  leaves the machine.
- **No account.** There is nothing to sign in to.
- **Your configuration stays local.** Subscriptions, profiles and settings live in
  your user data directory; the app reads them and writes them back.
- **The only network traffic** is what you asked for: your subscriptions, the
  nodes you connect through, the exit-country check, and the update check.

---

## FAQ

**Does RyxoN provide servers?**
No. It is a client. You bring a subscription or your own configs.

**Why does the exit country differ from the node's name?**
Because the name is a label someone typed. RyxoN measures the country your traffic
actually leaves from and shows that instead.

**The app says the engine did not connect.**
That message means the engine process started but never dialled back over its
pipe — usually a missing or wrong core. Rebuild with `make build-windows` (or
`make package-linux-distros`) so the pinned engine is compiled and embedded.

**Windows shows a SmartScreen warning.**
The executable is not code-signed. Choose **More info → Run anyway**; the source
is in this repository.

**Does it work on macOS?**
The codebase builds for macOS, but no macOS package is published. Treat it as
untested.

---

## Community

Release notes, questions and support live on the **RyxoN Telegram channel**:
**[t.me/ryxon](https://t.me/ryxon)**.

Full changelog: [RELEASE_NOTES.md](RELEASE_NOTES.md).

---

<div align="center">

### If RyxoN is useful to you, a star helps.

**Made by [RyxoStudio](https://ryxo.ir)**

<sub>© 2026 RyxoN · All rights reserved.</sub>

</div>
