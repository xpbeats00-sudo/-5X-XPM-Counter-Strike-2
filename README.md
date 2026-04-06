# ⚔️ XP MOD — CS2 Dedicated Server

> A fully custom **RPG perk system** for Counter-Strike 2, built on [CounterStrikeSharp](https://github.com/roflmuffin/CounterStrikeSharp) and [Metamod:Source](https://www.sourcemm.net/). Choose your class, earn XP, unlock perks, and dominate with class-specific active skills.

---

## 🖥️ Server Info

| Field | Value |
|-------|-------|
| **Hostname** | `[5X] XPMod` |
| **Map** | `de_dust2` (active rotation) |
| **Tickrate** | 128 |
| **Max Players** | 32 |
| **Mode** | Casual / Classic |
| **Connect** | `connect <server-ip>:27015` |

---

## 🎮 RPG System Overview

XP Mod transforms CS2 into a full RPG experience. Every kill, assist, bomb plant, defuse, MVP, and round win earns you **XP** (5x multiplier). Level up to unlock class perks and a powerful active skill that **auto-activates every round**.

### 📊 XP Sources

| Action | Base XP | Multiplied |
|--------|---------|------------|
| Kill | 50 | 250 |
| Headshot bonus | +10 | +50 |
| Knife kill bonus | +20 | +100 |
| AWP kill bonus | +15 | +75 |
| Assist | 20 | 100 |
| Bomb plant | 30 | 150 |
| Bomb defuse | 40 | 200 |
| Round win | 25 | 125 |
| MVP | 60 | 300 |

### 🏆 Level Milestones

| Level | Unlock |
|-------|--------|
| **1** | Tier 1 perks available |
| **5** | Active skill unlocked (auto-use each round) |
| **10** | Tier 2 perks available |
| **20** | Ultimate perks available |
| **30** | MAX LEVEL 👑 |

---

## 🔴 Terrorist Classes

### 💣 Bomber
*C4 specialist — plant fast, blow everything up*

- Speed burst after planting C4
- Bonus HP on spawn at higher levels
- **Skill:** `Adrenaline Rush` — +50% speed for 5s
- **Perks:** sprint · blastradius · ironwill · martyrdom · adrenaline

### 👻 Ghost
*Knife/stealth assassin — kill silently, heal on blood*

- Enhanced movement speed
- Vampirism: heal HP on every kill
- **Skill:** `Shadow Step` — +80% speed burst for 3s
- **Perks:** stealth · vampirism · shadowblade · smokescreen · martyrdom

### 🎯 Expert Shooter
*Rifle/AR master — headshots reward you*

- Bonus max HP for rifle duels
- Speed burst after headshot kills
- **Skill:** `Combat Stims` — +25 HP injection
- **Perks:** steadyaim · combatflow · hardenedbody · armorpiercer · stims

### 🏃 Runner
*SMG speedster — fastest player on the server*

- +10% base movement speed
- Kill frenzy: speed boost after every kill
- **Skill:** `Turbo Charge` — x2 speed for 4s
- **Perks:** sprint · lightfeet · runningshot · frenzy · turbo

---

## 🔵 Counter-Terrorist Classes

### 🔧 Defuser
*Bomb squad specialist — defuse anything, anywhere*

- Faster defuse speed
- Heal HP on each successful defuse
- +Armor on spawn
- **Skill:** `EMP Burst` — +30 HP tactical advantage
- **Perks:** rapidkit · defuse_heal · hardened · emp · overwatch

### 🔭 Sniper
*AWP specialist — one shot, one kill*

- Bonus HP for patient positioning
- Extra XP rewards for AWP kills
- **Skill:** `Eagle Eye` — slowed but deadly precision mode for 6s
- **Perks:** sniper_scope · longshot · patience · eagleeye · oneshot

### 🛡️ Guardian
*Site anchor — hold positions, build fortitude*

- Bonus HP and armor on spawn
- Fortify: gain armor per kill while defending
- **Skill:** `Last Stand` — +40 HP + full armor surge
- **Perks:** fortify · ironwall · holdtheline · laststand · angelshield

### 📡 Recon
*SMG/intel specialist — fast, smart, dangerous*

- +8% base movement speed
- Tactical positioning bonuses
- **Skill:** `Tactical Sprint` — +60% speed + 15 HP for 5s
- **Perks:** agility · quickdraw · infiltrate · tacticalsprint · ghostsignal

---

## ⚡ Active Skills

Each class has a unique skill that **auto-fires at round start** and can also be triggered manually with `!skill` on a cooldown.

| Class | Skill | Effect | Cooldown |
|-------|-------|--------|----------|
| Bomber | Adrenaline Rush | +50% speed · 5s | 45s |
| Ghost | Shadow Step | +80% speed · 3s | 30s |
| Expert Shooter | Combat Stims | +25 HP | 40s |
| Runner | Turbo Charge | x2 speed · 4s | 35s |
| Defuser | EMP Burst | +30 HP | 50s |
| Sniper | Eagle Eye | Slow + precision · 6s | 60s |
| Guardian | Last Stand | +40 HP + full armor | 55s |
| Recon | Tactical Sprint | +60% speed + 15 HP · 5s | 35s |

---

## 🧩 Perk Upgrades

Each class has **5 perks**, each upgradeable **3 times**. Upgrades cost XP:

| Upgrade Tier | XP Cost |
|-------------|---------|
| Level 1 | 200 XP |
| Level 2 | 400 XP |
| Level 3 | 600 XP |

Use `!upgrade <perkname>` to spend XP on upgrades.

---

## 💬 Chat Commands

| Command | Description |
|---------|-------------|
| `!xpm` | Open the main XP Menu HUD |
| `!class` | Browse and select your class |
| `!class <name>` | Directly set your class (e.g. `!class bomber`) |
| `!perks` | View your class perks and upgrade status |
| `!skill` | Manually trigger your active skill |
| `!upgrade <perk>` | Upgrade a perk using XP |
| `!rank` | Display your level, XP, and class |
| `!top` | Show the top 10 players leaderboard |

---

## 🖼️ HUD System

The server uses CS2's built-in HTML center display for rich in-game menus:

- **Welcome screen** on connect showing your level and class
- **XPM main menu** (`!xpm`) — level, XP progress bar, class, skill cooldown
- **Class selector** — styled panel with all options for your team side
- **Perk viewer** — star ratings, unlock requirements, upgrade costs
- **Rank card** — big level display with XP progress bar
- **Skill activation popup** — shows skill name and effect on use
- **Level-up splash** — full-screen celebration with unlock info

---

## 🛠️ Server Stack

| Component | Version |
|-----------|---------|
| CS2 Dedicated Server | Latest |
| Metamod:Source | git1313 |
| CounterStrikeSharp | v1.0.364 |
| CS2RPG Plugin | v2.0.0 |
| Ranks Plugin | v2.0.5.5 |
| MariaDB | 11 (Podman container) |
| OS | Bazzite Linux (Fedora-based) |

---

## 📁 Plugin Architecture

```
csgo/addons/
├── metamod/                    # Metamod:Source
├── counterstrikesharp/
│   ├── plugins/
│   │   ├── CS2RPG/            # XP Mod RPG system
│   │   │   ├── CS2RPG.dll
│   │   │   └── rpg.json       # Player data (auto-saved)
│   │   └── Ranks/             # Rank display system
│   └── configs/
│       └── plugins/
│           └── RanksCore/
│               └── ranks.json
```

---

## 🗄️ Data Persistence

- Player XP, levels, class selection, and perk upgrades are saved to `rpg.json`
- Auto-saves every **5 minutes** and on player disconnect
- Rank stats stored in **MariaDB** via the Ranks plugin

---

## 🚀 Quick Start (Server Operators)

```bash
# Start the database
podman start mariadb-xpmod

# Launch the server
~/cs2/launch_cs2.sh &

# Connect from CS2 client
connect <server-ip>:27015
```

---

## 📜 License

This server configuration and CS2RPG plugin are custom-built for personal use.  
CS2 is property of Valve Corporation. CounterStrikeSharp is MIT licensed.

---

*Built with ❤️ on Bazzite Linux*
