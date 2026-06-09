# 🎮 XPM RPG — CS2 Dedicated Server

> A fully custom RPG progression system built on top of Counter-Strike 2. Level up, choose a class, unlock skills, buy perks, prestige, and climb to Master Level 1000 — all while playing against adaptive bots on a private LAN server.

[![Platform](https://img.shields.io/badge/platform-Windows%2011-blue)]()
[![CS2](https://img.shields.io/badge/game-CS2-orange)]()
[![CSS](https://img.shields.io/badge/CounterStrikeSharp-1.0.369-green)]()
[![.NET](https://img.shields.io/badge/.NET-10.0-purple)]()

---

## 📋 Table of Contents

- [Overview](#overview)
- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [📁 Project Structure](#-project-structure)
- [🚀 Setup & Installation](#-setup--installation)
- [▶️ Running the Server](#️-running-the-server)
- [⚙️ Configuration](#️-configuration)
- [🧙 RPG System](#-rpg-system)
- [🏆 Prestige & Master Prestige](#-prestige--master-prestige)
- [🛒 Token Shop](#-token-shop)
- [📟 Commands](#-commands)
- [🖥️ HUD System](#️-hud-system)
- [📡 HTTP API](#-http-api)
- [🗄️ Data & Persistence](#️-data--persistence)
- [🤖 Bot Difficulty System](#-bot-difficulty-system)
- [✅ QoL Improvements](#-qol-improvements)
- [🔒 Security](#-security)
- [📝 Logging](#-logging)
- [📦 Building & Deploying](#-building--deploying)
- [🔮 Future Ideas](#-future-ideas)

---

## Overview

**XPM RPG** is a CounterStrikeSharp plugin that transforms a private CS2 LAN server into a full RPG experience. Players earn XP from in-game actions, level up, pick a team-locked class, upgrade perks, activate unique skills, and prestige through 10 tiers — then enter **Master Prestige**, a 1000-level grind with milestone rank icons. A cosmetic token shop rewards long-term play with chat tags, name colors, and kill banner styles.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🧙 **8 Team-Locked Classes** | 4 T-side, 4 CT-side — each with a unique active skill and passive bonuses |
| 📈 **XP & Leveling** | Kills, headshots, assists, bomb events, wins, and MVPs all award XP at 5× base |
| 🔮 **Perk Trees** | 5 perks per class × 3 ranks — permanently upgrade stats with XP |
| ⚡ **Active Skills** | Unlocked at Level 5, tracked with a live cooldown bar in the HUD |
| ⭐ **Prestige P1–P10** | 10 prestige tiers with stacking armor, HP, XP rate, and cooldown bonuses |
| 🏆 **Master Prestige** | CoD BO3-style Level 1–1000 with 10 milestone tiers, unique icons, and token rewards |
| 🛒 **Cosmetic Shop** | Earn tokens through play — buy chat tags, name colors, kill banner styles |
| 🤖 **Adaptive Bots** | 5 difficulty tiers auto-scaled to the human player's current level |
| 🖥️ **Live Center HUD** | Skill bar, XP progress, perks, kills, multiplier — all rendered in-screen |
| 🌐 **Panorama + HTTP API** | Custom Panorama layout + `localhost:34824` endpoint for streaming overlays |
| 💾 **Crash-Safe Saves** | Atomic JSON writes with automatic `.bak` recovery file |
| 🔄 **Map Rotation Safety** | Plugin-level match-end handler prevents server hang after game over |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Game | CS2 Dedicated Server (Build 10772+) |
| Plugin Framework | Metamod:Source 2.0.0-dev |
| Plugin API | CounterStrikeSharp 1.0.369 |
| Language | C# / .NET 10 |
| Data | JSON via System.Text.Json |
| HUD | CS2 Panorama (XML / JS / CSS) |
| API | .NET HttpListener |
| OS | Windows 11 x64 |

---

## 📁 Project Structure
C:\CS2Server
├── launch.bat # Interactive launcher — mode/map selector
│
├── CS2Build\CS2RPG
│ ├── CS2RPG.cs # Main plugin: XP, classes, skills, HUD, shop
│ ├── XPMPlayer.cs # Player data model (serialized to rpg.json)
│ ├── PlayerManager.cs # Thread-safe load/save with atomic writes
│ └── CS2RPG.csproj # Build config + auto-deploy post-build target
│
└── game\csgo
├── mapcycle.txt # Map rotation (plain names only — no comments)
├── cfg
│ ├── server.cfg # Core settings: hostname, rates, RCON
│ ├── xpm_mode_selected.cfg # Written by launch.bat at startup
│ ├── xpm_dm.cfg # Deathmatch overrides
│ ├── xpm_12v12.cfg # Casual 12v12 overrides
│ ├── xpm_competitive.cfg # Competitive 5v5 overrides
│ ├── my_bot_normal_config.cfg # Shared bot AI baseline
│ ├── xpm_bots_tier1.cfg # Beginner — Lv 1-2, vision 6,000
│ ├── xpm_bots_tier2.cfg # Intermediate — Lv 3-5, vision 10,000
│ ├── xpm_bots_tier3.cfg # Advanced — Lv 6-10, vision 18,000
│ ├── xpm_bots_tier4.cfg # Expert — Lv 11-25, vision 25,000
│ └── xpm_bots_tier5.cfg # Elite — Lv 26+, vision 30,000
├── panorama
│ ├── layout\xpm_hud.xml # Panel definitions
│ ├── scripts\xpm_hud.js # Event listeners, XP table, null guards
│ └── styles\xpm.css
└── addons\counterstrikesharp
└── plugins\CS2RPG
├── CS2RPG.dll # Compiled plugin (auto-deployed on build)
└── rpg.json # Live player data

---
## 🚀 Setup & Installation
### Prerequisites
- Windows 10/11 x64
- [SteamCMD](https://developer.valvesoftware.com/wiki/SteamCMD) to install CS2 server
- [.NET 10 SDK](https://dotnet.microsoft.com/download)
- [Metamod:Source](https://www.sourcemm.net/downloads.php?branch=master) (install first)
- [CounterStrikeSharp 1.0.369](https://github.com/roflmuffin/CounterStrikeSharp/releases)
### Steps
**1. Install CS2 Dedicated Server**
```cmd
steamcmd +login anonymous +force_install_dir C:\CS2Server +app_update 730 validate +quit
2. Install Metamod:Source

Extract to game\csgo\addons\metamod\ and create game\csgo\addons\metamod.vdf:

"Plugin" { "file" "../csgo/addons/metamod/bin/win64/server" }
3. Install CounterStrikeSharp

Extract the counterstrikesharp folder into game\csgo\addons\.

4. Build & Deploy the Plugin

cd C:\CS2Server\CS2Build\CS2RPG
dotnet build -c Release
The .csproj post-build target auto-copies the DLL to the plugins folder. No manual copy needed.

5. Place Config Files

All .cfg files → game\csgo\cfg\
xpm_hud.xml → game\csgo\panorama\layout\
xpm_hud.js → game\csgo\panorama\scripts\
xpm.css → game\csgo\panorama\styles\
Skill PNGs → game\csgo\panorama\images\xpm\
▶️ Running the Server
Interactive (Recommended)
C:\CS2Server\launch.bat
Select game mode, then map. The launcher writes xpm_mode_selected.cfg and starts CS2.

Direct Launch
"C:\CS2Server\game\bin\win64\cs2.exe" -dedicated -port 27015 -tickrate 128 +sv_lan 1 +game_type 1 +game_mode 2 +map ar_pool_day +exec server.cfg -insecure -console
Connect (Client)
connect 192.168.68.121:27015
⚙️ Configuration
server.cfg Key Settings
Setting	Value	Notes
sv_lan	1	LAN-only, no VAC
sv_cheats	1	Required for bot vision cvars
sv_maxrate	0	Unlimited (LAN)
sv_minrate	128000	Minimum client rate
rcon_password	xpm_rcon_lan_2026	Change before use
⚠️ sv_minupdaterate, sv_maxupdaterate, sv_mincmdrate, sv_maxcmdrate do not exist in CS2 — they are CS:GO-only and will produce Unknown command errors.

Game Modes
Mode	game_type	game_mode	Bot Quota
Deathmatch	1	2	22
Arms Race	1	0	22
Casual 12v12	0	0	22
Competitive 5v5	0	1	9
mapcycle.txt
⚠️ CS2 treats every non-blank line as a map name — // comments are NOT supported and will cause map rotation to fail. Use plain names only.

de_dust2
de_mirage
de_inferno
de_nuke
de_ancient
de_anubis
de_vertigo
de_train
de_overpass
de_cache
cs_office
cs_italy
ar_baggage
ar_pool_day
ar_shoots
🧙 RPG System
Classes (Team-Locked)
Players can only select classes matching their current side. On team switch, the plugin auto-reassigns at next spawn.

Terrorist Side
Class	Skill	Effect	Cooldown
Bomber	Adrenaline Rush	+50% speed for 5s	45s
Ghost	Shadow Step	+80% speed for 3s	30s
Expert Shooter	Combat Stims	Accuracy burst for 5s	35s
Runner	Turbo Charge	+100% speed for 4s	40s
Counter-Terrorist Side
Class	Skill	Effect	Cooldown
Defuser	EMP Burst	Slows nearby enemies 4s	50s
Sniper	Eagle Eye	No sway + zoom boost 6s	45s
Guardian	Last Stand	+50 HP regen burst 3s	60s
Recon	Tactical Sprint	+70% speed, silent 4s	35s
XP Sources
Action	Base XP
Kill	100
Headshot bonus	+50
Knife kill bonus	+75
AWP kill bonus	+100
Assist	40
Bomb plant	100
Bomb defuse	150
Round win	200
MVP	250
Base multiplier: 5×
With Prestige 3+ bonus: 5 × (1.0 + min((prestige - 2) × 0.05, 0.40))
Max (Prestige 10): 7.0×

Level Thresholds (Levels 1–30)
Lv	XP	Lv	XP	Lv	XP
1	0	11	28,000	21	74,500
2	1,000	12	32,500	22	81,000
3	2,500	13	37,000	23	87,500
4	4,500	14	41,500	24	94,000
5	7,000	15	46,000	25	100,500
6	10,000	16	50,500	26	107,000
7	13,500	17	55,000	27	113,500
8	17,000	18	59,500	28	120,000
9	20,500	19	64,000	29	126,500
10	24,000	20	68,500	30	133,000
Perks
5 perks per class, 3 ranks each. XP costs: 200 → 400 → 600 per rank.

!respec refunds 90% of all invested XP.

🏆 Prestige & Master Prestige
Prestige P1–P10
Use !prestige at Level 30. Level resets to 1; perks, tokens, and shop items are kept.

Prestige	Badge	Color	Bonus
P1	★	White	+5 armor/spawn
P2	★★	White	+10 HP/spawn
P3	★★★	White	+5% XP multiplier
P4	★★★★	White	−10s skill cooldown
P5	★★★★★	Gold	+3 tokens · Phantom tag unlocked
P6	◆	Blue	+10 more armor (total +15)
P7	◆◆	Blue	−5s more cooldown (total −15s)
P8	◆◆◆	Blue	+10% more XP mult (total +15%)
P9	◆◆◆◆	Blue	+10 more HP (total +20 HP)
P10	[Ω]	Gold	All bonuses · Champion tag unlocked
Master Prestige (Level 1–1000)
After P10 + Level 30, a second !prestige enters Master Prestige (+10 tokens, level resets to 1, cap becomes 1000). No further resets.

XP per level (formula-based):

Range	XP/Level	Total at Cap
Lv 31–100	+5,000	~483K at Lv 100
Lv 101–200	+8,000	~1.3M at Lv 200
Lv 201–500	+12,000	~4.9M at Lv 500
Lv 501–1000	+20,000	~14.9M at Lv 1000
Milestone Tiers (every 100 levels):

Levels	Symbol	Color	Tier	Tokens
1–99	[M]	Silver	Initiate	—
100–199	[★]	Gold	Marksman	+1
200–299	[◆]	Cyan Blue	Expert	+2
300–399	[✦]	Purple	Elite	+2
400–499	[⚔]	Red	Veteran	+2
500–599	[◆◆]	Blue	Legend	+3
600–699	[★★]	Orange	Champion	+3
700–799	[◆◆◆]	Cyan	Mythic	+4
800–899	[★★★]	Magenta	Immortal	+4
900–999	[Ω]	Orange-Red	Transcendent	+5
1000	[★ MASTER ★]	Gold	THE MASTER	+25
Each milestone triggers a double server-wide broadcast + 10-second center HUD celebration banner. Level 1000 is a triple broadcast.

🛒 Token Shop
Earning Tokens
Source	Amount
Every level gained	+1
Prestige P1–P4, P6–P9	+3
Prestige P5	+5
Prestige P10	+10
Enter Master Prestige	+10 (one-time)
Master milestones (100, 200 … 900)	+1 to +5
Master Level 1000	+25
5-kill streak	+1
Buy with XP (3K / 8K / 25K XP)	1 / 3 / 10 tokens
Shop Items
Chat Tags (cosmetic prefix on kill announcements and chat):

Tag	Cost	Prestige Req
[Recruit]	5	—
[Soldier]	10	—
[Veteran]	20	—
[Elite]	30	P1+
[Slayer]	40	P1+
[★ Legend]	60	P3+
[Phantom]	80	P5+
[✦ Mythic]	105	P7+
[⚔ Champion]	135	P10+
Name Colors: Gold, Sky Blue, Lime, Orange (20 tokens) · Crimson, Purple (25 tokens)

Kill Banner Styles:

Style	Cost	Effect
Default	Free	[XPM] Name — ⚡ TRIPLE KILL!
Compact	5	No [XPM] prefix
Dramatic	15	Includes class + level
Silent	10	No announcements
📟 Commands
Chat	Console	Description
!xpm	css_xpm	Main menu
!class	css_class	Class selection (team-filtered)
!perks	css_perks	Perk upgrade menu
!skill	css_skill	Activate skill
!rank	css_rank	Show rank card
!top	css_top	Top 10 leaderboard
!prestige	css_prestige	Prestige / enter Master / view Master tier
!respec	css_respec	Refund all perks (90% XP returned)
!shop	css_shop	Cosmetic shop
!tokens	css_tokens	Token count + equipped cosmetics
!map	css_map	Change map
!mode	css_mode	Change game mode
—	css_addbot	Add a bot
—	css_kickbot	Kick a bot
—	css_restartgame	Restart round
—	css_nextmap	Map selection menu
🖥️ HUD System
The center HUD is rendered via CSS's PrintToCenterHtml — pushed on spawn and refreshed while alive.

╔══════════════════════════════════════╗
║  ⚡ RUNNER    Lv 12  ◆ Expert M234  ║  Class · Level · Badge
║  [████████░░]  38,500 XP  +1,500    ║  XP bar · total XP · to next level
╠══════════════════════════════════════╣
║  ⚡ TURBO CHARGE  [████░░░░░░] 18s  ║  Skill name + cooldown bar + timer
║  +100% speed for 4s                  ║  Skill description
╠══════════════════════════════════════╣
║  Perks 4/15 · Kills 3 · P2 · ×5.0  ║  Stats row
╠══════════════════════════════════════╣
║  Kill+100  HS+50  Defuse+150  Win+200║  XP sources
║  Bot Tier: Advanced · Side: T        ║  Bot tier + side
╚══════════════════════════════════════╝
Master Prestige players get a tier-colored border (e.g. cyan for Mythic) and a tier symbol in the level display
Notifications (XP gain, level-up, skill activate) appear for 4–10 seconds between the stats and footer rows
📡 HTTP API
The plugin hosts a lightweight HTTP server:

http://127.0.0.1:34824/xpm-data?steamid=<STEAM64_ID>
Example response:

{
  "playerName": "XP",
  "level": 12,
  "totalXP": 38500,
  "currentXP": 6000,
  "nextLevelXP": 4500,
  "className": "Runner",
  "skillName": "Turbo Charge",
  "skillCooldown": 12.4,
  "skillReady": false,
  "prestige": 2,
  "perksTotal": 4,
  "perksMax": 15,
  "multiplier": 5.0
}
Used by LHM and other streaming overlay tools. Bound to localhost only — not externally accessible.

Ports:

Port	Use
27015	CS2 game traffic (UDP/TCP)
34824	XPM HUD API (localhost HTTP)
🗄️ Data & Persistence
rpg.json Schema
{
  "SteamId": "76561199386889933",
  "PlayerName": "XP",
  "Level": 12,
  "TotalXP": 38500,
  "ClassId": 3,
  "Prestige": 2,
  "IsMasterPrestige": false,
  "LifetimeXP": 250000,
  "Perks": { "sprint": 2, "frenzy": 1 },
  "Tokens": 14,
  "ShopOwned": { "tag_2": 1, "color_1": 1 },
  "ChatTagId": 2,
  "NameColorId": 1,
  "KillBannerStyle": 1
}
Save Triggers
Trigger	Method
Player disconnect (if changed)	SaveAllPlayers()
Every 5 minutes	SaveDirtyPlayers()
Match end	SaveAllPlayers()
Prestige confirmed	SaveAllPlayers()
Plugin unload	SaveAllPlayers()
Atomic Write
File.WriteAllText(dataFile + ".tmp", json);
File.Replace(dataFile + ".tmp", dataFile, dataFile + ".bak");
rpg.json is always either the previous complete save or the new one — never corrupted. rpg.json.bak is automatic one-step recovery.

Thread Safety
PlayerManager uses ReaderWriterLockSlim — multiple readers allowed concurrently, writes are exclusive. This protects against races between the main CSS thread and the HTTP API background task.

🤖 Bot Difficulty System
At every round start and player connect, the plugin finds the highest-level human player and applies the matching tier config:

Tier	Level Range	Vision Range	Config File
1 — Beginner	Lv 1–2	6,000	xpm_bots_tier1.cfg
2 — Intermediate	Lv 3–5	10,000	xpm_bots_tier2.cfg
3 — Advanced	Lv 6–10	18,000	xpm_bots_tier3.cfg
4 — Expert	Lv 11–25	25,000	xpm_bots_tier4.cfg
5 — Elite	Lv 26+ / Master	30,000	xpm_bots_tier5.cfg
Current tier is displayed in the center HUD footer.

✅ QoL Improvements
Every improvement was made to fix a real bug or meaningfully reduce friction.

#	Improvement	Problem Solved
1	Auto-deploy post-build	Eliminated manual DLL copy step — dotnet build -c Release now does everything
2	Atomic JSON saves	Crash mid-write used to corrupt rpg.json entirely; .tmp → .replace + .bak prevents data loss
3	ReaderWriterLockSlim	HTTP API thread and main game thread could race on player dict; now fully thread-safe
4	Memory leak fix on disconnect	_skillCooldownUntil, _skillActiveUntil, _hudNotif were never cleaned up — fixed
5	DateTime-based skill cooldown	Float decrement drifted under server load; DateTime.UtcNow diff is always exact
6	ApplySpeedBoost base speed fix	Runner/Recon class-specific speed perks were ignored on boost expiry — now uses shared helper
7	Class team-locking + auto-reassign	Players could pick CT classes as T; broken perks, exploits, and confusion — now enforced everywhere
8	ShowMainMenu reads live cooldown	Menu showed READY mid-cooldown because it read a stale float — now uses DateTime dict
9	Compact HUD redesign	Old skill section was 5 lines tall and cut off the bottom; redesigned to fit on screen with more info
10	Bot tier in HUD footer	No passive way to know current bot difficulty — now always visible
11	Master Prestige tier-colored HUD	Tier-colored border/header gives visual identity to rare ranks
12	Exact XP table in Panorama JS	Estimated formula produced wrong XP bar values; replaced with the same array the C# plugin uses
13	safePanel() null guards	Missing Panorama panel crashed the whole JS update loop silently; now logs the panel name
14	Rotating MOTD tips on connect	New players had no guidance; 8 rotating tips cover all key commands
15	Kill streak style shop item	Announcemnets are now a cosmetic choice rather than forced — Compact, Dramatic, or Silent
16	Chat tag injection via say listener	Tags appear in actual chat, not just kill announcements — makes cosmetic feel real
17	Removed dead CS:GO cvars	sv_minupdaterate etc. don't exist in CS2 — removed to stop Unknown command log spam
18	Removed client cvars from bot config	cl_interp_ratio, rate, bind in a server cfg file generated constant console noise
19	Fixed mapcycle.txt comments	// lines were parsed as map names, exhausted valid maps, and crashed map rotation
20	Map rotation safety net	EventCsWinPanelMatch saves players and sets a 25s watchdog changelevel with STOP_ON_MAPCHANGE
21	Graduated bot vision range	Tier 1→2 was a 3× jump (4K→12K); smoothed to 6K→10K to avoid a jarring difficulty spike
🔒 Security
Measure	Detail
sv_lan 1	Server not listed publicly; no VAC enforcement
LAN binding	Server binds to 192.168.68.121:27015 — not reachable from internet
HTTP API localhost-only	127.0.0.1:34824 — not accessible outside the server machine
RCON password	Set in server.cfg — change xpm_rcon_lan_2026 before first use
No admin gating	css_addbot etc. have no permission checks — acceptable for trusted LAN; add CSS admin flags for wider use
Atomic file writes	Prevents rpg.json corruption from crashes or power loss
📝 Logging
All plugin output uses CSS structured logging and appears in the server console and game\csgo\logs\YYYY_MM_DD_HHMMSS.log.

Key log lines:

[XPM] Loaded 14 players from rpg.json
[XPM] HUD API server started on http://127.0.0.1:34824/
[XPM] XP leveled up to 5
[XPM] XP prestiged to Prestige 2
[XPM] XP hit Master Level 100 (Marksman)
[XPM] Match over — players saved. Scheduling safety map rotation in 25s.
[XPM Bots] Tier applied: Advanced (Elo 1201-1500) (Lv9) — xpm_bots_tier3.cfg
Expected noise (safe to ignore):

Message	Reason
Could not PreloadLibrary ... Access violation	CS2 engine can't preload .NET DLLs — CSS handles this itself
Unknown command 'mp_weapons_glow_on_ground'	Inside CS2's own gamemode_deathmatch.cfg, not our code
CNavMesh::TestRayToMesh error	ar_pool_day nav mesh quirk — no gameplay impact
[AI BT]: Unable to buy after multiple attempts	Bot timing issue in continuous-respawn mode — harmless
📦 Building & Deploying
cd C:\CS2Server\CS2Build\CS2RPG
dotnet build -c Release
The post-build target in CS2RPG.csproj auto-copies the DLL:

[XPM] Deployed CS2RPG.dll to plugins folder.
Build succeeded. 0 Warning(s) 0 Error(s)
Post-Change Checklist
not done
!xpm menu opens correctly
not done
Level-up fires at correct XP thresholds
not done
!prestige works at Lv 30; Master entry works at P10 Lv 30
not done
Master milestone broadcast fires at Lv 100, 200 …
not done
!shop shows correct token balance and owned items
not done
Chat tag appears in kill announcements and say
not done
Kill streak announces at 3/4/5 kills
not done
!respec returns 90% XP correctly
not done
Wrong-team class selection is blocked
not done
HUD center panel shows without bottom cutoff
not done
rpg.json.bak exists after a save
not done
Map rotation works after match end (no hang)
🔮 Future Ideas
Idea	Complexity
CSS admin flag gating on admin commands	Low
Daily first-kill XP bonus	Medium
Leaderboard web page from the HTTP API	Medium
Prestige-gated perk tiers (enforce existing tier variable)	Low
Per-map bot config overrides	Low
Squad XP bonus when multiple humans on same team	Medium
CS2-Tags plugin integration for native chat prefixes	Low
Full CS2-SimpleAdmin integration	Low
🤝 Contributing
Branch off main for any change
Build with dotnet build -c Release — auto-deploy confirms success
Run the post-change checklist above
Never commit rpg.json (live player data) or rcon_password values
New per-player runtime state goes in CS2RPG.cs as Dictionary<ulong, T> with cleanup in OnPlayerDisconnect
New persisted state goes in XPMPlayer.cs with a sensible non-null default
📄 License
Private project — no public license applied.

CS2 and Counter-Strike are trademarks of Valve Corporation.
CounterStrikeSharp by roflmuffin — MIT License.
Metamod:Source by AlliedModders — Open Source.
