# Game Design Doc — (Working Title TBD)

> A 3D anime-style **battlegrounds fighting game** that runs in the browser.
> Original characters, original powers, original map. Inspired by the *genre*, not a copy of any game.

**Status:** Planning — no code yet
**Last updated:** 2026-11-15

---

## Table of Contents

1. [Overview](#1-overview)
2. [Platform & Tech](#2-platform--tech)
3. [Controls](#3-controls)
4. [Core Combat Mechanics](#4-core-combat-mechanics)
5. [Move Types (Block Rules)](#5-move-types-block-rules)
6. [Awakening System](#6-awakening-system)
7. [Fighters](#7-fighters)
   - [Juno Marrow — "The Blot"](#-juno-marrow--the-blot)
   - [Pip Hollow — "The Stitch"](#-pip-hollow--the-stitch)
   - [Mask — "The Understudy"](#-mask--the-understudy)
8. [Roster Balance & Matchups](#8-roster-balance--matchups)
9. [Map: Windstep Village](#9-map-windstep-village)
10. [Game Modes](#10-game-modes)
11. [Game Feel & Polish](#11-game-feel--polish)
12. [Build Plan](#12-build-plan)
13. [Starting Numbers (Tunable)](#13-starting-numbers-tunable)
14. [Open Questions](#14-open-questions)
15. [Playtest Notes](#15-playtest-notes)

---

## 1. Overview

**Genre:** 3D battlegrounds fighter (free-for-all arena brawler)

**Pitch:** Pick one of three fighters with strange powers — living ink, living thread, or stolen performances — and brawl across a huge cliffside village. Land combos, break blocks, smash opponents through paper walls, and when your meter is full, **awaken** to unlock a whole new set of moves and a cinematic finisher.

**Pillars:**
- **Combat feels heavy and flashy** — every hit has impact (hit-stop, knockback, screen shake).
- **Every fighter plays completely differently** — each has one clear game plan.
- **Moves have clear counters** — players can always tell how to deal with a move.
- **Big open map** — lots of space, height, and things to break.

---

## 2. Platform & Tech

- **Platform:** Web browser (desktop first; mobile/touch later).
- **Engine:** Three.js (3D in the browser) — to be confirmed when building.
- **Multiplayer:** Not in the first version. Start with **player vs. training dummy / bots**. Online multiplayer comes later once combat feels good.
- **Art:** First version uses simple shapes (blocky placeholder models). Real visuals come after the fighting feels right.

---

## 3. Controls

Same for every fighter.

| Action | Key | Notes |
|---|---|---|
| Move | `W A S D` | |
| Camera | Mouse | Shift-lock style over-the-shoulder camera |
| Jump | `Space` | |
| **M1** (basic attack) | Left click | 4-hit combo |
| **Block** | `F` (hold) | |
| **Dash** | `Q` | Direction follows movement keys |
| **Evasive** | `Q` while being hit | Escapes a combo; long cooldown |
| **Moves 1–4** | `1` `2` `3` `4` | Special moves |
| **R Special** | `R` | Each fighter's unique mechanic |
| **Awaken** | `G` | Only when awakening meter is full |
| Emote / Taunt | `T` | Cosmetic only |

---

## 4. Core Combat Mechanics

- **M1 Combo** — 4 quick hits. The 4th hit knocks back.
  - Hold **Space** on the 4th hit → **Uppercut** (launches opponent up).
  - Press M1 in the air on the 4th hit → **Downslam** (slams opponent into the ground).
- **Block** — reduces or stops damage from blockable attacks. Uses a **block meter**; blocking too much **breaks guard** and stuns you.
- **Perfect Block** — block right before a hit lands to **parry**. The attacker is staggered. Perfect-blocking a projectile reflects it.
- **Dash** — quick dodge in any direction. Short cooldown.
- **Evasive** — dash while being combo'd to break out. Long cooldown, so you must choose when to use it.
- **Ragdoll** — heavy hits knock fighters down. Downed fighters are briefly vulnerable before getting up.
- **Wall Slam** — knocking a fighter into a wall deals bonus damage and bounces them.
- **Follow-ups** — some moves turn into a new move for a few seconds if they hit (e.g. Juno's Splatter Shot → Tendril Snare).
- **Two-press moves** — first press sets something up (a summon, a decoy), second press uses it.
- **Hold variants** — some moves do something different when held instead of tapped.
- **R Special** — each fighter has a unique mechanic on `R`.

---

## 5. Move Types (Block Rules)

Every move is tagged so players know how to respond.

| Tag | Name | How to deal with it |
|---|---|---|
| 🟢 | **Blockable** | Block reduces/stops it |
| 🔴 | **Block Break** | Shatters block, stuns the blocker. Dodge it instead. |
| 🟣 | **Grab** | Ignores block. Dash away to avoid. |
| 🔵 | **Projectile** | Blockable. Perfect block reflects it. |
| ⚫ | **Unblockable** | Only a dash dodges it. Rare — mostly finishers. |

---

## 6. Awakening System

- Every fighter has an **awakening meter** that fills from **dealing and taking damage**.
- When full, press `G` to **awaken**:
  - Short cinematic: camera zoom, voice line, visual burst.
  - The fighter's look changes.
  - **Moves 1–4 are replaced** by 4 awakened moves.
  - Move 4 is always the fighter's **finisher**.
- Awakening lasts **~60 seconds** or **until the finisher is used**, whichever comes first.
- Each awakening has its own **music sting** (optional — see Open Questions).

---

## 7. Fighters

### 🖋️ Juno Marrow — "The Blot"

**Power:** Living ink
**Game plan:** **Cover the map in ink and control space.** The more ink on the ground, the more options Juno has.
**Range:** Mid–long **Difficulty:** Hard

**Backstory:** Juno is a quiet art student from a wealthy family that funds a secret research lab. She always drew in sketchbooks to escape her strict parents. On her 16th birthday, the ink started moving off the page. Now one drawing keeps appearing in her sketchbook that she never remembers making: a girl trapped behind glass. Her ink seems to remember things *she* doesn't.
**Personality:** Shy, sarcastic once comfortable, scared of what her power is trying to tell her.
**Signature look detail:** Ink stains on her hands and face that move when she's upset.

#### Passive: Ink Puddles
Many of Juno's moves leave **ink puddles** on the ground. Puddles stay on the map for a while, so fights get messier over time.

#### R Special: **Ink Well**
Juno has an **ink meter** that fills when her moves hit.
- **Tap R** — flick a small ink splash from her brush (quick poke, leaves a puddle).
- **Hold R** — spend ink to recharge move cooldowns faster.
- **Full ink meter** — moves get bonus effects (bigger puddles, faster summons).

#### Normal Kit

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Splatter Shot** | 🔵 Projectile | Fast ink throw. Leaves a puddle where it lands. **On hit → becomes Tendril Snare for 3s.** |
| 1↳ | **Tendril Snare** | 🟣 Grab | Follow-up. Ink wraps the opponent, lifts them, and slams them down. |
| 2 | **Sink** | 🟢 Blockable | Dives into the ground, pops up under the opponent with an uppercut. **Near a puddle:** can pop out of *any* puddle on the map. |
| 3 | **Ink Octopus** | Two-press | **1st press:** a giant floating ink pen draws a huge octopus beside her. **2nd press (tap):** Tentacle Whip 🟢. **2nd press (hold):** Ink Cloud — blinds the opponent. Octopus lasts ~8s or until used; it can be hit and destroyed. |
| 4 | **Paper Cut** | 🔴 Block Break | Tears a page from her sketchbook and slashes. Quick answer to blockers. |

#### Awakening: **"Wet Ink"**
*Look:* Ink stains spread across her whole body. Ink drips off her and leaves a trail wherever she walks.

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Ink Flood** | 🔴 Block Break | A wave of ink pushes everyone back and covers the floor in puddles. |
| 2 | **Kraken Draft** | Two-press | The giant pen draws a **massive** ink kraken. 2nd press: it slams down with all its tentacles. |
| 3 | **Brushstroke** | 🟢 Blockable | Huge brush slash that launches the opponent. |
| 4 | **🎨 Blackout Page** | ⚫ Unblockable — **Finisher** | The world turns into a black-and-white sketch. The opponent moves in slow motion while Juno strikes from every puddle, ending with one giant brushstroke. |

---

### 🧵 Pip Hollow — "The Stitch"

**Power:** Living thread and needles
**Game plan:** **Tag, pull, punish.** Stick needles in the opponent to stack **Stitches**, reel them in, then cash the stitches in for damage and healing.
**Range:** Close **Difficulty:** Medium

**Backstory:** Pip is a 16-year-old runaway who sewed together her own plush "family" so she'd feel less alone. When her power woke up, they started to move.
**Personality:** Scrappy, playful, fiercely loyal to her dolls.

#### Passive: **Stitches**
- Some attacks add a **Stitch** to the opponent (max **3**), shown as little X marks on their body.
- Some moves **pull out** stitches for bonus damage per stitch.
- Each time Pip pulls stitches out, **she heals a little** — she's patching herself with the thread.

#### R Special: **Anchor Thread**
- **Tap R** — throw an anchor needle into the ground or a wall.
- **Tap R again** — zip along the thread to the anchor.
- If an opponent is **between Pip and the anchor**, the thread clotheslines them and adds a Stitch.
- Works as movement, escape, and trap.

#### Normal Kit

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Needle Toss** | 🔵 Projectile | Throws 3 needles in a spread. Each hit adds a Stitch. **If any needle hits → becomes Reel In for 3s.** |
| 1↳ | **Reel In** | 🟣 Grab | Follow-up. Yanks the opponent straight to Pip, into M1 range. |
| 2 | **Hemline** | 🟢 Blockable | Spinning thread whip around her. **Pulls out all Stitches** — more stitches = more damage + bigger heal. Her main payoff move. |
| 3 | **Doll Decoy** | Two-press | **1st press:** drops a plush doll where she stands. **2nd press:** swaps places with the doll. If the opponent hits the doll, it bursts and briefly stuns them. |
| 4 | **Pin Down** | 🔴 Block Break | Stabs a giant sewing needle down in front of her. Breaks block and **pins the opponent's feet** briefly. |

#### Awakening: **"Unraveled"**
*Look:* Her hair and clothes come apart into floating threads. **Every hit adds a Stitch**, including M1s.

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Puppet Strings** | 🟣 Grab | Threads latch onto the opponent; she drags them through the air and slams them back and forth. |
| 2 | **Seam Rip** | 🟢 Blockable | Dashes straight through the opponent, leaving a line of stitches that tears open a second later. |
| 3 | **Big Teddy** | Two-press | 1st press: a giant stitched bear rips out of the ground. 2nd press: it belly-flops onto the opponent (🔴 Block Break). |
| 4 | **🧸 Patchwork Army** | ⚫ Unblockable — **Finisher** | Dozens of dolls swarm the opponent, pile on, and burst. Bonus damage per Stitch on the opponent. |

---

### 🎭 Mask — "The Understudy"

**Power:** Performance — copies, counters, and stage tricks
**Game plan:** **Read, react, steal.** A counter-fighter who wants the opponent to attack so he can punish or steal their move.
**Range:** Close–mid **Difficulty:** Hard

**Backstory:** A theater actor who lost his face — literally. Under his masks there's nothing but blank skin. He wears masks to feel like *someone*.
**Personality:** Dramatic, theatrical, speaks like he's always on stage. Hides a lot of sadness.

#### R Special: **Mask Swap**
Tap R to cycle masks. Each changes how **all** his moves feel. Short cooldown on swapping.

| Mask | Effect |
|---|---|
| 😐 **Blank** (default) | Copied moves are **stronger** |
| 😠 **Rage** | More damage, faster M1s — but takes more damage |
| 😢 **Sorrow** | Takes less damage, block meter refills faster — but deals less damage |

#### Normal Kit

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Understudy** | Counter stance | A short dramatic pose. **Hit by an M1:** counters with a quick strike. **Hit by a special move:** copies it — this slot becomes that move for **one use** (same block type as the original). |
| 2 | **Spotlight** | 🔵 Projectile | Beam of stage light that marks the opponent **"On Stage"** for 6s. Marked opponents take extra damage, and his next move on them comes out faster. |
| 3 | **Curtain Call** | 🟣 Grab | A red stage curtain wraps the opponent; he spins and throws them. **On a marked opponent:** throws much farther (great for wall slams). |
| 4 | **Prop Drop** | 🔴 Block Break | A heavy stage sandbag drops from above onto the opponent. Slower but breaks block. |

#### Awakening: **"Opening Night"**
*Look:* A spotlight follows him everywhere. A faint audience murmurs. A painted smile appears on his blank face.

| # | Move | Type | Description |
|---|---|---|---|
| 1 | **Dramatic Entrance** | 🟢 Blockable | Teleports behind the opponent in curtain smoke. On a marked opponent, auto follow-up kick. |
| 2 | **Intermission** | Buff | Wears **all three masks at once** for 6s — all bonuses, no downsides. |
| 3 | **Standing Ovation** | 🔴 Block Break | Giant invisible hands clap the opponent between them. |
| 4 | **🎭 Encore** | ⚫ Unblockable — **Finisher** | **Steals the opponent's finisher** and uses it on them. If they aren't awakened: **Curtain Drop** — a giant stage curtain falls and crushes them. |

---

## 8. Roster Balance & Matchups

| | Game plan | Range | Strength | Weakness | Difficulty |
|---|---|---|---|---|---|
| 🖋️ **Juno** | Ink control | Mid–long | Zoning, summons, puddle mobility | Weak when caught up close with no ink down | Hard |
| 🧵 **Pip** | Stack, pull, cash out | Close | Pressure, healing, mobility | Short range; needs Needle Toss to start | Medium |
| 🎭 **Mask** | Bait, counter, steal | Close–mid | Punishing aggressive players | Struggles vs. patient players | Hard |

**Rock–paper–scissors triangle:**
- **Pip beats Juno** — zips in and drags Juno out of her puddles.
- **Juno beats Mask** — fights from range with summons, giving him nothing to counter.
- **Mask beats Pip** — Pip must attack, which is exactly what Mask wants.

---

## 9. Map: Windstep Village

*(Name is a working title.)*

A mountain village built in **three tiers** up a cliffside. Mist, cherry blossoms, and a waterfall. Not a story map — designed for **space, variety, and height**.

### Tier 1 — Lower Village (main fighting area)
- **Training Courtyard (center):** Big open stone square with wooden dummies and weapon racks. Room for big summons and crowds.
- **Market Street:** Wooden stalls, lanterns, carts — all **splinter** when hit.
- **Village Houses:** Small homes with paper walls you can **smash through** (leaves a person-shaped hole).
- **The Well:** Small landmark to fight around.

### Tier 2 — Middle Terrace
- **Bamboo Forest:** Tight paths, ambushes, breaks line of sight. Bamboo snaps when hit.
- **Waterfall Pool:** Shallow water that slightly slows movement.
- **Rope Bridge:** Swaying bridge over a gap — knock people off to Tier 1.
- **Hot Spring:** Steam blocks vision.

### Tier 3 — Upper Shrine
- **The Dojo:** Large wooden training hall; good indoor arena. Walls crack under wall slams.
- **The Great Gate:** Giant red gate at the top of the stairs — main landmark visible from everywhere.
- **The Bell Tower:** Climbable; highest point on the map.
- **Cliff Overlook:** Ledge with a view of the clouds.

### Movement Between Tiers
- **Central stone stairs** connect all three tiers.
- **Side ramps and rooftops** let players jump up house roofs to the next tier.
- **Drop-downs** from any tier to the one below (good for escaping).
- **Pip's Anchor Thread** can zip between tiers; **Juno's Sink** can travel between puddles on different tiers.

### Map Rules
- **Boundaries:** Outer edge is a cliff with a low fence + invisible wall. No falling out of the world.
- **Destruction resets:** Broken stalls, walls, and bamboo rebuild after ~30 seconds.
- **Spawns:** Random points around the tier edges, far from other players.
- **Practice corner:** Side yard by the Dojo with training dummies.

### Atmosphere
- Cherry blossom petals in the wind
- Mist rolling over the cliff edge
- Paper lanterns that swing when hit
- Later: sunset and night (glowing lanterns) versions

---

## 10. Game Modes

| Mode | Description | When |
|---|---|---|
| **Training** | Fight a dummy that can be set to idle / block / attack / dodge | First version |
| **Vs. Bots** | Free-for-all against AI fighters | Early |
| **Battlegrounds** | Online free-for-all, respawn after KO | Later (needs multiplayer) |
| **1v1 Duels** | Ranked or casual duels | Later |
| **Boss Raid** | Team up against a giant monster | Ideas pile |

---

## 11. Game Feel & Polish

- **Hit-stop** (tiny freeze on impact), **screen shake**, and **knockback** on every solid hit.
- **Awakening cinematics:** half-second camera zoom, voice line, visual burst.
- **Character interaction lines** when fighters meet (e.g. Juno to Mask: *"…Do you even have a face under there?"*).
- **Kill effects:** unique KO animation per fighter.
- **Emotes / taunts** on `T`.
- **Later:** skins (e.g. red-ink Juno, patchwork-outfit Pip), day/night map variants.

---

## 12. Build Plan

Build in small steps. **Play after every step, note what feels wrong, fix it.**

1. **Foundation**
   - 3D scene, camera, simple blocky character that can walk, jump, and dash.
   - Graybox version of Windstep Village (blocks for houses, stairs, tiers).
2. **Core combat**
   - M1 combo, uppercut, downslam, block, perfect block, evasive, ragdoll, wall slam.
   - Health bars, hit-stop, knockback, screen shake.
   - Training dummy with settings.
3. **First fighter: Juno**
   - Full normal kit + Ink Well (R) + puddle system.
4. **Awakening**
   - Meter, activation cinematic, Juno's "Wet Ink" kit + Blackout Page finisher.
5. **Pip and Mask**
   - Full kits, R specials, awakenings.
6. **Bots**
   - Simple AI opponents to fight.
7. **Polish**
   - Real models/effects, map details, sound, music, menus.
8. **Online multiplayer** *(later)*

---

## 13. Starting Numbers (Tunable)

These are **starting guesses** — expect them to change a lot during playtesting.

| Setting | Value |
|---|---|
| Health | 100 |
| M1 damage | 3 per hit (4th hit: 4) |
| M1 combo reset time | 1.2s |
| Dash cooldown | 2s |
| Evasive cooldown | 20s |
| Block damage reduction | 80% |
| Block meter | Breaks after ~6 blocked M1s |
| Guard-break stun | 1.5s |
| Perfect block window | 0.15s |
| Follow-up window | 3s |
| Special move damage | 8–14 |
| Special move cooldowns | 6–15s |
| Awakening duration | 60s |
| Finisher damage | 30–40 |
| Destruction reset | 30s |
| Respawn time | 5s |

---

## 14. Open Questions

- [ ] **Game title?**
- [ ] **Map name** — keep "Windstep Village"?
- [ ] **Juno's mystery drawing** — the "girl behind glass" was originally tied to a removed character. Keep it as an unsolved mystery, or tie it to someone new?
- [ ] **World lore** — do we keep a shared world/setting for the backstories, or keep backstories standalone?
- [ ] **Music** — unique music for each awakening?
- [ ] **Fighter looks** — outfits, colors, effect colors for each fighter.
- [ ] **Mobile controls** — on-screen buttons layout.
- [ ] **Main menu & character select** design.

---

## 15. Playtest Notes

*Write down anything that feels off while playing. We'll fix it in the next build.*

| Date | Build | What felt wrong | Fix |
|---|---|---|---|
| | | | |
