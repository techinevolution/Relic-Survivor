# Relic Survivor – Agent Notes

## Player & Stakeholder Context
- Primary collaborator (Katherine) is a gamer-first designer with limited coding background; keep explanations high-level, avoid jargon, and share actionable steps when asking for feedback.
- When choices are needed, present 2–3 clear options and note expected gameplay impact rather than implementation detail.
- Pace work “slow and steady.” Flag risky refactors early and wait for approval before large rewrites.

## Project Structure
- Active build lives at `index.html` in the repo root (renamed from the previous `relic-survivor-vortex-r13-readable.html`). Gameplay logic, markup, and styling remain bundled there for double-click launches.
- `Outline.md` captures long-term direction (Adventure mode, Arcade rename, enemy plans). `ToDo.md` tracks actionable tasks—update both when scoping new work.
- `Data_formats.md` documents schemas shared between in-game data and external tooling; keep it accurate when introducing persistence, new enemies, or balance tables.
- `AGENTS.md` remains the collaboration playbook.
- Audio assets now live in `Assets/Audio/` (`Music/` and `SFX/` subfolders). Keep paths relative so the game still runs when opened directly from disk.
- No build tooling—keep the project runnable by double-clicking the HTML file in a browser.
- Persistence plan: Use browser `localStorage` (single key JSON). Document schema in `Data_formats.md`; bump version when fields change.
- Modal UI (level-up picker) is rendered with inline DOM elements inside the HTML. Everything else draws to the main `<canvas id="game">`.
- Options/Music: the Options overlay (from title or pause menu) toggles global music mute via `RS.State.settings.musicMuted`; audio crossfades respect the setting immediately.

## Code Architecture
- The script bootstraps under `'use strict'` and builds a single namespace object: `RS` with branches `Config`, `Util`, `State`, `Audio`, `Registry`, `Systems`, `Render`, `UI`, and `Tests`. Do not introduce globals outside this namespace.
- Stick with browser-native **JavaScript** (TypeScript optional with a build step); CSS is for presentation only. Python is reserved for offline tooling that reads/writes the schemas in `Data_formats.md`.
- Section order inside the script is deliberate and matches the comment banners:
  1. `RS.Config` constants (dimensions, palette, balance).
  2. `RS.Util` helpers (math, RNG, formatting).
  3. `RS.State` (authoritative mutable state).
  4. `RS.Audio` (music manager, playlists, crossfades).
  5. DOM grabs and key-blocking setup.
  6. Registries (`RS.Registry.ICON`, relics array, `addEnemyKind` calls).
  7. `RS.Systems` (gameplay tick handlers).
  8. Standalone helpers (e.g., `nearestEnemyTo`).
  9. `RS.UI` (canvas HUD buttons + DOM level picker).
  10. Event wiring (canvas clicks, keyboard listeners).
  11. `RS.Render` (world, HUD, menus, pause, death, attract).
  12. Game loop (`loop` / `draw`) and dev helpers (`showChoices`, `setChoices`).
  13. `RS.Tests.run` self-checks.
- Preserve this flow when adding features so future agents can scan the file quickly.

## Game State & Systems
- `RS.State` holds core run-time data: mode (`attract`, `menu`, `playing`, etc.), timers, player stats, arrays for enemies/projectiles/resources (including `vacuumDrops` spawned by high-rank Magnet Rune), and upgrade tracking (`levels`, `currentChoices`).
- Persistent UI prefs live on `RS.State.settings` (currently `musicMuted`). Pause-only overlays use `RS.State.pauseOptionsOpen`.
- `RS.Systems` houses per-frame logic. Update order in the main loop is fixed: input → spawner → enemies → weapon systems (`spinner`, `bow`, `storm`, `bomb`) → cleanup → pickups → regen. If adding systems (e.g., a new weapon), follow this pattern and hook in at the correct position.
- Balance tuning flows through `RS.Config.BALANCE`; keep new constants there rather than scattering numeric literals.
- Player inventory and stats are reset via `RS.Systems.restart`. Extend that function whenever new persistent state is introduced.

## Registries & Content Authoring
- `RS.Registry.ICON` maps upgrade IDs to emoji for UI badges.
- Relics are defined in the `Relics` array (object literals with `id`, `name`, `desc`, `max`, optional `canOffer`, and `onPick`). After definition they’re inserted into `RS.Registry.Relics`. Respect this pattern when adding upgrades so level-up UI and gating continue to work.
- Enemies are registered via `addEnemyKind`, which expects `id`, `make`, `update`, and `draw`. Spawning relies on `RS.Systems.spawner`, so new enemy types need spawn triggers wired there.

## Rendering & UI
- Core gameplay draws entirely on the main canvas. `RS.Render.world` handles terrain, player, weapons, VFX, and enemy rendering; keep new draw routines modular and reuse colors from `RS.Config.COLORS`.
- `RS.Render.hud`, `pause`, `death`, and `attract` implement overlays directly on the canvas using layout constants. Use existing helper methods (`drawButton`, `drawCenterText`, `drawHearts`) for consistency.
- Level-up choices live in the HTML overlay (`#levelModal`) and are managed through `RS.UI.showLevelModal`, `setChoices`, and `renderChoices`. DOM updates should go through these helpers to avoid duplicate listeners.
- Menu modes (`attract`, `menu`, `how`, `options`, `credits`) are canvas-driven; toggles occur by assigning `RS.State.mode`.

## Input Handling
- Movement keys funnel through `RS.State.keys` with lowercase lookups. Keyboard listeners prevent-default on arrow keys and space, and special keys drive meta actions: `P` pause, `R` restart, `M` jump to menu.
- Mouse clicks drive canvas UI buttons (pause/menu overlays), manual weapon aiming (for whichever weapon is set to Manual via the pause menu or scroll wheel), and level-up choices via DOM buttons. Touch support does not exist yet—plan to mirror pointer logic when requested.
- Keep input capture centralized in the existing listeners; avoid adding per-feature listeners scattered across the file.
- Dev panel toggle is hidden behind ⌘ + ⌥ + Z (while paused). The pause menu “Options” button exposes player-facing toggles instead of surfacing the dev panel directly.

## Economy & Progression
- XP gems (`s.orbs`) award progress toward `player.xpTo`; level-ups trigger `RS.UI.rollChoices` which pauses the game and surfaces 1–3 relic options.
- Damage, rate-of-fire, cooldowns, and leeching factors flow through `RS.Systems.effDamage`, `timeScale`, and upgrade callbacks. Reuse these helpers when creating new effects (e.g., apply damage via `RS.Systems.applyDamage` so leech tracking stays correct).
- Magnet Rune spawns low-chance `vacuumDrop` orbs (0.01% → 0.03% from rank 1→5) that pull in all loose XP when collected.
- Enemy spawns ramp using elapsed time (`s.elapsed`). When adding difficulty curves, extend `RS.Systems.spawner` and its timers rather than re-implementing elsewhere.

## Testing & Debugging
- Lightweight assertions exist in `RS.Tests.run`; expand this function for sanity checks (unique IDs, gating rules, math helpers).
- `showChoices`, `hideChoices`, `toggleChoices`, and `setChoices` are dev utilities bound on `window` for manual testing. Use them during manual QA to reproduce level-up states.
- Pause menu **Dev Mode** toggle (button beside Resume) enables invulnerability and provides +/- controls to adjust weapon & relic ranks mid-run; changes reapply the entire loadout instantly.
- No automated test runner or CI—manual playtesting (load title, run a wave, verify relic choices, confirm death screen) remains the validation path.

## Mobile & Touch Goals
- Target itch.io embed and standalone browsers; the canvas must scale responsively and expose a fullscreen toggle (desktop) plus full-bleed mobile view.
- Mobile default: auto mode in portrait with simplified movement; manual/dual-stick play is landscape-only for readability and control fidelity.
- Implement dual virtual sticks for movement/aim in landscape; bombs need a dedicated tap gesture when aimed manually.
- Treat the weapon action bar as tap targets only on touch devices to avoid accidental swaps on desktop.
- Persist touch/orientation preferences under `RS.State.settings.mobile` and document schema updates in `Data_formats.md`; boot mobile devices into portrait/auto and gate manual behind landscape.

## Versioning Workflow
- Increment versions by copying `index.html` to a versioned filename (e.g., `relic-survivor-vortex-r14-readable.html`) before major changes. Keep the previous version alongside it for rollback—there is no `archive/` folder yet.
- Note feature goals and outstanding bugs in `AGENTS.md` until separate docs are introduced; include dates so the history stays clear.
- When submitting work, summarize gameplay-facing changes for Katherine first, then add implementation notes for future agents.

## Collaboration Notes
- Communicate discoverables (bugs, balance quirks, UX polish ideas) in plain language with suggested next steps.
- When additional information is needed from Katherine, phrase questions using gameplay terminology (e.g., “Should enemies sprint sooner?” instead of “Adjust spawn scalar?”).
- Document any tuning changes (numbers, timers) so balance decisions can be tracked without digging into code.

## Update Log
- 2024-10-31 – Azure slimes vaporize when struck for ≥2× their max HP (e.g., 24+ damage), skip splitting, and drop two XP orbs offset left/right to signal the overkill.
- 2024-10-31 – Bombbloom cooldown now restores full ammo clip, trailing bombs wait a flat 0.35s between plants (independent of attack speed), manual throws arc to the click point with a bounce before arming, the planted bombs use a custom sprite with fuse VFX, and explosions apply full damage on contact.
- 2024-11-10 – Added the JS audio manager with four-track Arcade playlist, menu music crossfades, and Options toggle (title/pause) that flips `settings.musicMuted`; dev tools now open via ⌘ + ⌥ + Z while paused.
- 2024-11-10 – Codex expanded with Relics tab (weapon descriptions now show augmenting relics) and Whirring Wake trails heavily nerfed (lower damage, tiny wake, timed emission) so Spinner isn’t an AFK win button.
