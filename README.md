# ZONEBREAK — 1.0.1

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

## Five class menus, twenty-five fighters

Click a class to show only that class’s five fighter cards. The roster no longer fills the screen with every fighter.

| Class | Fighters |
| --- | --- |
| Tanks | Rook, Bulwark, Bramble, Kiln, Anchor |
| Damage dealers | Jolt, Nova, Flint, Echo, Prism |
| Healers | Sprig, Pulse, Brook, Lumen, Mender |
| Artillery | Fuse, Tumble, Cinder, Drizzle, Orbit |
| Assassins | Wisp, Nyx, Talon, Volt, Shade |

Each fighter has independent progression, different base stats, its own attack pattern and a unique super. Tanks have almost no basic attack range. Damage dealers specialize in mid-range fire. All five healers can heal allies or damage enemies with their basic attacks. Every artillery fighter lobs over walls. Assassins have high movement speed and low health. See **FIGHTERS.md** for all attacks, supers and stats.

New playstyles include Anchor’s hook, Echo’s returning wave, Bramble’s slowing thorns, Brook’s piercing healing bolts, Lumen’s protective halo, Cinder’s persistent fire, Nyx’s empowered cloak, Volt’s storm dash and Shade’s life-stealing super.

Every fighter starts with three ammo cells. Ammo reloads automatically. Staying out of combat restores health after four seconds. Damage and healing charge supers, alongside a slow passive charge. **Supers remain available at level 1; gadgets and passives do not.**

Each fighter now has **three gadget choices and three passive choices**, with class-based effects. Equip one gadget and one passive once their unlock levels are reached. Gadgets activate once per cooldown; holding E cannot repeatedly trigger one. The third options add tank mobility, damage-dealer evasive dashes, healer protection, artillery emergency ammo and assassin escape dashes. The third passives add healthy-tank movement, bonus super charge, stronger emergency healing, artillery mobility and out-of-combat assassin movement.

Bushes conceal enemies until you get close or they reveal themselves by attacking or taking damage. Wisp’s concealment also ends at close range and is broken by attacking. Cover blocks movement, ordinary shots and dashes; lobbed bombs travel over it.

## Fighter levels and saves

Each fighter has independent XP and levels 1–10. Each level adds 4% to base health, damage, and healing. All 25 fighters are selectable immediately. Unlocks are enforced in local practice and by the multiplayer server.

| Level | Ability unlock | Total fighter XP |
| --- | --- | --- |
| 1 | Basic attack and super; no gadget or passive | 0 |
| 2 | — | 350 |
| 3 | — | 800 |
| 4 | Gadget I | 1,350 |
| 5 | — | 2,000 |
| 6 | Passive I | 2,750 |
| 7 | Gadget II | 3,600 |
| 8 | Passive II | 4,550 |
| 9 | Gadget III | 5,600 |
| 10 | Passive III | 6,750 |

This is slower than 1.0.0: level 2 used to require 100 XP and now requires 350. **Previously earned XP is preserved** in the same browser save. Displayed levels are recalculated using the slower curve, so an existing fighter may show a lower level. Unavailable old loadout choices fall back to the first unlocked choice, or remain inactive until the first unlock. New fighters receive separate fresh XP records.

Finished matches award XP for participating, winning and contributing damage, healing or zone time. Practice earns 75% of online XP. Leaving an unfinished match does not award XP.

**Progress saves to this browser’s local storage.** It is not an account system, cannot move between devices automatically, and can be lost if browser data is cleared. File-based practice and the hosted website may have separate saves. Online loadouts are validated for their allowed ranges, but browser-owned levels are not cheat-proof. This is a casual first version, not a ranked economy.

## Online play

All players must open the same hosted website.

- **Online:** separate matchmaking queues for each mode. Duel waits for **2 real players**; Hot Zone and Knockout wait for **6 real players**. These queues do not silently add bots.
- **Friends:** create a room and share its code. Friends enter only the code and press **Join Existing Room**; the host’s mode applies automatically. The host can start with fewer humans and empty seats become bots. Teams are balanced automatically. A room can replay or change mode after a match; Duel requires no more than two room members.
- **Practice:** local bots only; no other players join. Choose Rookie, Contender or Veteran.

The server owns combat and match state. Movement uses local prediction, server reconciliation and remote interpolation. If a player leaves, their fighter becomes a bot without resetting the game. The host role moves to another room member. Online games continue while a player opens the match menu.

## Update your existing ZONEBREAK website

Replace the files in the existing **ZONEBREAK** repository with the files inside this ZIP’s `ZONEBREAK` folder, then commit the changes. **Include the new `roster.js` file** along with the updated `core.js`, `render.js`, `app.js`, `index.html`, `style.css`, package files and `PLAY.html`. Keeping an old core or omitting the new roster file will break the page. No separate graphics upload is needed.

Use your existing Render Web Service and its existing commands; they have not changed. After deployment, refresh the page and check that the menu shows **1.0.1**. Do not clear browser storage if you want to retain earned XP. An update restarts the game server, so finish active matches first.

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

Edit `index.html`, `style.css`, `app.js`, `roster.js`, `core.js`, or `render.js`. After changes, regenerate the optional offline practice page:

```sh
node build.cjs
npm test
```

The 36 automated tests cover the 25-fighter roster, five class filters, all basic attacks and healing attacks, higher-level unlocks, all 75 gadget selections, distinct super mechanics, wall-face sliding across all maps and fighter sizes, the original corner-lock regression, dash collisions, prediction, combat and objectives, bot navigation, rewards, real WebSocket matchmaking and room replay, multiplayer wall movement, save migration and UI flows. The old version stops moving in the corner-lock regression; this version slides past it.

An additional 30 complete simulated bot matches exercised all three modes with locked level-1 loadouts and unlocked level-10 loadouts. The actual Canvas renderer was used to inspect every fighter portrait. Neither check is a claim of a live browser playtest or internet latency test.

Tests include real HTTP/WebSocket connections; the UI tests use a simulated browser DOM. They do not replace a live browser playtest with friends or a real-world latency test. This package has not been deployed to your Render account.
