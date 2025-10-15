# Relic Survivor – To‑Do

## High Priority
- [x] Rename current survival build to **Arcade Mode** across UI, code comments, and documentation.  ✅ done this session (UI messaging + docs).
- [x] Add a mode-select flow that exposes **Adventure** vs. **Arcade** from the title screen.  ✅ selector live with per-mode messaging.
- [ ] Draft Adventure Mode structure: stage list, unlock flow, and onboarding beats.
- [ ] Decide on persistence stack (localStorage primary, JSON export/import secondary) and design reset/export UX.
- [ ] Update global combat rules so weapon rank-ups modify patterns only; shift damage/attack-speed scaling to global relics.
- [ ] Rework projectile systems (boomerang, bow, skybrand) to respect the player’s 180° facing cone and current facing direction.

## Weapons & Relics
- [ ] Sword: implement tiered arc growth (45° → 180° by max rank).
- [ ] Boomerang: add volley count per rank and ignore heart pickups at full health (bug regression check).
- [ ] Bow: convert projectiles to triangles and add extra arrows per rank.
- [ ] Skybrand: scale chain count with ranks; Rank 5 adds fork chance per jump.
- [ ] Bombbloom: halve base explosion radius/visual, expand bomb counts per rank, Rank 5 restores wide blast.
- [ ] Spinner/Wake: cap blades at five; scale wake length with rank.
- [ ] Tempo Charm: ensure each weapon’s cadence responds to the relic’s attack-speed bonus.

## Enemies & Encounters
- [ ] Slimes: add delay before split children become targetable/damageable.
- [ ] Goblins: align initial elite stats with standard goblins.
- [ ] Design & implement new enemy behaviors:
  - [ ] Skull dash unit with flame trail.
  - [ ] Spider with charge-and-web root attack.
  - [ ] Ghost with visibility-based vulnerability and retreat dash.
- [ ] Plan art refresh toward “modern Atari” style using provided player sprite as reference.
- [ ] Decide how placeholders vs. final art roll out (e.g., silhouettes first, full Atari treatment later).

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
- [ ] Expand `AGENTS.md` with Arcade/Adventure mode vocabulary once changes land.
- [ ] Capture balancing notes and open questions in Outline/ToDo during development.
- [ ] Prototype optional Python tooling for batch-editing stage or weapon data using `Data_formats.md` schemas.

## Nice to Have / Later
- [ ] Explore leaderboard or run-history export once persistence exists.
- [ ] Investigate modular build pipeline if single-file structure becomes limiting.
- [ ] Consider accessibility options (colorblind outlines, screen shake toggle) while revamping art and VFX.
- [ ] Evaluate WebGL-backed renderer (Pixi.js/Three.js) if Canvas performance becomes a bottleneck after art/VFX updates.
