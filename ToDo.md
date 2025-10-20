# Relic Survivor – To‑Do

## High Priority
- [x] Rename current survival build to **Arcade Mode** across UI, code comments, and documentation.  ✅ done this session (UI messaging + docs).
- [x] Add a mode-select flow that exposes **Adventure** vs. **Arcade** from the title screen.  ✅ selector live with per-mode messaging.
- [ ] Draft Adventure Mode structure: stage list, unlock flow, and onboarding beats.
- [ ] Decide on persistence stack (localStorage primary, JSON export/import secondary) and design reset/export UX.
- [x] Update global combat rules so weapon rank-ups modify patterns only; shift damage/attack-speed scaling to global relics.  ✅ sword/bow/bomb now pattern-only.
- [ ] Recenter projectile feel now that facing lock is gone; make sure boomerang, bow, and skybrand targeting reads clearly without directional input.

## Weapons & Relics
- [x] Sword: implement tiered arc growth (45° → 180° by max rank).
- [x] Sword: replace the translucent wedge with a visible blade sweep that travels across the current rank’s arc.
- [x] Implement dock-style action bar with cooldown wipes and pause/scroll-based manual weapon selection.  ✅ icons auto-fill slots; manual weapon is unique.
- [x] Manual weapon mode support confirmed live in current build.
- [ ] Add click feedback + range cues for manual weapons (reticle, “no target” hint) to help players learn the mode.
- [ ] Implement compact auto bar for full-auto runs; enforce active-weapon cap once weapon roster expands.

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
- [ ] Bombbloom manual mode: convert to thrown projectile that travels toward click point before arming/exploding.
- [ ] Spinner manual mode: prototype press-and-hold expansion with retract-on-release behavior.
- [x] Magnet Rune vacuum drop: make Skywell orbs spawn from rank 1 with low chance (0.01%) and scale frequency to 0.03% by rank 5; balance against heart spawn rate.  ✅ chance scales per rank (0.01% → 0.03%).

## Enemies & Encounters
- [ ] Slimes: add delay before split children become targetable/damageable.
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
- [ ] Implement save system using `localStorage` (auto-save hooks + Options menu controls).
- [ ] Add export/import/reset UI for saves; ensure JSON schema versioning is documented.

- [ ] Expand `AGENTS.md` with Arcade/Adventure mode vocabulary once changes land.
- [ ] Capture balancing notes and open questions in Outline/ToDo during development.
- [ ] Prototype optional Python tooling for batch-editing stage or weapon data using `Data_formats.md` schemas.

## Nice to Have / Later
- [ ] Explore leaderboard or run-history export once persistence exists.
- [ ] Investigate modular build pipeline if single-file structure becomes limiting.
- [ ] Consider accessibility options (colorblind outlines, screen shake toggle) while revamping art and VFX.
- [ ] Evaluate WebGL-backed renderer (Pixi.js/Three.js) if Canvas performance becomes a bottleneck after art/VFX updates.
- [x] Prototype optional manual weapon controls so players can click-to-attack or toggle individual weapons between auto/manual fire.
