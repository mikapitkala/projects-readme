# kood / Melee

**Newtonian Combat Arena** - A browser-based multiplayer space combat game for 2-4 players.

Inspired by [Star Control 2 SuperMelee](https://en.wikipedia.org/wiki/Star_Control_II), this game features Newtonian(ish) physics, diverse ship loadouts, and intense real-time battles. Built entirely with DOM elements - no canvas, no images.

---

## Technical Highlights

This project pushes the boundaries of what's possible with pure HTML, CSS, and JavaScript:

- **Zero Images** - Every visual element is rendered with CSS. Ships are font glyphs, explosions are gradients and box-shadows, stars are procedural dots.
- **Ok,** ***One*** **Image** - We did make a favicon, but it's a screenshot of the CSS logo
- **No Canvas** - The entire game uses DOM elements with CSS transforms for rendering. Hardware-accelerated via `will-change: transform`.
- **Ships Are Letters** - Each hull type is a single character (V, W, Y, A, C, U) from a pixel font, rotated and styled with CSS.
- **Newtonian Physics** - Optional full Newtonian(ish) mechanics with no drag. Ships drift forever until you thrust in the opposite direction. There is a top speed though.
- **Spatial Audio** - Web Audio API with 3D positioning. Sounds pan based on where they occur relative to your view.
- **Dynamic Music** - Three music layers blend in real-time based on combat intensity.

---

## Quick Start

### Requirements

- Node.js (v18+)
- A modern browser (Chrome, Firefox, Edge, maybe even Safari)

### Installation

```bash
git clone https://gitea.kood.tech/mikapitkala/multi-player
cd multi-player
npm install
```

### Running Locally

```bash
node server.js
```

Open http://localhost:3000 in your browser.

### Online Multiplayer

We have an online server hosted on ngrok available for testing [here](https://8d360f39e2ce.ngrok-free.app/)

#### Hosting a server yourself on ngrok

To play with friends over the internet, expose your local server using [ngrok](https://ngrok.com/):

```bash
ngrok http 3000
```

Share the generated URL with your friends. Each player opens the URL in their browser, enters a unique name, and joins the lobby.

You can obviously host it on many different clouds, like Heroku, Render.com, Fly.io, Digital Ocean and so on.

---

## Controls

### Local Multiplayer

#### Player 1 (WASD)

| Action | Key |
|--------|-----|
| Thrust | W |
| Rotate Left | A |
| Rotate Right | D |
| Fire Primary | Space |
| Fire Secondary | Left Shift |

#### Player 2 (Arrow Keys)

| Action | Key |
|--------|-----|
| Thrust | ↑ |
| Rotate Left | ← |
| Rotate Right | → |
| Fire Primary | Enter |
| Fire Secondary | Right Shift |

#### Player 3 (IJKL)

| Action | Key |
|--------|-----|
| Thrust | I |
| Rotate Left | J |
| Rotate Right | L |
| Fire Primary | O |
| Fire Secondary | P |

#### Player 4 (Numpad)

| Action | Key |
|--------|-----|
| Thrust | Numpad 8 |
| Rotate Left | Numpad 4 |
| Rotate Right | Numpad 6 |
| Fire Primary | Numpad 0 |
| Fire Secondary | Numpad Enter |

#### General

| Action | Key |
|--------|-----|
| Pause Menu | ESC |

#### Respawn Menu

| Action | Key |
|--------|-----|
| Select ship | rotate left - rotate right |
| Select secondary | thrust - down |

### Online Multiplayer

#### Player (WASD)

| Action | Key |
|--------|-----|
| Thrust | W |
| Rotate Left | A |
| Rotate Right | D |
| Fire Primary | Space |
| Fire Secondary | Left Shift |

#### Respawn Menu (WASD)

| Action | Key |
|--------|-----|
| Select ship | A D |
| Select secondary | W S |

#### General

| Action | Key |
|--------|-----|
| Pause Menu | ESC |


---

## Gameplay

### Game Modes

| Mode | Description |
|------|-------------|
| **Deathmatch** | Score points by destroying enemies. Highest score when time runs out wins. Respawn on death. |
| **Last Ship Standing** | Each player has limited lives. Last player alive wins. |
| **Sudden Death** | One life only, one shot is all it takes. All players use **Glass Cannon** hulls with **Railguns** and Afterburners. Physics set to **Advanced** |

### Physics Presets

| Preset | Description |
|--------|-------------|
| Beginner | Strong drag, arcade-like handling |
| Medium | Light drag, balanced feel |
| Advanced | No drag - full Newtonian physics |

### Gameplay Features

- **Energy Management** - Weapons and abilities drain energy from your reactor. Energy recharges over time based on your hull's Recharge stat. Run dry and you're defenseless until it recovers.
- **Arena Wrapping** - The arena has no walls. Fly off one edge and you'll appear on the opposite side. If you get to the very edge of the arena, you'll bounce back in the opposite direction.
- **Dynamic Camera** - The camera automatically zooms and pans to keep all ships in view. In tight duels it zooms in close; when ships spread out, it pulls back for a wider view.
- **Collision Damage** - Ships that collide take damage and bounce off each other. Ramming can be a valid (if risky) tactic.
- **Gravity Well** - A large celestial body placed randomly on the arena generates inverse-square gravity. Use it for slingshot maneuvers or to drag enemies to their doom. Can be toggled off in match settings.
- **Respawn Loadout** - When respawning, you can change your ship and secondary ability. Use the directional keys to browse options before spawning back in Local games and pick from the menu Online. You have 5 seconds before your respawn

### Ship Hulls

Each hull has different stats: Armor (A), Reactor (R), Recharge (C), Thrust (T), and Agility (G).

| Hull | Symbol | A | R | C | T | G | Specialty |
|------|--------|---|---|---|---|---|-----------|
| Baseline Fighter | V | 5 | 5 | 5 | 5 | 5 | Balanced all-rounder |
| Heavy Dreadnought | W | 10 | 6 | 2 | 2 | 3 | Slow but heavily armored |
| Glass Cannon | Y | 2 | 8 | 2 | 6 | 6 | Fragile but powerful |
| Interceptor | A | 3 | 5 | 3 | 8 | 6 | Fastest acceleration |
| Dogfighter | C | 4 | 6 | 3 | 4 | 8 | Superior maneuverability |
| Sustain Fighter | U | 4 | 5 | 7 | 5 | 4 | Rapid energy regeneration |

### Primary Weapons

| Weapon | Description |
|--------|-------------|
| Autocannon | Medium range fast-firing projectiles |
| Railgun | Very high damage, extremely fast long range projectile with slow fire rate |
| Missile | Powerful homing missiles |
| Flak Cannon | Short range spread of 7 projectiles |

### Secondary Abilities

| Ability | Description |
|---------|-------------|
| Shield Pulse | Brief invulnerability window, time it well to get some Power back |
| Afterburner | 3x speed boost, drains energy |
| Point Defense | Auto-targets incoming projectiles, but can track a limited amount of them |
| EMP Mine | Drops mine that stuns enemies. Stunned enemies can't maneuver and take double damage |
| Gravity Anchor | Generate a powerful gravity well, stop instantly and pull in enemy ships |
| Rear Guns | Fire primary weapon backwards |

### Archetypes

12 pre-built loadouts combining hulls and weapons, plus a Random option:

| Hull | Primary | Playstyle |
|------|---------|-----------|
| Baseline | Autocannon | Solid all-rounder. Good for learning the ropes. |
| Baseline | Flak | Brawler. Get in close and shred. |
| Dreadnought | Railgun | Siege tank. Line up shots while absorbing hits. |
| Dreadnought | Flak | Slow bruiser. Waddle in and unleash hell. |
| Glass Cannon | Railgun | One-shot sniper. Hit or be hit. |
| Glass Cannon | Missile | Hit-and-run. Fire and evade. |
| Interceptor | Autocannon | Fast assault. Chase down and pepper targets. |
| Interceptor | Missile | Speed + homing. Hard to escape. |
| Dogfighter | Autocannon | Nimble duelist. Out-turn everyone. |
| Dogfighter | Flak | Circle-strafe specialist. Stay on their tail. |
| Sustain | Autocannon | War of attrition. Never run out of energy. |
| Sustain | Missile | Missile spam. Keep the pressure constant. |

---

## Project Structure

```
melee/
├── index.html          # Launcher/lobby interface
├── launcher.js         # Lobby logic and multiplayer connection
├── launcher.css        # Lobby styling
├── game.html           # Game viewport (embedded as iframe)
├── game.js             # Game entry point
├── game.css            # All in-game visual styling
├── server.js           # Node.js multiplayer server (Express + Socket.IO)
├── game/
│   ├── core/           # Game.js - main game loop and state
│   ├── config/         # Ship hulls, weapons, secondaries, archetypes
│   ├── entities/       # Ship, Projectile, EMPMine, PDCBeam
│   ├── effects/        # Visual effects (explosions, shockwaves, trails)
│   ├── modes/          # Deathmatch, LastShipStanding, SuddenDeath
│   ├── ui/             # HUD, KillFeed, LoadoutSelection
│   ├── input/          # InputManager for keyboard controls
│   ├── audio/          # AudioManager with Web Audio API
│   ├── systems/        # Renderer (DOM-based)
│   └── networking/     # NetworkManager for multiplayer sync
├── music/              # Battle music layers (3 intensity tracks + menu)
└── sounds/             # Sound effects (weapons, explosions, UI)
```

---

## Multiplayer Architecture

- **Host-Authoritative** - The first player to connect becomes the host. The host runs the game simulation and broadcasts state to all clients.
- **Host Migration** - If the host disconnects, another player automatically takes over as host.
- **Socket.IO** - Real-time WebSocket communication for low-latency gameplay.
- **State Sync** - Game state is synchronized at 30Hz. Clients interpolate between updates.
- **Pause System** - Any player can pause (2 pauses per player, 30-second limit). All players see who paused.
- **Observer Mode** - When the lobby is full (4 players), additional connections can spectate the match.

---

## Credits & Attribution

### Inspiration

This game is heavily inspired by **Star Control 2: The Ur-Quan Masters** and its SuperMelee mode. The ship-to-ship combat, energy management, and Newtonian physics pay homage to that classic.

### Audio

Sound effects and music are sourced from:

- **Star Control 2 & 3** - Music, various sound effects
- **Quake 2** - Railgun sound effect
- **[Kenney.nl](https://kenney.nl/)** - UI sounds and additional effects

### Technology

Built with vanilla JavaScript, HTML, and CSS. Server powered by:

- [Express](https://expressjs.com/) - Web server
- [Socket.IO](https://socket.io/) - Real-time multiplayer

---

## Development

### Debug Controls (Local Play Only; your mileage may vary)

| Key | Action |
|-----|--------|
| 1-4 | Spawn random ship for player 1-4 |
| G | Toggle gravity well |
| C | Toggle collision |
| H | Toggle debug HUD |
| B | Toggle hitbox display |
| V | Toggle camera debug overlay |

### Performance Monitoring

Use Chrome DevTools Performance tab to monitor frame times. The game targets 60 FPS with a fixed 16.67ms physics timestep.

---

## Requirements Checklist

Per the assignment specification:

- [x] 2-4 player real-time multiplayer
- [x] Players join via URL from separate computers
- [x] Unique player names
- [x] Host can start game when 2-4 players ready
- [x] 60 FPS minimum with RequestAnimationFrame
- [x] DOM-only rendering (no canvas)
- [x] Pause/Resume/Quit menu with player name broadcast
- [x] Scoring system with real-time updates
- [x] Winner displayed at game end
- [x] Game timer visible to all players
- [x] Keyboard controls
- [x] Sound effects and music
- [x] Multiple game modes and ship customization

*Built with ❤️ by Mika and Pavel.*
