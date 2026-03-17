# HeroesNeverDie

A tactical third-person shooter game built with **Unreal Engine 5.4**, set during the 1971 Indo-Pakistani War. Play as an elite hero operative navigating enemy territory with stealth, precision, and firepower.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Controls](#controls)
- [Characters](#characters)
- [Weapons](#weapons)
- [Enemy AI](#enemy-ai)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Building & Packaging](#building--packaging)
- [License](#license)

---

## Overview

**HeroesNeverDie** is a single-player tactical shooter set in 1971. Players control a hero character through enemy-occupied environments, using a combination of stealth takedowns, long-range shooting, and close-quarters combat. Enemies patrol routes and respond dynamically to the player's presence using an AI Behavior Tree system.

- **Engine:** Unreal Engine 5.4
- **Platform:** Windows (DirectX 12)
- **Scripting:** Blueprint Visual Scripting
- **Main Map:** `1971` — a large environment set in 1971

---

## Features

- **Third-person tactical shooter** with full cover and crouch mechanics
- **Stealth system** — assassination takedowns, crouch movement, and silenced weapons
- **40+ hero animations** — running, aiming, shooting, crouching, rolling, jumping, and more
- **Enemy AI** — patrol routes, behavior trees with alert/search/attack states
- **Weapon variety** — AR4, KA-47, KA-74U, KA-Val, SMG-11, M9 Knife, G67 Grenade
- **Weapon accessories** — red dot sights, suppressors, and grips
- **Healing system** — in-field health recovery
- **Inventory & Map UI** — in-game item management and map display
- **Quixel Megascans environment** — high-quality surface materials
- **Unreal Engine 5.4 Enhanced Input System** — full keyboard/mouse and gamepad support

---

## Prerequisites

- **Unreal Engine 5.4** — [Download from Epic Games Launcher](https://www.unrealengine.com/en-US/download)
- **Windows 10/11** with DirectX 12 support
- **GPU:** DirectX 12 compatible GPU (Shader Model 6)
- **RAM:** 16 GB or more recommended
- **Storage:** ~700 MB for the project

---

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/taxin1/HeroesNeverDie.git
   cd HeroesNeverDie
   ```

2. **Open the project in Unreal Engine 5.4:**
   - Launch the **Epic Games Launcher** and open **Unreal Engine 5.4**.
   - Click **Open Project** and navigate to `HERO.uproject`.
   - Allow Unreal Engine to compile shaders on first launch (this may take several minutes).

3. **Play in the editor:**
   - In the editor, make sure the **1971** map is loaded (`Content/Maps/1971.umap`).
   - Press the **Play** button (▶) to start a play-in-editor session.

---

## Controls

| Action | Keyboard / Mouse | Gamepad |
|---|---|---|
| Move | `W A S D` | Left Stick |
| Look | Mouse | Right Stick |
| Jump | `Space` | Face Button (Bottom) |
| Sprint | `Left Shift` | Left Stick Click |
| Crouch | `Left Ctrl` | Face Button (Right) |
| Roll / Dodge | `Q` | Left Bumper |
| Aim / Zoom | `Right Mouse Button` | Left Trigger |
| Shoot | `Left Mouse Button` | Right Trigger |
| Concentrate | `C` | D-Pad Down |
| Assassinate | `E` (near enemy) | Face Button (Top) |
| Throw Grenade | `G` | Right Bumper |
| Heal | `H` | D-Pad Up |
| Interact | `F` | Face Button (Left) |
| Inventory | `I` | D-Pad Left |
| Map | `M` | D-Pad Right |
| Pause | `Escape` | Start |

> Mouse sensitivity is set to `0.07` by default. Gamepad deadzone is `0.25`.  
> These values can be adjusted in `Config/DefaultInput.ini`.

---

## Characters

### Hero
- **Blueprint:** `Content/Characters/Hero/BP_Hero.uasset`
- **Model:** Ch15
- **Animation Blueprint:** `ABP_HeroAnimation.uasset`
- Features full body IK (foot placement), 40+ animations, and third-person camera setup.

### Enemy (Pakistani Soldier)
- **Blueprint:** `Content/Characters/Enemy/Pakistani/BP_Pakistani.uasset`
- **Model:** Ch49
- **AI Controller:** `AIC_Pakistani_AI.uasset`
- **Behavior Tree:** `BT_Pakistani.uasset`
- Uses patrol route following, line-of-sight detection, and reactive combat states.

### Human NPCs
- **Blueprint:** `Content/Characters/Human/BP_Human.uasset`
- Generic NPC characters that populate the environment.

---

## Weapons

| Weapon | Type | Notes |
|---|---|---|
| AR4 | Assault Rifle | Primary weapon |
| KA-47 | Assault Rifle | High damage |
| KA-74U | Assault Rifle (compact) | Faster handling |
| KA-Val | Silenced Rifle | Stealth primary |
| SMG-11 | Submachine Gun | Close-quarters |
| M9 Knife | Melee | Silent takedown |
| G67 Grenade | Explosive | Throwable |

Weapon blueprints are located in `Content/Weapons/`. Asset meshes and materials live in `Content/FPS_Weapon_Bundle/`.

---

## Enemy AI

Enemies use Unreal Engine's **Behavior Tree** system with a **Blackboard** for shared state.

**AI States:**
1. **Patrol** — Enemies follow waypoints defined by `BP_PatrolRoute`.
2. **Suspicious** — Enemy investigates last-known player position.
3. **Alerted / Combat** — Enemy engages the player and shoots.

**Key Blueprints:**
- `BT_Pakistani.uasset` — Behavior Tree root
- `BB_Pakistani.uasset` — Blackboard (stores focus target, patrol route, etc.)
- `BTT_MoveAlongPatrolRoute.uasset` — Patrol task
- `BTT_SetFocus.uasset` / `BTT_ClearFocus.uasset` — Attention control
- `BTTask_Shoot.uasset` — Combat shooting task
- `BTD_HasPatrolRoute.uasset` — Decorator for conditional patrolling

---

## Project Structure

```
HeroesNeverDie/
├── Config/                   # Engine, game, input, and editor configuration
├── Content/
│   ├── Assets/               # Character meshes and textures (Hero & Enemy)
│   ├── Blueprints/           # Game mode blueprint (1971GameMode)
│   ├── Characters/
│   │   ├── Hero/             # Player character blueprint and animations
│   │   ├── Enemy/            # Enemy blueprints, AI controller, behavior trees
│   │   └── Human/            # NPC blueprints
│   ├── FPS_Weapon_Bundle/    # Third-party weapon meshes, materials, and textures
│   ├── Input/                # Enhanced Input System actions and mappings
│   ├── Maps/                 # Main game level (1971.umap)
│   ├── Megascans/            # Quixel Megascans environment surfaces
│   └── Weapons/              # Weapon blueprints
├── HERO.uproject             # Unreal Engine 5.4 project descriptor
├── Intermediate/             # Compiled shader and build cache (auto-generated)
└── Saved/                    # Logs, crash reports, and auto-saves (auto-generated)
```

---

## Configuration

All configuration files are in the `Config/` directory:

| File | Purpose |
|---|---|
| `DefaultEngine.ini` | Rendering (DX12/SM6), audio, startup map, game mode |
| `DefaultGame.ini` | Project ID and game-specific settings |
| `DefaultInput.ini` | Mouse sensitivity, gamepad deadzone, key bindings |
| `DefaultEditor.ini` | Unreal Editor preferences |

**Key settings in `DefaultEngine.ini`:**
- Startup map: `/Game/Maps/1971`
- Default game mode: `1971GameMode`
- Shader model: `PCD3D_SM6` (DirectX 12)
- Audio sample rate: `48000 Hz`

---

## Building & Packaging

### Play in Editor
Open `HERO.uproject` in Unreal Engine 5.4 and press **Play**.

### Package for Windows
1. In the Unreal Editor, go to **Platforms → Windows → Package Project**.
2. Choose an output directory.
3. Wait for the packaging process to complete.
4. Run the generated `.exe` from the output folder.

### Command-line packaging
```bash
"<UE5_Install_Dir>\Engine\Build\BatchFiles\RunUAT.bat" BuildCookRun ^
  -project="<path_to>\HERO.uproject" ^
  -noP4 -platform=Win64 -clientconfig=Shipping ^
  -cook -build -stage -pak -archive ^
  -archivedirectory="<output_dir>"
```

---

## License

This project is for personal and educational use. Third-party assets (Quixel Megascans, FPS Weapon Bundle) are subject to their respective licenses from the Unreal Engine Marketplace and Epic Games.
