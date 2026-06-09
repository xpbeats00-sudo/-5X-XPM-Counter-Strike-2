# 🎮 XPM RPG — CS2 Dedicated Server

> A fully custom **RPG experience** baked into a Counter-Strike 2 dedicated server — featuring 8 team-locked classes, skill trees, prestige up to Master Level 1000, a cosmetic token shop, dynamic bot difficulty scaling, and a live center-screen HUD. Built on CounterStrikeSharp + Metamod:Source.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [✨ Key Features](#-key-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [📁 Project Structure](#-project-structure)
- [🔧 Prerequisites](#-prerequisites)
- [🚀 Installation & Setup](#-installation--setup)
- [▶️ Running the Server](#️-running-the-server)
- [⚙️ Configuration Reference](#️-configuration-reference)
  - [server.cfg](#servercfg)
  - [Game Mode CFGs](#game-mode-cfgs)
  - [Bot Tier CFGs](#bot-tier-cfgs)
  - [launch.bat Variables](#launchbat-variables)
- [🧙 RPG System Deep Dive](#-rpg-system-deep-dive)
  - [Classes](#classes)
  - [XP Sources](#xp-sources)
  - [Level System](#level-system)
  - [Perk System](#perk-system)
  - [Skill System](#skill-system)
  - [Prestige System (P1–P10)](#prestige-system-p1p10)
  - [Master Prestige (Level 1–1000)](#master-prestige-level-11000)
  - [Token Shop](#token-shop)
- [📟 Command Reference](#-command-reference)
- [🖥️ HUD System](#️-hud-system)
  - [Center HUD (PrintToCenterHtml)](#center-hud-printtocenterhtml)
  - [Panorama Custom HUD](#panorama-custom-hud)
  - [HTTP API](#http-api)
- [🗄️ Data Storage](#️-data-storage)
- [🤖 Bot Difficulty System](#-bot-difficulty-system)
- [🗺️ Map Rotation](#️-map-rotation)
- [✅ QoL Features](#-qol-features)
- [🔒 Security Measures](#-security-measures)
- [📝 Logging & Error Handling](#-logging--error-handling)
- [📦 Building & Deploying the Plugin](#-building--deploying-the-plugin)
- [🔮 Future Improvement Ideas](#-future-improvement-ideas)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🌐 Overview

**XPM RPG** is a custom RPG overlay for a CS2 dedicated server hosted on a Windows 11 LAN machine. It intercepts normal CS2 gameplay and layers a full progression system on top — players earn XP for kills, objectives, and assists, spend it on perks, unlock class-specific active skills, prestige up to 10 times, and ultimately climb a Master Prestige ladder from level 1 to 1000.

The server is designed for private LAN play with friends and supports multiple game modes (Deathmatch, Arms Race, Casual, Competitive 5v5), with bot difficulty that automatically scales to the human player's RPG level.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🧙 **8 Team-Locked Classes** | Four T-side and four CT-side classes, each with a unique active skill, passive speed, and spawn bonuses |
| 📈 **Full XP & Leveling** | Kill, headshot, knife, AWP, assist, bomb, round win, and MVP all award XP at a 5× multiplier |
| 🔮 **Perk Trees** | 5 perks per class × 3 ranks each — spend XP to permanently upgrade stats |
| ⚡ **Active Skills** | Each class gets a unique skill at Level 5 with a live cooldown display |
| ⭐ **Prestige P1–P10** | 10 prestige tiers with stacking bonuses (armor, HP, XP rate, cooldown reduction) |
| 🏆 **Master Prestige (1–1000)** | CoD BO3-style Master Prestige — 10 milestone tiers with unique icons every 100 levels |
| 🛒 **Cosmetic Token Shop** | Earn tokens through play, spend on chat tags, name colors, kill banner styles |
| 🤖 **Adaptive Bot AI** | 5 bot difficulty tiers auto-scaled to the human player's level with vision range tuning |
| 🖥️ **Live Center HUD** | Real-time skill cooldown bar, XP progress, perks, kills, multiplier — all in-screen |
| 🌐 **Panorama + HTTP API** | Custom Panorama layout + local HTTP server for external HUD tools (LHM, overlays) |
| 💾 **Atomic Data Saves** | Crash-safe atomic JSON writes with automatic `.bak` backup |
| 🔄 **Map Rotation Safety** | Plugin-level match-end handler prevents server hang on map cycle failures |

---

## 🛠️ Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Game Engine | Counter-Strike 2 Dedicated Server | Latest (Build 10772+) |
| Plugin Framework | Metamod:Source | 2.0.0-dev+1402 |
| Plugin API | CounterStrikeSharp (CSS) | 1.0.369 |
| Plugin Language | C# / .NET | .NET 10 |
| Data Format | JSON (System.Text.Json) | .NET built-in |
| HUD Scripting | Panorama JavaScript / XML / CSS | CS2 built-in |
| HTTP API | .NET `HttpListener` | .NET built-in |
| OS / Platform | Windows 11 LAN | x64 |
| Build Tool | `dotnet build` | .NET SDK 10 |

---

## 📁 Project Structure
