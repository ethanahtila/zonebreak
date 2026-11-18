# ZONEBREAK — 1.0.0

A separate, original browser arena game. ZONEBREAK is a working title. It does not modify CU-Escape. All graphics are drawn in code, sound is synthesized, and the whole project is small enough to upload together. There are no sprite packs, external fonts, asset servers, or build downloads.

## Try it immediately

Extract this ZIP, then open **PLAY.html** in a desktop browser. This single file includes the complete game for offline bot practice. Use the normal website or local Node server for online play. A standalone file cannot provide its own multiplayer server.

## Controls

| Control | Action |
| --- | --- |
| WASD | Move |
| Mouse | Aim |
| Left click / hold | Basic attack |
| Q or right click | Charged super ability |
| E | Gadget |
| Escape | Pause practice / open online match menu |

This initial version targets computers with a keyboard and mouse. It has no touch movement controls.

## Modes

- **Duel:** 1 vs 1. First to two round wins, no mid-round respawn. Each round lasts up to 80 seconds.
- **Hot Zone:** 3 vs 3. Hold the central zone to reach 100%. When both teams occupy it, scoring stops. Defeated fighters respawn after 3.5 seconds. A match lasts up to three minutes.
- **Knockout:** 3 vs 3. Eliminate the opposing team, first to two round wins. No mid-round respawns; rounds last up to 90 seconds.

Duel and Knockout have a closing danger ring during the final 25 seconds. A timeout compares total remaining health as a fraction of each fighter’s maximum health. Ties draw the round; a ten-minute overall cap prevents endless tied matches. Each mode has its own cover and bush layout.

## Five fighters

| Fighter | Role | Basic attack | Super |
| --- | --- | --- | --- |
| Rook | Tank | Very short-range, heavy frontal strike | Faultline: charge, area damage and temporary protection |
| Jolt | Damage | High-damage, mid-range three-bolt burst | Rail Surge: piercing charged shot |
| Sprig | Healer | Bolts heal wounded teammates or damage enemies | Sanctuary: place a healing area |
| Fuse | Artillery | Lob bombs over walls; damage occurs when they land | Fireworks: clustered bombardment |
| Wisp | Assassin | Fast, fragile fighter with short-range dagger bursts | Slipstrike: aimed dash and slash |

Every fighter starts with three ammo cells, one equipped gadget, and one passive. Ammo reloads automatically. Staying out of combat restores health after four seconds. Damage and healing charge supers, alongside a slow passive charge.

**Gadgets:** Rook chooses damage reduction or emergency healing; Jolt chooses instant ammo or a stronger next burst; Sprig chooses self-healing or ally healing; Fuse chooses a retreating blast or instant bomb detonation; Wisp chooses brief concealment or bonus burst damage. Each activates once per cooldown. Holding E does not repeatedly activate it when the cooldown expires. Gadgets recharge with time, not payments or limited match charges.

**Passives:** two options per fighter enhance their role through slowing, low-health defense, range damage, faster reloading, healing return, faster regeneration, wider blasts, lingering damage, finishing damage, or healing on eliminations. Read the exact values in the loadout menu.

Bushes conceal enemies until you get close or they reveal themselves by attacking or taking damage. Wisp’s concealment also ends at close range and is broken by attacking. Cover blocks movement, ordinary shots and dashes; lobbed bombs travel over it.

## Fighter levels and saves

Each fighter has independent XP and levels 1–10. Each level adds 4% to base health, damage, and healing. The alternate gadget unlocks at level 3; the alternate passive at level 5. All five fighters and their first loadouts are available immediately.

Finished matches award XP for participating, winning and contributing damage, healing or zone time. Practice earns 75% of online XP. Leaving an unfinished match does not award XP.

**Progress saves to this browser’s local storage.** It is not an account system, cannot move between devices automatically, and can be lost if browser data is cleared. File-based practice and the hosted website may have separate saves. Online loadouts are validated for their allowed ranges, but browser-owned levels are not cheat-proof. This is a casual first version, not a ranked economy.

## Online play

All players must open the same hosted website.

- **Online:** separate matchmaking queues for each mode. Duel waits for **2 real players**; Hot Zone and Knockout wait for **6 real players**. These queues do not silently add bots.
- **Friends:** create a room and share its code. Friends enter only the code and press **Join Existing Room**; the host’s mode applies automatically. The host can start with fewer humans and empty seats become bots. Teams are balanced automatically. A room can replay or change mode after a match; Duel requires no more than two room members.
- **Practice:** local bots only; no other players join. Choose Rookie, Contender or Veteran.

The server owns combat and match state. Movement uses local prediction, server reconciliation and remote interpolation. If a player leaves, their fighter becomes a bot without resetting the game. The host role moves to another room member. Online games continue while a player opens the match menu.

## Deploy as a NEW Render game

Keep CU-Escape in its current repository and service. Create a **separate GitHub repository** for this game.

1. Extract the ZIP. Open the `ZONEBREAK` folder.
2. Upload **everything inside that folder** to the root of the new repository. Include the `vendor` folder: it contains the bundled WebSocket library and its license. `package.json`, `server.cjs` and `index.html` should be visible at the repository’s top level. There is no `public` folder and no separate sprite upload.
3. Commit the upload. In Render, create a new **Web Service** connected to that repository. Do not choose Static Site: multiplayer needs the Node server.
4. Use these settings:

   | Setting | Value |
   | --- | --- |
   | Runtime | Node |
   | Root directory | Leave blank if files are at the repository root |
   | Build command | `npm ci --omit=dev` |
   | Start command | `npm start` |
   | Health check path | `/health` |
   | Node version | `24` |

5. Deploy, then open Render’s assigned HTTPS address and share it. WebSocket connections automatically use **WSS** on that address. No API keys, database, additional socket URL, or paid asset service is required by the game.
6. To update, commit changed files to the branch connected to Render and deploy that commit. The included `render.yaml` also describes the service if using Render’s repository configuration workflow.

Keep the server at **one instance**. Rooms and queues live in memory; restarting or deploying ends active matches and waiting rooms. Multiple independent server instances would need a shared room system, which this starter does not include. Hosting capacity and network conditions still affect multiplayer performance.

## Run locally

Install Node 24, open a terminal in this folder, then run:

```sh
npm ci --omit=dev
npm start
```

Open `http://localhost:3000`. The server reads the `PORT` environment variable when hosted and otherwise uses port 3000. The required MIT-licensed `ws` library is bundled in `vendor/ws`, so installation does not need to download any packages. `vendor/ws/LICENSE` contains its license.

## Development and verification

Edit `index.html`, `style.css`, `app.js`, `core.js`, or `render.js`. After changes, regenerate the optional offline practice page:

```sh
node build.cjs
npm test
```

The 23 automated tests cover combat, five role differences, cover/lob interactions, healing, gadgets and cooldowns, leveling and unlocks, visibility, mode objectives, bot navigation, finished-match rewards, real WebSocket matchmaking, room joining/replay/settings, host migration, disconnect continuity, authoritative input, served assets and health checks, and application menu/input/save flows using a DOM fixture.

Tests include real HTTP/WebSocket connections; the UI tests use a simulated browser DOM. They do not replace a live browser playtest with friends or a real-world latency test. This package has not been deployed to your Render account.
