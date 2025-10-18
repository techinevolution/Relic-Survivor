# Relic Survivor – Outline

## Core Vision
- Retain a pick-up-and-play survival loop with short, high-intensity runs.
- Rename the existing endless run to **Arcade Mode** and make it the score-chasing destination.
- Add a curated **Adventure Mode** that unlocks weapons, relics, and stages. Adventure completions permanently open content for Arcade.
- Keep delivery lightweight (single HTML) in the short term, but plan for lightweight persistence to remember unlocks across sessions.

## Modes & Structure
- **Adventure Mode**
  - Stage-based progression with handcrafted encounters.
  - Weapons appear in-world as pickups; first-time pickup unlocks them globally.
  - Introduce simple map events (tutorial beats, minibosses) to showcase new gear.
  - Stage-select map with illustrated tiles (e.g., “Grasslands”) inspired by SMB3; unlocks flow left-to-right as stages clear.
  - Tutorial stage: quiet field, no spawns until the boomerang pickup; pickup triggers pop-up (“You got the Boomerang!”) and a character quip balloon.
  - Subsequent stages gate progress behind survival/kill objectives; first boss drops the bow unlock.
- **Arcade Mode**
  - Pure survival, all previously unlocked gear available.
  - Leaderboard-ready once persistence exists.
  - Unlock condition: collect every weapon in Adventure (temporarily open for development/testing builds).

## Progression & Persistence
- Add a save record (localStorage or exportable JSON) storing:
  - Unlocked weapons/relics.
  - Adventure stage completion flags.
  - Cosmetic toggles (future-proofing).
- Provide manual reset/export options to keep the single-file distribution viable.

## Weapons & Relics Direction
- **Global Rules**
  - Weapon rank-ups change behavior/coverage only (no per-weapon damage or attack-speed scaling).
  - Global relics handle universal damage, attack speed, and utility boosts.
  - Projectiles (boomerang, bow, skybrand) originate from the player’s facing, within a 180° frontal cone.
- **Sword (Brambleblade)**
  - Rank 1: 45° strike.
  - Each rank widens the arc until 180° at max rank.
- **Boomerang (Skyhook Loop)**
  - Each rank adds another boomerang in the volley.
  - Each boomerang will run an independent timer so the screen can stay busy; add logic to seek XP drops only when no enemies are nearby.
  - Boomerang ignores heart pickups unless the player is missing health.
- **Bow (Voyager Bow)**
  - Ranks add arrows.
  - Projectiles render as forward-pointing triangles.
- **Skybrand (Lightning)**
  - Ranks increase chain count.
  - Rank 5 expansion: chance for each chain to fork to an additional enemy.
- **Bombbloom**
  - Halve base explosion radius and sprite size.
  - Rank-ups increase bomb count per drop.
  - Rank 5 expansion restores large blast radius.
- **Spinner / Wake**
  - Cap core blades at 5 orbiting projectiles.
  - Wake trail starts short and lengthens with ranks.
- **Tempo Charm**
  - Provides global attack-speed scaling per weapon: sword swing frequency, boomerang volleys, bow salvos, skybrand cooldown, bomb volleys, spinner rotation speed.
- **Magnet Rune**
  - Ranks 1-4: widen pickup radius steadily.
  - Rank 5: spawn a limited-use vacuum drop that pulls all XP on the field when collected.
- **Boomerang Augment (future relic)**
  - Unlock bonus that boosts boomerang pickup radius per rank, so returned blades sweep wider XP arcs.

- **Interface Modes**
  - **Action Bar** (manual/hybrid): weapon icons run along the bottom center with radial cooldowns, auto toggles, and a gold highlight for the selected weapon. Left-click fires the highlighted weapon toward cursor/facing while respecting cooldown floors.
  - **Compact Auto Bar** (survivor-style): shrunk icons summarise owned weapons when full auto is preferred. Cap simultaneous weapons (e.g., 4 main + 2 utility) once new gear is added.

## Enemies & Encounters
- **Slimes**: Delay mini-split spawn to avoid instant multi-hits.
- **Bats**: Leave as current baseline.
- **Goblins**: Initial elites use standard goblin stats for fairness.
- **Skull**: Fast “dash across screen” unit with red outline and flame trail.
- **Spider**: Quick approach, short pause, fires dodgeable web that roots the player briefly.
- **Ghost**: Becomes translucent and pauses when faced; dashes away if approached. Vulnerable only when visible, encouraging area damage.

## Art Direction
- Evolve enemy visuals toward a minimalist “modern Atari” look.
- Use the provided player sprite proportions as reference for new enemy designs.
- Highlight special enemies (skull flames, spider webs) with simple but readable VFX.

## Technical Considerations
- Investigate modularizing the single HTML file only when persistence or tooling demands it.
- Introduce `Data_formats.md` as the schema hub shared between HTML and potential Python tooling.
- Document renaming of the current system to **Arcade Mode** in code comments and UI during future implementation.
- Long-term input goal: allow manual weapon control via click-to-attack and per-weapon auto/manual toggles once Adventure work settles.

## Open Questions
- How are Adventure Mode stages structured (linear, branching, challenge tiers)?
- Preferred method for persistence (localStorage vs. JSON export/import)?
- Timeline for art refresh versus core systems work; do enemies ship with placeholder silhouettes first?
