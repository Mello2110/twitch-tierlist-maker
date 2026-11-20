---
id: "twitch-tierlist-maker"
title: "Twitch Tierlist Maker"
tagline: "Interactive OBS broadcast overlay for live Twitch chat tierlist voting with real-time charts and IndexedDB storage."
category: "tool"
status: "production"
featured: false
badge: "OBS Studio Tool"
problemStatement: "Standard web-based tierlist makers lack native Twitch chat integration and force streamers to capture cluttered browser windows instead of clean 1920x1080 OBS overlays. Furthermore, storing dozens of custom item images in localStorage quickly hits the 5 MB browser quota limit."
technicalSolution: "A self-contained single-file HTML5 broadcast application designed directly for OBS Studio Browser Sources, connecting to Twitch IRC over WebSockets with live Chart.js vote visualization. Uploaded images are compressed to WebP and persisted in IndexedDB to bypass localStorage limits while keeping all overlay controls, bilingual UI, and JSON backups offline-capable."
techStack:
  - "HTML5"
  - "CSS3"
  - "JavaScript"
  - "Chart.js"
  - "IndexedDB"
  - "Twitch IRC WebSocket"
architectureHighlights:
  - "Zero-dependency single-file architecture tailored for OBS Studio Browser Source and Interact window workflows"
  - "IndexedDB image store with synchronous in-memory cache and automatic localStorage migration"
  - "Twitch IRC WebSocket client with IRCv3 tags for broadcaster/moderator chat commands and silent exponential-backoff reconnect"
  - "Scoped 1400x1032 overlays keeping the 520x520 OBS chat area unobstructed during pause and result screens"
screenshots:
  - "/screenshots/twitch-tierlist-maker/01-overview.png"
  - "/screenshots/twitch-tierlist-maker/02-feature.png"
  - "/screenshots/twitch-tierlist-maker/03-detail.png"
links:
  chromeWebStore: ""
  demoUrl: ""
  githubUrl: "https://github.com/Mello2110/twitch-tierlist-maker"
sandbox:
  enabled: false
  type: "none"
  embedUrl: ""
  notes: "Designed as a local 1920x1080 OBS Studio Browser Source overlay with Twitch IRC WebSocket integration."
stats:
  version: "v2.5.0"
---

# Twitch Tierlist Maker

[![Status](https://img.shields.io/badge/Status-Active-emerald?style=flat-square)](#)
[![Version](https://img.shields.io/badge/Version-v2.5.0-blue?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](#)

> Interactive OBS broadcast overlay for live Twitch chat tierlist voting with real-time charts and IndexedDB storage.

<p align="left">
  <a href="https://github.com/Mello2110"><b>Mellow Solutions on GitHub</b></a> &nbsp;|&nbsp;
  <a href="https://buymeacoffee.com/mellowsolutions"><b>Buy Me a Coffee</b></a>
</p>

---

## Problem & Motivation
Running community tierlists on Twitch usually requires either manual drag-and-drop without real vote counting or screen-capturing third-party websites filled with ads and mismatched aspect ratios. Streamers need a clean, reliable `1920×1080` OBS Browser Source where viewers can vote directly via chat commands (`!S`, `!A`, `!B`, ...) while keeping a dedicated `520×520` space unobstructed for an on-stream Twitch chat overlay.

## Technical Solution
**Twitch Tierlist Maker** (`TierlistProSystem.html`) is a zero-build, single-file broadcast tool built for OBS Studio:
- **Live Twitch Chat Voting:** Connects directly to `wss://irc-ws.chat.twitch.tv:443` with `CAP REQ :twitch.tv/tags`, supporting single-vote correction, a toggleable **Multi-Vote** mode, optional trailing text after commands (`!S great game`), and broadcaster/moderator commands (`!tl start`, `!tl pause`, `!tl next`, `!tl skip`).
- **Dual Scoring Modes:** Choose between **Absolute Mode** (most votes win) and **Weighted Average Mode** (score-weighted placement with configurable tie-breakers and optional auto-sorting).
- **Unlimited Local Image Storage:** Uploaded images are center-cropped, WebP-encoded, and stored in **IndexedDB** (`TierlistProImages`) with an in-memory render cache, avoiding the 5 MB `localStorage` limit.
- **Broadcast-Ready Overlays & Themes:** Features a Gold-to-Crimson vintage tier palette, adjustable background opacity (`0–100%`) for transparent OBS scenes, bilingual UI (`English` / `Deutsch`), and scoped pause/result overlays that never cover the `520×520` chat area.

## Architecture & Tech Stack
- **Languages & Libraries:** Vanilla HTML5, CSS3 (custom properties & 1920×1080 broadcast grid), ES2022 JavaScript, Chart.js 4.4 (UMD).
- **Core Architecture:**
  - **Storage Layer:** `IndexedDB` for binary/WebP item thumbnails + `localStorage` for tier configuration, placements, and Twitch credentials with automatic schema migration.
  - **Network Layer:** Stateful Twitch IRC WebSocket client with `PING`/`PONG` heartbeat, silent exponential-backoff reconnect, and auth-error handling.
  - **UI & Controls:** Tabbed OBS-friendly settings drawer (*Twitch & Setup*, *Items*, *Tiers & Voting*, *Design & OBS*, *Backup*), drag-and-drop plus click-to-move item controls, and two-step inline confirmation for destructive actions.

## Installation & Usage
1. Download or clone the repository and locate `TierlistProSystem.html`.
2. In **OBS Studio**, add a new **Browser** source, enable **Local file**, and select `TierlistProSystem.html`.
3. Set the Browser Source resolution to **Width: `1920`**, **Height: `1080`**.
4. Right-click the source in OBS and open **Interact** → click the **Settings** gear icon:
   - **Twitch & Setup:** Enter your Twitch channel name and OAuth token (`chat:read` scope) and click **Save & Connect**.
   - **Items:** Drag & drop your images, adjust names or shuffle the queue.
   - **Tiers & Voting / Design & OBS:** Customize tier commands, colors, voting mode, language (`EN`/`DE`), and background opacity.
5. Click **Start Voting** (or use hotkeys `N` Next, `U` Undo, `Space` Pause, `Esc` Close Menu) and let your chat vote with `!S`, `!A`, `!B`, `!C`, `!D`, `!L`.

## License & Disclaimer
Part of the **Mellow Solutions** portfolio. Provided under the MIT License as-is for non-commercial and personal utility.
