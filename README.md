# ⚔️ XP MOD — CS2 Dedicated Server

> A fully custom **RPG perk system** for Counter-Strike 2, built on [CounterStrikeSharp](https://github.com/roflmuffin/CounterStrikeSharp) and [Metamod:Source](https://www.sourcemm.net/). Choose your class, earn XP, unlock perks, activate class skills, and prestige for permanent bonuses.

---

## 🖥️ Server Info

| Field | Value |
|-------|-------|
| **Hostname** | `[5X] XPMod` |
| **Map** | `de_dust2` (active rotation) |
| **Tickrate** | 128 |
| **Max Players** | 32 (16v16) |
| **Bots** | 32 bots, difficulty 2 |
| **Mode** | Casual |
| **Connect** | `connect <server-ip>:27015` |

---

## 🎮 RPG System Overview

XP Mod transforms CS2 into a full RPG experience. Every kill, assist, bomb plant, defuse, MVP, and round win earns you **XP** (5x multiplier). Level up to unlock class perks and a powerful active skill that **auto-activates every round start**. Reach Level 30 and **Prestige** for permanent stat bonuses.

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

> Prestige 3+ grants a 5% XP multiplier bonus per prestige tier above 2.

### 🏆 Level Milestones

| Level | Unlock |
|-------|--------|
| **1** | Tier 1 perks available |
| **5** | Active skill unlocked — auto-fires every round |
| **10** | Tier 2 perks available |
| **20** | Ultimate perks available |
| **30** | MAX LEVEL — `!prestige` available 👑 |

---

## ⭐ Prestige System

Reach **Level 30** and type `!prestige` to reset back to Level 1 in exchange for a permanent prestige badge and passive bonus. Max 5 prestiges.

| Prestige | Badge | Permanent Bonus |
|----------|-------|-----------------|
| 1 | `[*]` | +5 armor every spawn |
| 2 | `[**]` | +10 HP every spawn |
| 3 | `[***]` | +5% XP gain bonus |
| 4 | `[****]` | -10s skill cooldown |
| 5 | `[*****]` | All bonuses + legend status in top list |

- Your **class, perks, and prestige badge** are kept on reset
- Badge displays next to your name in `!xpm`, `!rank`, and `!top`
- Prestige bonuses **stack** — Prestige 5 has all of the above

---

## 🔴 Terrorist Classes

### 💣 Bomber
*C4 specialist — plant fast, blow everything up*

- Speed burst after planting C4
- Bonus HP on spawn at higher levels
- **Skill:** `Adrenaline Rush` — +50% speed for 5s (cooldown 45s)
- **Perks:** sprint · blastradius · ironwill · martyrdom · adrenaline

### 👻 Ghost
*Knife/stealth assassin — kill silently, heal on blood*

- Enhanced movement speed
- Vampirism: heal HP on every kill (unlocks Lv5)
- **Skill:** `Shadow Step` — +80% speed burst for 3s (cooldown 30s)
- **Perks:** stealth · vampirism · shadowblade · smokescreen · martyrdom

### 🎯 Expert Shooter
*Rifle/AR master — headshots reward you*

- Bonus max HP for rifle duels
- Speed burst after headshot kills (unlocks Lv5)
- **Skill:** `Combat Stims` — +25 HP injection (cooldown 40s)
- **Perks:** steadyaim · combatflow · hardenedbody · armorpiercer · stims

### 🏃 Runner
*SMG speedster — fastest player on the server*

- +10% base movement speed
- Kill frenzy: speed boost after every kill (unlocks Lv10)
- **Skill:** `Turbo Charge` — x2 speed for 4s (cooldown 35s)
- **Perks:** sprint · lightfeet · runningshot · frenzy · turbo

---

## 🔵 Counter-Terrorist Classes

### 🔧 Defuser
*Bomb squad specialist — defuse anything, anywhere*

- Faster defuse, heal HP on each successful defuse
- +Armor on spawn
- **Skill:** `EMP Burst` — +30 HP (cooldown 50s)
- **Perks:** rapidkit · defuse_heal · hardened · emp · overwatch

### 🔭 Sniper
*AWP specialist — one shot, one kill*

- Bonus HP for patient positioning
- Extra XP rewards for AWP kills
- **Skill:** `Eagle Eye` — slowed but deadly precision mode for 6s (cooldown 60s)
- **Perks:** sniper_scope · longshot · patience · eagleeye · oneshot

### 🛡️ Guardian
*Site anchor — hold positions, build fortitude*

- Bonus HP and armor on spawn
- Fortify: gain armor per kill while defending (unlocks Lv5)
- **Skill:** `Last Stand` — +40 HP + full armor surge (cooldown 55s)
- **Perks:** fortify · ironwall · holdtheline · laststand · angelshield

### 📡 Recon
*SMG/intel specialist — fast, smart, dangerous*

- +8% base movement speed
- Tactical positioning bonuses
- **Skill:** `Tactical Sprint` — +60% speed + 15 HP for 5s (cooldown 35s)
- **Perks:** agility · quickdraw · infiltrate · tacticalsprint · ghostsignal

---

## ⚡ Active Skills

Each class has a unique skill that **auto-fires at round start** (1.5s delay) and can also be triggered manually with `!skill` on a cooldown. Prestige 4 reduces all cooldowns by 10s.

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
| Level 1 → 2 | 200 XP |
| Level 2 → 3 | 400 XP |
| Level 3 → MAX | 600 XP |

Use `!upgrade <perkname>` or navigate via `!xpm → Perks` to upgrade directly in-menu.

---

## 💬 Chat Commands

| Command | Description |
|---------|-------------|
| `!xpm` | Open the main XP Menu (navigable with number keys) |
| `!class` | Browse and select your class |
| `!class <n>` | Directly set class (e.g. `!class bomber`) |
| `!perks` | View your perks and upgrade status |
| `!skill` | Manually trigger your active skill |
| `!upgrade <perk>` | Upgrade a perk using XP |
| `!rank` | Show your level, XP, prestige, and class |
| `!top` | Top 10 players leaderboard with prestige badges |
| `!prestige` | Prestige at Level 30 (confirmation menu) |

---

## 📋 XPM Menu System

Type `!xpm` to open the full interactive chat menu. Navigate with **number keys**:

```
 [XPM] [***] Lv18 | 38,850 XP | [########--]
 1. [ Class ] Guardian
 2. [ Perks ] Guardian
 3. [ Skill ] Last Stand | Ready
 4. [ Stats ] Level 18
 5. [ Top Players ]
 6. [ Close ]
```

Each sub-menu has a **Back** option to return to the main menu. The Perks menu lets you upgrade directly by selecting the perk number.

---

## 🛠️ Server Stack

| Component | Version |
|-----------|---------|
| CS2 Dedicated Server | Latest |
| Metamod:Source | git1313 |
| CounterStrikeSharp | v1.0.364 |
| CS2RPG Plugin | v3.0.0 |
| Ranks Plugin | v2.0.5.5 |
| MariaDB | 11 (Podman container) |
| OS | Bazzite Linux (Fedora-based) |

---

## 📁 Plugin Architecture

```
csgo/addons/
├── metamod/
├── counterstrikesharp/
│   ├── plugins/
│   │   ├── CS2RPG/
│   │   │   ├── CS2RPG.dll
│   │   │   └── rpg.json        # Player data (auto-saved)
│   │   └── Ranks/
│   └── configs/plugins/RanksCore/ranks.json
csgo/cfg/
├── server.cfg
├── custom_bots.cfg             # 32 bot fill
└── custom_all.cfg              # Gameplay overrides
```

---

## 🗄️ Data Persistence

- Player XP, levels, prestige, class, and perk upgrades saved to `rpg.json`
- Auto-saves every **5 minutes** and on player disconnect
- Rank stats stored in **MariaDB** via the Ranks plugin

---

## 🚀 Quick Start

```bash
podman start mariadb-xpmod
~/cs2/launch_cs2.sh &
# Then in CS2: connect <server-ip>:27015
```

---

## 📜 Changelog

### v3.0.0
- Full interactive `ChatMenu` — navigate with number keys
- `!xpm` hub with Class, Perks, Skill, Stats, Top submenus
- **Prestige system** — 5 tiers, permanent bonuses, badges in `!top`
- Skills auto-activate on round start
- Bot fix — weapons enabled, full buy money

### v2.0.0
- HTML center HUD menus
- Auto-skill on round start
- Welcome screen on connect

### v1.0.0
- Initial release — 8 classes, 5 perks each, XP system, Ranks integration

---

*Built with ❤️ on Bazzite Linux*
