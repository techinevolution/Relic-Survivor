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
  - Future UI polish: add a compact auto bar plus a relic/global icon strip under the weapon dock so pickups read at a glance.
  - Spinner manual aim polish: blades should launch from their current orbit slot, travel past the cursor (boomerang range), then drift back into the standard formation (pairs/triangle/square/pentagon) using tempo speed; UI should show ammo/active shots and scroll/number hotkeys must access Spinner.

## Recent Systems (Nov 2024)
- **Audio & Options**: Inline music manager now cycles four Arcade tracks, runs the menu loop with crossfades, and exposes a Music toggle under Options (title or pause menu). Respect `settings.musicMuted` anywhere new audio is added.
- **Codex Expansion**: Codex panel now has Monsters, Weapons, and Relics tabs. Weapon blurbs mention modifying relics (Lightstone included on all); relic tab should include future augments/globals with icons and unlock notes.
- **Spinner / Whirring Wake**: Trails emit on a timer, use smaller hitboxes, and deal `spinner damage × (0.25 → 0.45)` at 4 ticks/sec so Wake is supportive instead of AFK dominant. Keep new tuning in mind when adding cadence buffs.

## Progression & Persistence
- Add a save record (localStorage or exportable JSON) storing:
  - Unlocked weapons/relics.
  - Adventure stage completion flags.
  - Cosmetic toggles (future-proofing).
- Provide manual reset/export options to keep the single-file distribution viable.

## Persistence & Save UX
- Use browser `localStorage` for primary save data (`relic-survivor-save` JSON).
- Track schema version so we can migrate or reset gracefully.
- Provide Options menu actions:
  - `Save Now` / auto-save on significant events (level-up, stage clear).
  - `Export Save` (downloads JSON) and `Import Save` (paste/upload).
  - `Reset Progress` with confirmation dialog.
- Store: unlocked weapons/relics, adventure stage flags, options, stats seeds.
- Future: optional manual save slots / cloud sync hooks if platform allows.

## Weapons & Relics Direction
- **Global Rules**
  - Weapon rank-ups change behavior/coverage only (no per-weapon damage or attack-speed scaling).
  - Global relics handle universal damage, attack speed, and utility boosts.
  - Projectile weapons auto-target nearby threats regardless of player facing; only the sword keys off movement direction.
  - Audio polish backlog: XP pickup SFX should play even when vortex/boomerang scoops orbs, and overall mix needs another ~10% reduction so spam feels soft.
- **Sword (Brambleblade)**
  - Rank 1: 45° strike.
  - Each rank widens the arc until 180° at max rank.
  - Visual: conjure a blade in front of the survivor that sweeps across the active arc with a bright trail so the hit zone reads clearly.
  - Desired QoL: sword swipes should vacuum nearby drops (XP gems, hearts, vortex orbs) on contact, similar to how boomerangs scoop pickups.
- **Boomerang (Skyhook Loop)**
  - Auto mode: eventually launch the full volley simultaneously at unique targets, then idle for a longer cooldown (lets cooldown relics matter again).
  - Manual mode: keep rapid one-at-a-time throws that follow the click aim; boomerangs already seek XP when no enemies remain and skip hearts when full.
  - Each rank adds another boomerang to the volley.
  - UX polish: XP orbs gathered by a returning boomerang should ride the weapon, surface above it, and trigger the pickup sound when the return arrives (even if a vortex initiated the gather).
- **Bow (Voyager Bow)**
  - Ranks add arrows.
  - Projectiles render as forward-pointing triangles.
  - Upcoming tweak: scale up arrow sprites approximately 30% so volleys read clearly as the roster grows.
- **Skybrand (Lightning)**
  - Ranks increase chain count.
  - Rank 5 expansion: chance for each chain to fork to an additional enemy.
  - Future augment relic: `Stormshard Chorus` (name WIP) that adds a zizzling aftershock (`lightning_zizzle.mp3`) as the secondary effect; plan to gate it behind Skybrand Rank 5 similar to Skyhook Resonance.
- **Bombbloom**
  - Halve base explosion radius and sprite size.
  - Rank-ups increase bomb count per drop.
  - Rank 5 expansion restores large blast radius.
  - Manual mode (future): bombs should be thrown toward the click location, traveling before arming and detonating.
- **Spinner / Wake**
  - Cap core blades at 5 orbiting projectiles.
  - Wake trail starts short and lengthens with ranks.
  - Manual mode concept: press/hold to expand the ring, release to retract.
  - Visual backlog: Whirring Wake’s trail should read brighter/longer without increasing damage so players notice it’s active.
- **Tempo Charm**
  - Provides global attack-speed scaling per weapon: sword swing frequency, boomerang volleys, bow salvos, skybrand cooldown, bomb volleys, spinner rotation speed.
- **Magnet Rune**
  - Ranks 1-4: widen pickup radius steadily.
  - Vacuum drops should spawn from Rank 1 with a very low chance (~0.01%) and scale up to ~0.03% by Rank 5 so players feel the benefit early.
- **Skyhook Resonance (boomerang augment)**
  - Unlock bonus that boosts boomerang pickup radius per rank; plan to gate this relic behind Boomerang Rank 5.

- **Interface Modes**
- **Action Bar** (manual/hybrid) — live in Arcade/Adventure builds: dock-style icon strip with six slots, sweep-to-ready cooldown wipes, and a gold outline on the Manual weapon. Manual selection now happens via pause menu clicks or the scroll wheel while playing; left-clicking the arena still fires the active Manual weapon.
  - **Compact Auto Bar** (survivor-style): shrunk icons summarise owned weapons when full auto is preferred. Cap simultaneous weapons (e.g., 4 main + 2 utility) once new gear is added.

## Enemies & Encounters
- **Slimes**: Delay mini-split spawn to avoid instant multi-hits.
  - Azure variant task: ensure any hit dealing ≥24 damage vaporizes the slime even if earlier boomerang pokes occurred; current overkill logic still lets bombs trigger splits.
- **Bats**: Leave as current baseline.
- **Goblins**: Initial elites use standard goblin stats for fairness.
- **Skull**: Fast “dash across screen” unit with red outline and flame trail.
- **Spider**: Quick approach, short pause, fires dodgeable web that roots the player briefly.
- **Ghost**: Becomes translucent and pauses when faced; dashes away if approached. Vulnerable only when visible, encouraging area damage.

## Art Direction
- Evolve visuals toward minimalist “modern Atari” shapes while embracing a brighter, grassy palette inspired by the reference image (punchy greens, dark outlines).
- Use the provided player sprite proportions as reference for new enemy designs.
- Highlight special enemies (skull flames, spider webs) with simple but readable VFX.

## Technical Considerations
- Investigate modularizing the single HTML file only when persistence or tooling demands it.
- Introduce `Data_formats.md` as the schema hub shared between HTML and potential Python tooling.
- Document renaming of the current system to **Arcade Mode** in code comments and UI during future implementation.
- Long-term input goal: allow manual weapon control via click-to-attack and per-weapon auto/manual toggles once Adventure work settles.
- Pause menu Dev Mode exposes invulnerability toggle and per-relic/weapon rank controls for rapid balancing experiments.

## Open Questions
- How are Adventure Mode stages structured (linear, branching, challenge tiers)?
- Preferred method for persistence (localStorage vs. JSON export/import)?
- Timeline for art refresh versus core systems work; do enemies ship with placeholder silhouettes first?
