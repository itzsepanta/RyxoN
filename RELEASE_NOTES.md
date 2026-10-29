# RyxoN v1.2.1 — Release Notes

**Release date:** October 2026

**Downloads:** [v1.2.1 release page](https://github.com/itzsepanta/RyxoN/releases/tag/v1.2.1) — the counter is on the asset itself.

RyxoN 1.2.1 is the **fixes release**: the config formats that would not import
now do, the split tunnel does what it says, the ad blocker is worth turning on,
and the parts of the interface that got in the way have been got out of it.

---

## ✨ Highlights

- **Linux.** The same application, packaged for Linux x64: an AppImage that
  carries its own GTK and WebKitGTK, `.deb` and `.rpm` packages for the
  distributions that ship them, and a portable archive. Both WebKitGTK 4.0 and
  4.1 are covered, because they are different shared libraries and a build
  against one does not start on a system that only has the other.
- **WireGuard and AmneziaWG configs import properly.** A `.conf` pasted or added
  as a manual config is read as a config rather than as a link that fails to
  parse, and an AmneziaWG config keeps the obfuscation parameters (`Jc`, `Jmin`,
  `Jmax`, `S1`–`S4`, `H1`–`H4`) that its handshake depends on — dropping them was
  why a config that answered a ping elsewhere never answered one here.
- **Configs are named after themselves.** An imported config shows the name it
  carries, in its comment or its `Name` field, instead of every one of them being
  called "AmneziaWG".
- **A stronger ad blocker.** A curated list of mainstream advertising, analytics,
  measurement, session-replay and mobile-SDK networks — domains as
  `DOMAIN-SUFFIX`, plus keyword rules for the hosts that rotate too fast to name.
  Blocked names are now refused at the **DNS stage** as well as the connection,
  so a page cannot resolve an ad host and then be refused, and refusals **drop**
  the connection instead of resetting it, which is the shape ad-blocking
  detectors look for.
- **The split tunnel works, and says so.** It accepts a full path as well as a
  file name (the engine matches the file name, so a pasted path used to produce a
  rule that could never fire), rejects what cannot be a name instead of storing
  it, and tells you that routing is decided at connect time.
- **An error is reported once per run.** Errors your own actions produce — and
  the critical ones, such as a subscription that failed to refresh — are still
  reported every time.
- **TUIC and MASQUE.** Two more protocols the engine can carry, both read from
  share links, kept through a manual config, and written back out intact.
- **A ping is a measurement now.** Each node is sampled three times and reported
  as the median, with the spread beside it — so the number says how fast the node
  is *and* whether it stays that way.

---

## 🆕 New

### Subscriptions
- **Manual is a row.** It is pinned first, cannot be edited or deleted, shows how
  many hand-added configs there are, and carries the tick that makes them the
  configs the engine connects through.
- **Long addresses are readable.** A URL field is rendered left-to-right whatever
  the interface language (it was being displayed backwards in Persian), in a
  monospaced face, in a wider dialog, and the truncated address in the table can
  be read in full on hover.

### Servers
- **Hide is available on every row.** It used to be drawn only for a
  subscription's nodes, so a manual config had Delete as its only action — and
  deleting is exactly what someone who wants a config out of the list, but not
  gone, does not want to do.
- **The table fits.** Columns are sized so the row fits an ordinary window, and
  the Actions column is pinned to the end of the row so it is reachable even when
  it does not.
- The duplicate **Reachable / Delay / Speed / Options** row that sat under the
  subscription selector has been removed; the labelled one below it stays.

### Engine
- Ad-block rules are **prepended to a subscription that carries its own rules**.
  One that does not bring its own nodes — `proxy-providers`, most often — used to
  keep its own rule list, so the blocker was on and silently did nothing for it.
- Blocking is applied to DNS as well as to connections, through the same rules.

### Protocols
- **TUIC** — read from `tuic://` links, both the `uuid:password` form and the
  older token form, and the settings that decide how it performs are kept:
  congestion controller, UDP relay mode, heartbeat, reduce-RTT, ALPN, SNI.
- **MASQUE** — a WireGuard tunnel inside HTTP/3, so a config carries both halves:
  the key pair and address the tunnel authenticates with, and the URI it is
  dialled through. Read from `masque://` links, written back out the same way.
- Both are in the manual-config editor, in the protocol list, and in the
  sing-box converter, so a panel that serves them is not silently short a node.

### Measurement
- **A delay is the median of three samples.** One sample pays for the handshake
  as well as the round trip, and a single slow sample moves the number by more
  than the difference between two neighbouring nodes — which is how a list ends
  up ordered by luck. The median is what a person gets if they try it a few
  times.
- **The spread is shown beside it** (`84 ms ±6`). A node at 84 ms ±2 and one at
  84 ms ±90 are different choices, and one number cannot say which it is.
- **A TCP dial is no longer reported as a ping for protocols that do not answer
  on TCP.** Hysteria2, TUIC, WireGuard, AmneziaWG and MASQUE carry their payload
  in datagrams; dialling their port measured something that was not the proxy.

---

## 🐞 Fixes

- A WireGuard `.conf` added as a manual config no longer lands in the list
  unreadable, and a list mixing `.conf` bodies with share links keeps both.
- An AmneziaWG export keeps its obfuscation parameters, so a config that arrived
  correct is not quietly changed by being re-exported.
- A split-tunnel entry pasted as a path is stored as the executable name the
  engine actually matches, and two spellings of one program are one rule.
- Editing a very long subscription URL no longer distorts the dialog or the table.
- Errors that arrive on their own — the engine reporting the same failure on
  every reconnect attempt, the test loop reporting the same node every run — are
  reported once per run instead of filling the screen.
- A **VLESS or VMess** config that asks to skip certificate verification now
  reaches the engine with that flag. It was read for Trojan and Hysteria2 but not
  for those two, so a self-signed node failed TLS and read as a node that was
  down; a VMess config's uTLS fingerprint is kept for the same reason.
- A **Trojan WebSocket** link keeps its `Host` header and falls back to it for
  SNI. The header is what the server routes on: without it the config reached the
  right port and the wrong site.
- **Hysteria2** keeps its `up`/`down` bandwidth hints, which the engine uses to
  size its initial congestion window.
- A **sing-box** subscription's TUIC outbounds convert instead of being dropped,
  and a QUIC outbound is no longer given a `network: tcp` it does not have.
- A subscription's **status is no longer cut off** at the column edge. It used to
  read `Updated Oct 28, 09:1…` — three dots where the time should be — because
  the cell truncated a sentence; it wraps now, and the column is wider.
- **Switches animate in Persian.** The knob was moved twice — once by Tailwind's
  `translate` and once by a hand-written `transform: translateX(-0.9rem)` rule —
  and the two compose rather than replace each other, so they cancelled out and
  the knob sat still while the track turned blue. The hand-written rule is gone
  and the component mirrors the transform for RTL itself, so the knob slides
  from the right edge to the left one. It slides over 260ms on a soft curve,
  the same 260ms the track takes to change colour, so the two halves move
  together instead of the colour arriving first.
- **Notifications are in the interface language.** The sentences the app writes
  itself — a subscription refreshed, a chosen node that stopped carrying traffic,
  proxy settings that could not be changed, the firewall notice, and the
  subscription's own "updated" line — are translated, and the time inside them is
  formatted in that language. The engine's own errors stay as they are: they are
  technical detail, and a translation of them would help nobody read them.

---

## 🧹 Repository

- The CI and release workflows and the Arch packaging files were removed; this is
  not a project that is published from CI.
- The vendored engine source is no longer part of the repository. It is fetched
  by `desktop/scripts/setup-mihomo-core.sh` when it is needed.
- Third-party notices for the components that ship inside the application are
  kept in `licenses/`, where they have to be.

---

## 📥 Downloads

**Windows 10 / 11**

| Asset | Use it when |
|:--|:--|
| `RyxoN.exe` | 64-bit Windows 10 or 11 on Intel or AMD. No installation — just run it. |

**Linux (x64)**

| Asset | Use it when |
|:--|:--|
| `RyxoN-Desktop-1.2.1-linux-amd64.AppImage` | Any distribution. `chmod +x` and run — no installation. |
| `RyxoN-Desktop-1.2.1-linux-amd64.deb` | Debian 12, Ubuntu 22.04, Mint 21 — WebKitGTK 4.0. |
| `RyxoN-Desktop-1.2.1-linux-amd64.rpm` | Fedora 38–39, RHEL 9 — WebKitGTK 4.0. |
| `RyxoN-Desktop-1.2.1-linux-amd64-webkit41.deb` | Ubuntu 24.04+, Debian 13, Mint 22 — WebKitGTK 4.1. |
| `RyxoN-Desktop-1.2.1-linux-amd64-webkit41.rpm` | Fedora 40+, RHEL 10 — WebKitGTK 4.1. |
| `RyxoN-Desktop-1.2.1-linux-amd64.zip` | Portable fallback: unpack and run `./RyxoN`. |

The AppImage carries its own GTK 3 and WebKitGTK libraries. The `.deb` and
`.rpm` use the ones from the distribution, so each comes in two variants —
install the one that matches the WebKitGTK your distribution ships.

---

# RyxoN v1.2.0 — Release Notes

**Release date:** September 2026

**Downloads:** [v1.2.0 release page](https://github.com/itzsepanta/RyxoN/releases/tag/v1.2.0) — the counter is on the asset itself.

RyxoN 1.2.0 is the **rebrand release**: the app is now **RyxoN**, with a new identity, an **ad blocker**, a rebuilt notification system, a state-aware tray icon, and **in-app updates** that download and install themselves on restart instead of leaving you to fetch a new file by hand.

---

## ✨ Highlights

- **New name, new look.** The app is now **RyxoN** — a new logo and icon set across the executable, taskbar, tray, and window, and the version shown beside the name in the sidebar. The violet-to-pink theme carries through the whole interface.
- **In-app updates.** RyxoN checks for a newer release on its own and on demand from **Settings → Updates**. It shows the version and notes, downloads the correct asset for your platform, and **installs it on restart**. GitHub is fetched over the tunnel first, so updating works from the same networks the app exists to get around.
- **Ad blocker.** Rejects known advertising and tracker domains at the engine, before any traffic leaves. Off by default.

---

## 🆕 New

### Ad blocker
- A built-in blocklist of mainstream ad and analytics networks, applied as `DOMAIN-SUFFIX` rules so subdomains are covered without an unwieldy list. **Off by default** — blocklists are opinionated, and a fresh install must not break pages until you ask for it.
- Composes with split tunnel and connection chaining.

### Updates
- **Check for updates** from **Settings → Updates**, showing the current version, the new version, and the release notes.
- **Download** fetches the release asset for your platform, and **Install & Restart** swaps it in. Downloads go over the tunnel first when one is up.
- The app remembers a version it has already told you about, so the "update available" notice appears **once**, not on every launch.

### Interface
- **State-aware tray icon** — it colours to show whether traffic is actually being carried, so a dead tunnel is visible at a glance instead of looking identical to a healthy one.
- **Rebuilt notifications** — a single, consistent notice system with proper stacking, dismissal, and expandable details (including firewall prompts).

### Nodes
- **Test every subscription in one run**, with results labelled by the list each one came from.
- **Choose the port** shared on the local network, rather than letting it be discovered and hoping it stays put.

---

## 🔧 Changed

- **Legacy import is broader.** On first launch, profiles from both **MigMig VPN** and **WhiteDNS Desktop** installs are offered for import.
- **The version now comes from the build.** A release built through the Makefile carries its real version; a plain development build honestly says `dev` instead of claiming a release number nobody cut.
- **Linux tunnel** is offered where it can come up, and is verified on a real Linux machine in CI.

---

## 🗑️ Removed

The **Tools** section is gone, along with the pages that lived in it:
- the IP/endpoint **validator and scanner**,
- **White IP** generation and import,
- **Backup / restore** of settings as JSON,
- the **YouTube** subscribe item.

What they did is either handled automatically now, sat outside what this app is for, or was a maintenance surface that did not earn its keep.

---

##  Fixed

- **In-app update flow** — five defects in the new download-and-install path:
  - The app **never exited** to let the update helper swap the binary, so the helper waited forever. It now schedules its own exit after handing off.
  - The download used the **release page URL** (an HTML page) instead of the platform's release asset — which would have saved a web page as the new executable. It now picks the right asset per platform, with a sensible fallback.
  - The download ignored the active tunnel and used a direct connection.
  - The Windows and Unix restart helpers used unreliable wait logic (`%ERRORLEVEL%` expansion and `pgrep` by basename); both now wait correctly.
  - The "already notified about this version" check was per-session only, so the notice reappeared on every launch.
- **Closing the window** quits when no tray icon is shown, instead of leaving a process with no way back.
- **Filter menus** open reliably.

---

## ️ Under the hood

- **CI builds and tests the engine**, so its tests stop silently skipping, and asks a **real Mac** and a **real Linux machine** the questions the proxy and tunnel rules rest on.

---

## 📥 Download

**Windows 10 / 11 · 64-bit · No installation required — just run the `.exe`.**

[Download RyxoN v1.2.0](https://github.com/itzsepanta/RyxoN/releases/latest)

> 💡 If Windows SmartScreen shows a warning, click **More info → Run anyway**.

---

## 📝 Upgrading

Run RyxoN and it will offer the update, or check **Settings → Updates**. Profiles from a MigMig VPN or WhiteDNS Desktop install are detected on first launch and offered for import; nothing on your machine is changed until you accept.

---

**Full diff:** [`v1.0.19...v1.2.0`](https://github.com/itzsepanta/RyxoN/compare/v1.0.19...v1.2.0)