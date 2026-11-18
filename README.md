# ZONEBREAK — 1.0.4

A lightweight, original browser arena game with 30 fighters, six class menus, Duel, Hot Zone, Knockout, bot practice, friend rooms and real-player matchmaking. All art is drawn in code and all sound is synthesized. This game is separate from CU-Escape.

This update replaces XP with **coins, individual fighter trophies, a trophy road and daily win chests**. Twenty-level stat growth stays in place. There are no real-money purchases.

## Try it

Extract the ZIP and open **PLAY.html** in a desktop browser for offline bot practice. Online play needs the included Node Web Service. No separate image packs or asset uploads are needed.

| Control | Action |
| --- | --- |
| WASD | Move |
| Mouse | Aim |
| Left click / hold | Basic attack |
| Q or right click | Charged super |
| E | Equipped gadget |
| Escape | Pause practice / open online match menu / close reward screens |

This version uses a keyboard and mouse, without touch movement controls.

## Start with Jolt and build a roster

**New profiles own Jolt only.** Other fighters can be previewed in their class menu, but cannot be played, leveled or equipped until collected. Join-room fighter selectors also disable unowned fighters.

| Class | Fighters |
| --- | --- |
| Tanks | Rook, Bulwark, Bramble, Kiln, Anchor |
| Damage dealers | Jolt, Nova, Flint, Echo, Prism |
| Healers | Sprig, Pulse, Brook, Lumen, Mender |
| Artillery | Fuse, Tumble, Cinder, Drizzle, Orbit |
| Assassins | Wisp, Nyx, Talon, Volt, Shade |
| Marksmen | Scope, Kestrel, Vega, Quill, Sable |

Tanks hit hard at very short range. Damage dealers specialize in mid-range pressure. Healers damage enemies or heal wounded allies. Artillery throws over cover. Assassins are quick and fragile. Marksmen have medium health and very long-range shots that still stop at walls. Each fighter has its own stats, attack pattern and super; see **FIGHTERS.md**.

Fighters have three reloading ammo cells. Staying out of combat restores health after four seconds. Damage/healing and a slow passive charge fill the super meter. Bushes conceal enemies unless close or revealed by attacking/taking damage. Walls block walking, dashes and ordinary shots; artillery bombs travel over them.

## Trophies and trophy road

Completed matches grant trophies **only to the fighter used**:

| Result | Fighter trophies |
| --- | --- |
| Win | +8 |
| Draw | +4 |
| Loss | +2 |
| Leave before the match ends | 0 |

Practice, friend-room and public online matches count. Trophies do not increase a fighter’s level. Switching fighters switches to that fighter’s own trophy counter.

The combined lifetime trophy total advances the **trophy road**. It does not copy trophies to other fighters. Rewards are added automatically and can be viewed with the Trophy Road button. Coins appear at 20 trophies and every 40 after that; fighter unlocks appear at 40 trophies and every 40 after that, finishing at 1,160. Every nonstarter fighter is on the road. If a chest already awarded that fighter, its road milestone gives 250 coins instead. Rewards cannot be claimed twice.

See **ECONOMY.md** for the complete road and prices.

## Five daily win chests

The first **five wins per day** each award one chest. Losses/draws do not award chests. Further wins still award trophies. The counter resets at **midnight in Cedarville, Ohio: America/New_York / Eastern Time**, automatically accounting for daylight saving.

Click Daily Drops in the menu or Open Daily Drop on the result screen. Each chest starts Common and gives **exactly six upgrade attempts**. Each successful click advances one rarity; a failed attempt keeps the current rarity. Reward delivery happens once, on click six.

| Current rarity | Chance each click upgrades it | Coin reward if final rarity |
| --- | --- | --- |
| Common | 60% → Rare | 60–100 |
| Rare | 40% → Epic | 120–180 |
| Epic | 25% → Mythic | 240–360 |
| Mythic | 12% → Legendary | 500–750 |
| Legendary | Already maximum | 1,000–1,500 |

Only a **Legendary** chest can award a fighter: it has a **25% chance** to award one randomly chosen unowned fighter instead of coins. If every fighter is owned, it awards coins. Lower rarities always give coins. Upgrade odds are conditional on the chest’s current rarity, not the probability of obtaining that final rarity.

Earned unopened chests carry over to later days. The chest’s seed, clicks, rarity and final reward are saved, so closing/reloading cannot restart its attempts or pay out again.

## Coins buy levels and abilities separately

XP is no longer earned or used. Coins come from chests and trophy-road rewards. Spend them to level **an owned fighter**, one level at a time, up to 20. The level-2 upgrade costs 60 coins; each subsequent upgrade costs 20 more, up to 420 for level 20. All nineteen upgrades together cost 4,560 coins.

Health, damage and healing still start at **65% of their maximum values**, growing evenly each level to 100% at level 20. The former level-1 base values are the current level-20 maxima. Speed, range and cooldowns do not grow with level. The menu shows current/max stats and a 20-level track. Level 20 grants the mastery badge automatically.

An ability’s level requirement only makes it **eligible for purchase**. It is not free when leveling up:

| Choice | Gadget level / price | Passive level / price |
| --- | --- | --- |
| I | Level 5 / 150 coins | Level 8 / 250 coins |
| II | Level 10 / 300 coins | Level 12 / 450 coins |
| III | Level 15 / 600 coins | Level 16 / 750 coins |
| IV | Level 18 / 1,000 coins | Level 20 / 1,200 coins |

Purchasing equips that ability. Switching between already-owned choices is free. Only one gadget and one passive are equipped at once. All gadgets have cooldowns. Supers are available from level 1 and cost no coins. Descriptions list level-20 damage/healing values; the actual output scales with level.

## Online matchmaking and friends

Everyone must open the same hosted website.

- **Public Online:** separate queues by mode **and exact selected-fighter trophy count**. Duel needs two real players at that trophy count; Hot Zone and Knockout each need six. Level is not a matchmaking restriction. The queue never widens the trophy range or quietly adds bots. This can mean waiting longer when few players are online.
- **Friends:** create a room, share the code, and join using the code alone. Private rooms do not require equal trophies, so friends can play together. The host can start with empty seats filled by bots. Rooms support replays and mode changes after matches.
- **Practice:** local bots only. Bots are given the selected fighter’s trophy count and level; their characters are random. Choose Rookie, Contender or Veteran.

| Mode | Rules |
| --- | --- |
| Duel | 1v1, first to two round wins, up to 80 seconds per round, no mid-round respawn |
| Hot Zone | 3v3, capture to 100%, contested zone stops scoring, 3.5-second respawn, three-minute cap |
| Knockout | 3v3, first to two elimination-round wins, up to 90 seconds per round |

Duel/Knockout have a closing danger ring in the last 25 seconds. Timeout compares remaining health fractions; ties draw the round. A ten-minute overall cap prevents endless tied rounds. There are three original cover/bush layouts.

The server owns combat, uses a 30 Hz simulation, and sends 15 Hz snapshots. Clients predict local movement and interpolate remote movement. Disconnecting fighters become bots without resetting the match, and the room host transfers to another member. Online games continue while the match menu is open.

## Saves and upgrading from 1.0.3

**Profiles remain browser-local, not server accounts.** Coins, fighter ownership, purchases, levels, trophies, road claims and chest progress save in this browser. Clearing its storage can erase them. Saves do not automatically transfer between devices or between file-based practice and a hosted website.

Old XP profiles are read once: fighters with previously earned XP remain owned and retain their corresponding level and previously earned ability choices. Jolt is always owned. Unplayed fighters that were previously just selectable now need collecting. Old XP is not earned further and is not converted into spendable coins. Career wins/match counts remain. Old results do not retroactively create trophies or daily chests.

Combat validates level limits, purchased ability declarations and unlock levels. However, **there is no authoritative account database**: the server trusts the local profile’s supplied ownership, purchases and trophies. These casual profiles and exact-trophy queues are not cheat-proof or a secure ranked economy. The daily clock uses the device’s time interpreted in Eastern Time. A server-account economy would need server-owned profiles and transactions.

## Update your existing Render game

Replace the contents of your existing ZONEBREAK repository with the files inside this ZIP’s `ZONEBREAK` folder, then commit. **Include the new `economy.js`**, as well as the updated `roster.js`, `core.js`, `render.js`, `app.js`, `index.html`, `style.css`, `PLAY.html` and package files. Keep `vendor` in the repository. No `public` folder or separate art upload is used.

Use the same Render **Web Service**, with these unchanged settings:

| Setting | Value |
| --- | --- |
| Build | `npm ci --omit=dev` |
| Start | `npm start` |
| Health check | `/health` |
| Node | `24` |
| Root directory | Blank if package.json is at repository root |

Once deployed, reload and check for **1.0.4** in the menu. HTTPS automatically uses WSS for game connections. This package has not been deployed to your Render account. Keep CU-Escape in its separate repository/service.

One server instance is supported. Rooms/queues are in memory, so deploying or restarting ends active matches. Additional instances would need shared matchmaking/room infrastructure.

## Run and verify locally

Install Node 24, then run in this folder:

```sh
npm ci --omit=dev
npm start
```

Open `http://localhost:3000`. The server reads `PORT` when hosted. The MIT-licensed WebSocket dependency is bundled in `vendor/ws`, including its license, so installation needs no registry downloads.

After changing sources, regenerate the offline page and run checks:

```sh
node build.cjs
npm test
```

The 63 automated tests cover combat, all fighters and abilities, wall sliding, 20-level scaling, purchased ability gates, coin transactions, Jolt-only starts, trophy-road rewards, six-click saved chests, daily limits and Eastern Time/DST resets, exact-trophy queues at different levels, real HTTP/WebSocket games, room replay/disconnects, save migration and application UI flows. UI tests use a simulated DOM; they do not replace live browser or internet-latency playtesting.
