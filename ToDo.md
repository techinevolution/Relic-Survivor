# Relic Survivor – To‑Do

## High Priority
- [ ] Rename current survival build to **Arcade Mode** across UI, code comments, and documentation.
- [ ] Draft Adventure Mode structure: stage list, unlock flow, and onboarding beats.
- [ ] Design persistence strategy (likely localStorage) for weapon unlocks, stage completion, and settings.
- [ ] Update global combat rules so weapon rank-ups modify patterns only; shift damage/attack-speed scaling to global relics.
- [ ] Rework projectile systems (boomerang, bow, skybrand) to respect the player’s 180° facing cone.

## Weapons & Relics
- [ ] Sword: implement tiered arc growth (45° → 180° by max rank).
- [ ] Boomerang: add volley count per rank and ignore heart pickups at full health.
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

## Adventure & Progression
- [ ] Place first-run weapon pickups in Adventure stages; mark unlocked status in persistence.
- [ ] Define unlock milestones (e.g., beat Stage 1 to unlock bow).
- [ ] Outline reward pacing for relics and global upgrades.

## Tooling & Docs
- [ ] Keep `Data_formats.md` in sync with new schemas (progress saves, weapon configs, enemy definitions).
- [ ] Expand `AGENTS.md` with Arcade/Adventure mode vocabulary once changes land.
- [ ] Capture balancing notes and open questions in Outline/ToDo during development.

## Nice to Have / Later
- [ ] Explore leaderboard or run-history export once persistence exists.
- [ ] Investigate modular build pipeline if single-file structure becomes limiting.
- [ ] Consider accessibility options (colorblind outlines, screen shake toggle) while revamping art and VFX.
