# Peacefully Normal — CHANGELOG.md

---

## v0.11.005 (Current)

### Summary
Stabilized client/server parity, reintroduced creeper hiss and blink, fixed in-game config behavior, and restored all textures.  
This marks the first fully stable release of the modernized Forge 1.20.1 build.

---

### Added
- **Client-side overlay system**
  - Implemented `PNCreeperClient.java` and `PNClientInit.java`.
  - Added smooth overlay blink using `creeper_armor.png`.
  - Blink cadence driven by proximity instead of explosion swell.
  - Textures embedded into JAR:
    - `assets/peacefullynormal/textures/entity/creeper/creeper.png`
    - `assets/peacefullynormal/textures/entity/creeper/creeper_armor.png`
- **Resource helper system**
  - Added `PNResourceHelper.java` for mod-namespace lookups.
  - Functions: `mine()` and `mineExists()` provide resource-safe access.
  - Compatible with both `assets/peacefullynormal/...` and `assets/minecraft/...` paths.
- **UI / Config**
  - Rebuilt in-game config screen (`PNConfigScreen.java`) with tabs:  
    General • Triggers • Visuals • Creeper • Lists
  - Buttons realigned; tab switching clears correctly.
  - Boolean toggles and numeric fields update instantly.
  - Added live field validation, labels, and spacing.
- **Embedded textures**
  - All textures now shipped inside the mod JAR.
  - External texture pack optional; overrides still supported.

---

### Fixed
- **B4.0**  Zombies and skeletons now burn in daylight again.  
- **B5.0**  Creeper hiss restored via state machine.  
- **B6.0**  Creeper overlay blinks correctly, replacing vanilla flash.  
- **B7.0**  Nearby player actions no longer trigger aggression.  
- **B8.0**  Fixed missing textures (namespace corrected).  
- **B10.0**  Reintroduced complete config UI.  
- **B10.1 – B10.3**  Tab refresh, default highlight, and misaligned text fixed.

---

### Updated Config Defaults
```
passive_until_provoked = true
provocation_seconds    = 10
on_player_action_radius = 0.0
cancel_explosion       = true
force_no_swell         = true
respect_cat_avoidance  = true
```

---

### Added removed_mobs list
```
removed_mobs = [
  "minecraft:chicken_jockey",
  "minecraft:zombie[baby=true]",
  "minecraft:zombified_piglin[baby=true]",
  "minecraft:zombie_villager[baby=true]",
  "minecraft:drowned[baby=true]",
  "minecraft:husk[baby=true]"
]
```

---

#### Config behavior
- In-game config and TOML sync in both directions.  
- Reads on startup, writes on change.  
- Hiss cadence and proximity radius restored.  
- Mirrored JSON created at `/config/peacefullynormal.json`.

---

### Known Issues / Next Phase
- Add config hot-reload (live update mid-session).  
- Center labels and improve UI styling.  
- Finalize `PNTextureOverrides` fallback system.  
- Extend `removed_mobs` to variants (e.g., slimes by size).  
- Multiplayer sync pending; single-player verified.

---

## v0.11.004
### Fixed
- Resolved B10.1–B10.3 UI refresh and tab alignment.  
- Config defaults now stable across reloads.  
- Confirmed proper client/server code separation.

---

## v0.11.003
### Fixed
- Removed baby variants via `EntityJoinLevelEvent` discard.  
- Prevented chicken jockey aliasing.  
- No crashes or missing texture exceptions found in event handlers.

---

## v0.11.002
### Fixed
- Fixed `EventPriority.HIGHEST` mismatch that blocked builds.  
- Updated `build.gradle` for automatic version naming.

---

## v0.11.001
### Added
- Introduced new config handler (`PNConfig.java`) with synchronized TOML schema.  
- Improved parameter descriptions and comments.  
- Added client/server config registration via `PNConfig.register()`.

---

## v0.11.000
### Added
- Rebuilt mod in IntelliJ using Forge 47.4.0 (Java 17).  
- Organized structure:
  ```
  peacefullynormal/
  ├── config/
  ├── client/
  ├── event/
  └── command/
  ```
- Introduced modular event handling and proper side separation.

---

## v0.10.000 (Baseline Reference)
### Behavior
- Passive-until-provoked working for zombies.  
- Creepers hiss and blink with vanilla white flash.  
- All mobs use custom textures.  
- Explosions disabled.  
- Early TOML/JSON config without UI.

---

### Notes
Versions **v0.10 → v0.11.005** mark full modernization:  
- Config migrated from JSON to TOML.  
- In-game configuration implemented.  
- Event handling modularized.  
- Embedded texture system added.  
- Compatible with Forge 1.20.1.

---

### Credits
**Project:** Peacefully Normal (Forge 1.20.1)  
**Developer:** Catherine “Cat” Phillips  
**Collaboration:** ChatGPT (GPT-5)  
**Status:** Actively maintained — modular threads in use for performance optimization.

