# Relic Survivor – Data Formats

This reference keeps HTML game data and any external tooling (Python notebooks, balancing scripts, etc.) aligned. Use these shapes when adding persistence, Adventure stages, or batch-editing content.

## Implementation Guidance
- Core gameplay stays in browser-native **JavaScript** (optionally TypeScript compiled to JS). Keep logic inside the `RS` namespace; prefer modules only if we adopt a build step later.
- **CSS** is for presentation only (HUD, overlays). Avoid moving gameplay logic into CSS animations.
- Use **Python** strictly for offline tooling (data munging, balancing sims) that read/write these schemas. Export results as JSON consumable by the HTML build.
- Store persistent data with browser APIs (`localStorage`, future IndexedDB) to preserve the double-click runnable distribution.

## Player Progress
```jsonc
{
  "version": "r14",
  "unlocks": {
    "weapons": ["sword", "boomerang", "bow"],
    "relics": ["tempo", "magnet"]
  },
  "adventure": {
    "stagesCleared": ["forest-01", "ruins-02"]
  },
  "options": {
    "mute": false,
    "screenShake": true
  }
}
```
- Store in localStorage (primary) with optional export/import.
- `version` allows format migrations.

## Weapon Definition
```jsonc
{
  "id": "sword",
  "name": "Brambleblade",
  "mode": "arcade",
  "base": {
    "type": "melee",
    "cooldown": 1.15,
    "damage": 20
  },
  "ranks": [
    { "arcDegrees": 45 },
    { "arcDegrees": 90 },
    { "arcDegrees": 120 },
    { "arcDegrees": 150 },
    { "arcDegrees": 180, "expansion": "wake" }
  ],
  "tempoScaling": "attackSpeed"  // maps to global tempo charm hook
}
```
- Shared between Arcade balance tables and Adventure unlock records.

## Projectile Profile
```jsonc
{
  "id": "boomerang",
  "spawnCone": 180,
  "travel": {
    "speed": 460,
    "radius": { "min": 70, "max": 160 }
  },
  "return": {
    "speedMultiplier": 1.35,
    "ignoreHeartsWhenFull": true
  }
}
```
- Used by bow/boomerang/skybrand behaviors to keep aiming consistent.

## Enemy Definition
```jsonc
{
  "id": "spider",
  "hp": 24,
  "speed": 220,
  "xp": 7,
  "behaviour": {
    "type": "charge-then-web",
    "chargeRange": 280,
    "webDuration": 1.75
  },
  "art": {
    "palette": ["#243629", "#86efac"],
    "style": "atari"
  }
}
```
- Behaviour block signals which system to execute (charge, dash, stealth, etc.).

## Stage Definition (Adventure Mode)
```jsonc
{
  "id": "forest-01",
  "name": "Forest Clearing",
  "intro": "Find the Brambleblade relic.",
  "waves": [
    { "time": 0, "spawn": [{ "enemy": "slime", "count": 6 }] },
    { "time": 45, "spawn": [{ "enemy": "spider", "count": 2 }] }
  ],
  "pickups": [
    { "time": 20, "type": "weapon", "id": "sword" }
  ],
  "unlockRewards": {
    "weapons": ["sword"],
    "stages": ["forest-02"]
  }
}
```
- Enables tooling to simulate stage flow or export balancing charts.

## Relic Definition
```jsonc
{
  "id": "tempo",
  "name": "Tempo Charm",
  "maxRank": 5,
  "effects": [
    { "rank": 1, "attackSpeed": 0.10 },
    { "rank": 5, "attackSpeed": 0.30 }
  ],
  "appliesTo": ["sword", "boomerang", "bow", "skybrand", "bomb", "spinner"]
}
```
- Captures global scaling so weapon scripts can look up modifiers uniformly.

## Art Asset Reference
```jsonc
{
  "id": "sprite.skull",
  "style": "atari",
  "frames": 2,
  "notes": "Red outline, flame trail particles lasting 0.8s."
}
```
- Lightweight way to document visual expectations before implementing new sprites.

---
Keep this file updated whenever schemas change so tooling and in-game data stay in sync. Update `ToDo.md` when new sections are required.
