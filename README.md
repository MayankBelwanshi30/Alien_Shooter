# Alien Shooter 
## Project Preview
![Gameplay Screenshot](screenshots/gameplay.png)

## Description
**Alien Shooter** is a top-down survival shooter built entirely as a **single self-contained HTML file** — no build step, no bundler, no dependencies. Just Canvas 2D, the Web Audio API, and vanilla JavaScript.

You wake up outside **St. Mercy Hospital**. Somewhere inside is a vaccine — nobody knows which room. Search the wards, fight through runners, crawlers, and tanks, find the vaccine, radio it in from the Radio Room, then fight your way across the building to the Exit Corridor before the chopper leaves without you.

Built to explore how far a browser game can go with **zero frameworks**: procedural floor rendering, room-by-room alien spawning, a breakable-wall shortcut system, and a fully synthesized + sample-based audio layer.

---
## Features
* Full loop-corridor hospital map with a sealed core and a **breakable-wall shortcut**
* Room-by-room alien reveal — doors trigger spawns only when you get close
* 3 weapons + a limited-use melee **Katana** finisher
* Vaccine → Radio Room → Exit Corridor three-stage mission structure
* Escalating post-radio-call survival phase with scaling alien spawns
* Pause menu (**ESC**) with a return-to-main-menu option
* Health, armor, and medkit pickup system
* Real sample-based SFX (gunfire, footsteps, reload, alien, radio, chopper) layered with lightweight synthesized hit/pickup sounds
* Menu music while browsing, a separate ambient loop while playing
* Level Select screen with 3 mission slots (1 playable, 2 coming soon)

---
## Screenshots

**Title Screen**
![Title Screen](screenshots/title_screen.png)

**Level Selection**
![Level Selection](screenshots/level_select.png)

**In-Game**
![Gameplay](screenshots/gameplay.png)

---
## Weapons

| Weapon | Damage | Magazine | Reserve | Fire Rate | Notes |
|---|---|---|---|---|---|
| **Pistol** | 32 | 12 | 192 | Semi-auto | Fast reload, reliable starter sidearm |
| **Assault Rifle** | 16 | 30 | 420 | Full-auto | High rate of fire, moderate spread |
| **Shotgun** | 11 × 8 pellets | 6 | 84 | Slow | Devastating up close, wide spread |
| **Katana** ⚔ | Instant kill | 3 charges | — | Melee | Kills every alien in a short radius around you, no ammo required |

Weapons are switched with **1 / 2 / 3**, the Katana is triggered with **Q**, and each has its own reload behavior — the pistol snaps back into action almost twice as fast as the rifle or shotgun.

---
## The Hospital

St. Mercy Hospital is built as a **loop corridor** wrapped around a sealed interior core, with rooms hanging off all four sides:

```
                 RECEPTION   WAITING HALL   LABORATORY
                     └───────────┬───────────┘
         SECURITY  ┌──────────────────────────────┐  ICU
                   │        (sealed core,         │
        RADIO ROOM │     breakable shortcut       │  EMERGENCY
                   │         through center)      │  WARD
                   └──────────────────────────────┘
                     ┌───────────┬───────────┐
               PHARMACY   STORAGE   GENERATOR   EXIT CORRIDOR
```

* **Reception** — your starting room
* **Laboratory / ICU / Emergency Ward / Generator Room** — the heaviest alien concentrations (crawlers & tanks)
* **Radio Room** — call in the vaccine once you've found it
* **Exit Corridor** — the extraction point, on the opposite side of the building from Reception
* **Sealed core shortcut** — a barricaded wall through the middle of the hospital that aliens (and bullets) can break open over time, creating a secret shortcut across the map

Once you call in the vaccine, the loop corridors become the arena for an escalating final stand as you fight your way to the Exit Corridor.

---
## Controls

| Key | Action |
|---|---|
| **WASD / Arrows** | Move |
| **Mouse** | Aim |
| **Click** | Fire |
| **R** | Reload |
| **1 / 2 / 3** | Pistol / Assault Rifle / Shotgun |
| **Q** | Katana (3 charges) |
| **E** | Interact (collect vaccine, call radio, escape) |
| **H** | Use medkit |
| **ESC** | Pause / Resume |
| **M** | Return to Main Menu (while paused or on an end screen) |

---
## Project Structure
```
alien-shooter-hospital/
├── game.html                 Entire game — HTML, CSS, and JS in one file
├── README.md
├── screenshots/
│   ├── title_screen.png
│   ├── level_select.png
│   └── gameplay.png
└── assets/
    ├── start.jpg              Title screen background
    ├── hospital1.jpg           Level 1 thumbnail
    ├── hospital2.jpg           Level 2 thumbnail (Courtyard)
    ├── hospital3.jpg           Level 3 thumbnail (Vilgax)
    ├── pistol.jpg              Weapon HUD icon
    ├── ar.jpg                  Weapon HUD icon
    ├── shotgun.jpg             Weapon HUD icon
    ├── Assets/soldier.png       Player sprite
    ├── Assets/alien4.png        Runner sprite
    ├── Assets/alien7.png        Crawler sprite
    ├── tank.png                Tank sprite
    ├── bgm.mp3                 Menu / loading music
    ├── creep.mp3               In-game ambient loop
    ├── pistol.mp3               Pistol fire
    ├── ar.mp3                   AR fire
    ├── shotgun.mp3              Shotgun fire
    ├── foot.mp3                 Footsteps
    ├── reload.mp3                Reload
    ├── alien.mp3                 Alien growl / reveal
    ├── radio.mp3                  Radio call
    └── heli.mp3                   Helicopter extraction
```

---
## Tech Stack
* **Rendering:** HTML5 Canvas 2D (no WebGL, no rendering libraries)
* **Audio:** Web Audio API for synthesized hit/pickup SFX + `<audio>` elements for sampled weapon, ambient, and event sounds
* **Language:** Vanilla JavaScript (ES6 classes, no framework, no bundler)
* **Fonts:** Google Fonts (Poppins)

---
## Getting Started
No install, no build step.

### 1. Get the files
```
git clone https://github.com/yourusername/alien-shooter-hospital.git
cd alien-shooter-hospital
```

### 2. Add the assets
Drop the image/audio files listed in **Project Structure** above into an `assets/` folder next to `game.html`.

### 3. Run it
Just open `game.html` in a browser — or serve it locally to avoid any file:// audio restrictions:
```
npx serve .
```
Then visit the local URL it prints.

---
## Future Improvements
* **Level 2 — Courtyard**: outdoor combat with open sightlines and different alien AI
* **Level 3 — Vilgax**: a boss-driven finale
* A real minimap instead of relying on memory of the loop layout
* More weapons (SMG, sniper rifle, grenade launcher)
* Persistent save/progress system across levels
* Difficulty settings and a New Game+ mode
* Controller and mobile touch-control support
* Proper sprite-sheet animation for the player and aliens instead of static rotated sprites
* Leaderboard / score persistence

---
## Learning Outcomes
* Structuring a full game loop (input → update → collision → render) in vanilla JS without a game engine
* Doorway-triggered, room-scoped enemy spawning driven by simple proximity checks
* Building a believable wall/collision system with axis-sliding movement and breakable barricades
* Mixing procedurally synthesized audio (Web Audio API buffers) with sampled `<audio>` playback for a layered sound design
* Managing screen/state flow (menu → level select → mission brief → game → pause → end screens) with plain DOM + CSS transitions alongside a canvas-rendered game
