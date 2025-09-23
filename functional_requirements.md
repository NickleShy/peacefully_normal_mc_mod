**Functional Requirements for the Peacefully Normal Mod**

1. **Platform & Version**:
    - Implement as a **Forge 1.20.1 mod** for Minecraft Java Edition.
    - Use Java 17 for compilation.
2. **Difficulty Preset Activation**:
    - Introduce a custom difficulty preset called **“Peacefully Normal.”**
    - Provide a gamerule peacefullyNormal that toggles the preset (true/false).
    - Provide /pn on, /pn off, and /pn toggle commands to enable or disable the preset at runtime.
    - When disabled, the game behaves exactly like vanilla.
    - When enabled, the rules below apply immediately without restart.
3. **Config File**:
    - On first world load, create config/peacefullynormal.json if it does not exist.
    - Expose configurable values including:
        - provocation_seconds (default 10) – seconds a mob remains aggressive after being hit.
        - inter_mob_hostility (default false) – whether mobs attack each other (should default to false).
        - creeper.proximity_radius (default 3.0) and creeper.exit_radius (default 3.5) – distance thresholds for creeper hissing/blinking.
        - creeper.hiss_min_seconds (default 0.3) and creeper.hiss_max_seconds (default 0.9) – min/max hiss burst durations.
        - creeper.pause_min_seconds (default 0.3) and creeper.pause_max_seconds (default 0.9) – min/max pause durations between hiss bursts.
        - creeper.allow_unprovoked_hiss (default true) – whether creepers hiss when a player is near even if not hit.
        - creeper.blink_overlay_enabled (default true) – whether to flash the creeper’s overlay (blinking lights).
        - creeper.respect_cat_avoidance (default true) – whether creepers avoid cats.
        - Arrays keep_original_skin (mobs that use vanilla skins) and disabled_mobs (mobs that do not spawn).
    - Reload the config dynamically via /pn toggle without restarting the game.
4. **Hunger & Health**:
    - Starvation cannot kill the player. Health stops dropping at **1 heart** (2 HP).
    - Natural regeneration functions exactly as vanilla on Normal difficulty.
5. **Inter‑Mob Pacifism**:
    - All mobs ignore other mobs; hostile mobs do **not** attack other hostiles, neutral mobs, passive mobs, or villagers.
    - Examples: wolves never hunt sheep; drowned never attack axolotls; zombies and skeletons do not fight each other; pillagers and vindicators do not attack villagers until provoked by the player.
6. **Re‑Skinning & Appearance**:
    - All hostile mobs (unless specified in keep_original_skin) spawn with **custom textures**.
    - These re‑skinned mobs retain the **animations, pathfinding, AI, and sounds** of the underlying vanilla mob.
    - Held items and combat animations (bow draw, crossbow reload, axe swing, potion throw, trident throw) must appear in the villager’s hands.
    - Use a resource‑pack friendly approach so users can replace textures
    - Spiders and zombie villagers remain unmodified (they keep vanilla skins), but they still follow the peaceful‑until‑provoked rules.
7. **Mob Spawning Rules**:
    - Baby zombies, baby drowned, baby husks, and chicken jockeys are **disabled** from spawning.
    - Spider jockeys: spider retains vanilla skin; rider uses a re‑skinned skeleton/stray/wither skeleton depending on biome.
    - Skeleton horsemen: horse uses vanilla horse, horse_white.png; skeleton rider uses re‑skinned skeleton skin.
    - Hoglin jockeys (baby piglin riding a hoglin) spawn with original hoglin/piglin skins and follow the peaceful‑until‑provoked behaviour.
    - Baby piglins and baby hoglins spawn (as custom skins) but remain passive unless provoked.
    - Other hostile spawn rules match vanilla.
8. **Pacifism Toward Players (Provocation Mechanic)**:
    - Hostile mobs **do not attack players** unless the player damages them (melee or projectile).
    - When a player hits a mob, that mob becomes aggressive towards that player for provocation_seconds ticks.
    - Hitting the mob again resets the timer.
    - Only the player who provoked it is targeted; other players remain ignored (Multiplayer).
    - After the timer expires (no further damage), the mob stops attacking and returns to passive behaviour.
9. **Normal Loot & XP**:
    - Re‑skinned mobs drop **vanilla loot and experience**. Nothing is added or removed.
    - Advancements such as “Monster Hunter” must trigger as normal when killing re‑skinned mobs.
10. **Daylight Behaviour**:
    - Re‑skinned mobs **do not burn** in sunlight.
    - This must be configurable if needed via the keep_original_skin list (e.g., re‑enable burning by keeping the original skin).
11. **Special Mob Behaviours**:
    - Husks: remain passive until hit but inflict Hunger on attack.
    - Strays: remain passive until hit but shoot arrows of Slowness.
    - Wither skeletons: remain passive until hit but inflict the Wither effect.
    - Witches: remain passive until hit but drink healing potions and throw harmful potions.
    - Blazes: remain passive until hit but hover and shoot fireballs.
    - Drowned: remain passive until hit but swim normally and throw tridents when provoked; drop tridents at vanilla rate.
    - Pillagers & Vindicators: remain passive until hit; pillagers reload and fire crossbows; vindicators swing axes.
    - Piglins & Hoglins: remain passive until hit; behave normally when provoked but do not attack each other; piglin brutes wield golden axes.
    - Endermen: do not aggro upon eye contact; only become aggressive when hit; continue teleporting as usual; can carry blocks.
    - Iron golems do not attack re‑skinned mobs unless the player provokes them (e.g., by attacking villagers/golems).
12. **Creeper Behaviour**:
    - Re‑skinned creepers **never explode**; explosion events must be cancelled server‑side.
    - Creeper swell timer is clamped to zero (no flashing).
    - Creepers avoid cats (respecting creeper.respect_cat_avoidance), if set true.
    - When a player enters the creeper.proximity_radius (default 3 m), creepers emit short hiss bursts (randomly 0.3–0.9 s) with random pauses (0.3–0.9 s) while the player remains within range.
    - Blink the creeper’s overlay (creeper_armor.png) during the proximity warning; blink control can be disabled via blink_overlay_enabled.
    - Define allow_unprovoked_hiss to toggle whether creepers hiss without being hit.
    - Creepers drop normal loot (gunpowder, music discs when killed by skeletons) and take normal damage.
    - Hitting a creeper provokes it for provocation_seconds but does not reintroduce explosion.
    - Configurable creeper.proximity_radius, exit_radius, hiss_min_seconds, hiss_max_seconds, and pause durations.
13. **Command & Config Reload**:
    - /pn on, /pn off, /pn toggle must switch the preset on or off and reload the configuration.
    - Changing values in peacefullynormal.json and toggling the preset must apply new settings in the current session (no restart).
14. **Resource Pack & Models**:
    - The mod must support external resource packs for re‑skinned textures.
    - When the mod is installed on a server only, clients without the mod will see vanilla skins but will still experience pacifist behaviour; clients with the mod will see the re‑skinned visuals.
15. **Non‑interference with Villagers**:
    - Normal villagers, baby villagers and trading mechanics must remain unaffected.
    - Baby villagers must not be re‑skinned; they use vanilla textures.
    - The mod must not alter villager breeding or trading.
16. **Environmental Hazards**:
    - Lava, cacti, fall damage, drowning and other environmental hazards damage re‑skinned mobs exactly like vanilla.
    - Mobs die and drop loot normally.
17. **Multiplayer Compatibility**:
    - All behaviour changes must be enforced server‑side.
    - Clients without the mod should still experience peaceful‑until‑provoked behaviour but see vanilla models.
    - Clients with the mod and resource packs should see re‑skinned visuals and get the pacifist behaviour.
