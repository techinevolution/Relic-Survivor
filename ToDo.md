# Relic Survivor – To‑Do

## High Priority
- [x] Rename current survival build to **Arcade Mode** across UI, code comments, and documentation.  ✅ done this session (UI messaging + docs).
- [x] Add a mode-select flow that exposes **Adventure** vs. **Arcade** from the title screen.  ✅ selector live with per-mode messaging.
- [x] Cleanup pause menu weapon panels so there is a single selection list (with icon + rank info) that also controls manual weapon mode.  ✅ consolidated to one list w/ icons + level, manual toggle.
- [x] Remove the Adventure/Arcade label in the top-left HUD so max hearts are never obscured.  ✅ top-left text gone.
- [x] Recenter the XP bar and relocate it beneath the weapon toolbar so layout stays readable as runs progress.  ✅ centered bar now under weapon dock.
- [ ] Draft Adventure Mode structure: stage list, unlock flow, and onboarding beats.
- [ ] Decide on persistence stack (localStorage primary, JSON export/import secondary) and design reset/export UX.
- [x] Update global combat rules so weapon rank-ups modify patterns only; shift damage/attack-speed scaling to global relics.  ✅ sword/bow/bomb now pattern-only.
- [x] Recenter projectile feel now that facing lock is gone; make sure boomerang, bow, and skybrand targeting reads clearly without directional input. ✅ handled earlier.
- [x] Verify that weapon rank-ups do not boost damage (Lightstone of Wisdom should be the only damage scalar) and update the pause panel display accordingly. ✅ messaging/panel in place.

## Weapons & Relics
- [x] Sword: implement tiered arc growth (45° → 180° by max rank).
- [x] Sword: replace the translucent wedge with a visible blade sweep that travels across the current rank’s arc.
- [x] Implement dock-style action bar with cooldown wipes and pause/scroll-based manual weapon selection.  ✅ icons auto-fill slots; manual weapon is unique.
- [x] Manual weapon mode support confirmed live in current build.
- [ ] Add click feedback + range cues for manual weapons (reticle, “no target” hint) to help players learn the mode.
- [ ] Implement compact auto bar for full-auto runs; enforce active-weapon cap once weapon roster expands.
- [ ] Surface relic/global icons beneath the weapon bar so pickups are visible during runs.

- [x] Boomerang: add volley count per rank and ignore heart pickups at full health (bug regression check).  ✅ per-slot launchers keep volleys live.
  - [x] Tweak cadence: track per-boomerang timers so a full volley stays active; consider XP-seek behavior when no enemies remain.  ✅ boomerangs fan to XP when no targets.
- [x] Bow: convert projectiles to triangles and add extra arrows per rank.
- [x] Magnet Rune: scale pickup radius per rank; add Skywell vacuum drop chance that ramps with rank.  ✅ radius tiers + rank-based 0.01%→0.03% drop rate.
- [x] Lightstone of Wisdom: ensure damage multiplier applies to all weapons and surfaces in pause stats.  ✅ pause panel shows current multiplier.
- [x] Design boomerang augment relic that increases boomerang pickup radius per rank.  ✅ Skyhook Resonance relic boosts scoop radius.
- [x] Revisit Skyhook Loop auto-fire: launch full volley simultaneously at unique targets, lengthen base cooldown, and retune cooldown rune impact.  ✅ volleys fire together after ammo recharge.
- [x] Gate Skyhook Resonance unlock behind Boomerang rank 5; reassess collect radius per rank once gating lands.  ✅ `canOffer` now requires Boomerang Lv5.

- [x] Skybrand: scale chain count with ranks; Rank 5 adds fork chance per jump.  ✅ chains scale; fork sparks at rank 5.
- [x] Bombbloom: halve base explosion radius/visual, expand bomb counts per rank, Rank 5 restores wide blast.  (Base radius toned down & scales, trail-only rank ups.)
- [x] Spinner/Wake: cap blades at five; scale wake length with rank.  ✅ single ring tops at five blades; wake trail length grows with rank.
- [x] Tempo Charm: ensure each weapon’s cadence responds to the relic’s attack-speed bonus.  ✅ all cadence timers now respect atkSpeed multiplier.
- [x] Bombbloom manual mode: convert to thrown projectile that travels toward click point before arming/exploding. ✅ manual throws arc, bounce, then arm.
- [x] Spinner manual mode: manual shots now fire individual blades toward the cursor and return along the path (ammo mirrors orbiting blades).
- [ ] Spinner manual mode polish: launch blades from their current orbit slot, travel past the cursor to boomerang max range, glide back into the default formation using tempo speed, and show active shots so ammo/readiness stays readable. Ensure scroll+number hotkeys can pick the spinner instantly.
- [x] Magnet Rune vacuum drop: make Skywell orbs spawn from rank 1 with low chance (0.01%) and scale frequency to 0.03% by rank 5; balance against heart spawn rate.  ✅ chance scales per rank (0.01% → 0.03%).
- [x] Rebuild Boomerang firing to be ammo-based (shots consume ammo and refill on return; auto-fire only when ammo available).  ✅ ammo refills on return now.
- [x] Fix Bombbloom ammo recharge so the full stock refills after cooldown and respect rank-based capacity.  ✅ full refill after cooldown.
- [x] Reduce Forest Spinner base damage to 5 (Lightstone of Wisdom handles scaling). ✅ already tuned.
- [x] Give Bombbloom a bomb-shaped sprite and VFX so it reads clearly in play.  ✅ new sprite + detonation flash.
- [ ] Add a relic that unlocks Skybrand branching at rank 5 instead of the rank itself.
- [x] Adjust Sanguine Thread to boost only the sword and gate its rank-ups behind Sword Rank 5.  ✅ Now a Brambleblade-only augment unlocked at sword rank 5.
- [ ] Wire up the new weapon SFX set (files landed under Audio/SFX/) so each weapon fire/use cue plays an appropriate sound.
- [ ] EXP pickup polish: drop the `exp_pickup` volume another 10% (total 15% below music) and ensure boomerang-carried XP rides visibly on the boomerang and plays the pickup sound when the boomerang returns (or when vortex auto-collect finishes).
- [ ] Bow readability: scale arrow sprites up by ~30% so volleys read clearly mid-fight.
- [ ] Whirring Wake chip polish: rework the trail visuals (brighter pulses/longer streaks) without changing damage.
- [ ] Sword swipe QoL: sword arcs should vacuum nearby drops (XP, hearts, vortex orbs) when they connect, mirroring boomerang returns.

## Enemies & Encounters
- [x] Slimes: add delay before split children become targetable/damageable.  ✅ parent shakes then spawns staggered minis.
- [ ] Goblins: align initial elite stats with standard goblins.
- [ ] Design & implement new enemy behaviors:
  - [ ] Skull dash unit with flame trail.
  - [ ] Spider with charge-and-web root attack.
  - [ ] Ghost with visibility-based vulnerability and retreat dash.
- [ ] Plan art refresh toward “modern Atari” style using provided player sprite as reference.
  - [ ] Derive palette (bright greens, dark outlines) to match inspiration while keeping minimalist shapes.
  - [ ] Refresh ground layer (procedural grass noise + darker patches) with new palette.
- [ ] Decide how placeholders vs. final art roll out (e.g., silhouettes first, full Atari treatment later).
  - [ ] Create lightweight tree/bush/rock sprites using new palette and Atari-style simplification.
- [x] Halve mini-slime contact damage so they deal 0.5 heart on hit.  ✅ minis now stagger in with half-heart damage.
- [ ] Azure slimes: respect the “24+ damage instantly vaporizes” rule even if prior hits came from boomerangs; currently bombs/other weapons can trigger splits after the overkill threshold.

## Adventure & Progression
- [ ] Place first-run weapon pickups in Adventure stages; mark unlocked status in persistence.
- [ ] Define unlock milestones (e.g., beat Stage 1 to unlock bow).
- [ ] Outline reward pacing for relics and global upgrades.
- [ ] Build stage-select UI (card-based path like SMB3) for Adventure mode navigation.
- [ ] Implement weapon discovery pop-ups with character quips when new gear is found.
- [ ] Script boss/mission objectives that gate weapon unlocks (e.g., boomerang find, bow dropped by stage boss).
- [ ] Answer open questions: stage structure (linear vs branching) and Adventure difficulty ramp.

## Tooling & Docs
- [ ] Keep `Data_formats.md` in sync with new schemas (progress saves, weapon configs, enemy definitions, art metadata).
- [ ] Persist player Options (music mute, future toggles) in the save schema and load them on boot.
- [ ] Implement save system using `localStorage` (auto-save hooks + Options menu controls).
- [ ] Add export/import/reset UI for saves; ensure JSON schema versioning is documented.

- [ ] Expand `AGENTS.md` with Arcade/Adventure mode vocabulary once changes land.
- [ ] Capture balancing notes and open questions in Outline/ToDo during development.
- [ ] Prototype optional Python tooling for batch-editing stage or weapon data using `Data_formats.md` schemas.
- [x] Update How To Play copy so manual weapon mode, click-to-attack, and new systems are represented. ✅ Pause overlay + How To Play panel now describe Manual Mode, click aiming, and options toggle.
- [x] Expand the Codex with a Relics category and ensure all relics are documented. ✅ Codex now includes a Relics tab with proper icons/descriptions; weapon entries cite their augments.

## Nice to Have / Later
- [ ] Explore leaderboard or run-history export once persistence exists.
- [ ] Investigate modular build pipeline if single-file structure becomes limiting.
- [ ] Consider accessibility options (colorblind outlines, screen shake toggle) while revamping art and VFX.
- [ ] Evaluate WebGL-backed renderer (Pixi.js/Three.js) if Canvas performance becomes a bottleneck after art/VFX updates.
- [x] Prototype optional manual weapon controls so players can click-to-attack or toggle individual weapons between auto/manual fire.
- [ ] Add a death-screen polish pass (death animation + pause/stop the music while the death overlay is up).
