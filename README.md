# Peacefully Normal, a Minecraft Mod
A Forge 1.20.1 mod named “Peacefully Normal” that implements a custom difficulty preset. When enabled, the mod re‑skins hostile mobs to custom textures, makes mobs passive unless provoked, modifies creeper behaviour, and enforces complete inter‑mob pacifism. Starvation never kills the player. All vanilla mechanics (loot, AI, animations, trading, teleportation) remain intact unless overridden by these rules.

Reskinned Mobs:
1.	Creeper
2.	Drowned
3.	Enderman
4.	Husk
5.	Pillager
6.	Skeleton
7.	Skeleton Horse
8.	Stray
9.	Witch
10.	Wither Skeleton
11.	Zombie

Key features to implement:
1.	A gamerule peacefullyNormal and commands /pn on, /pn off, /pn toggle to enable/disable the preset. Enabled by default.
2.	Automatic creation and reload of config/peacefullynormal.json with parameters: provocation_seconds, inter mob hostility flag, creeper proximity/hiss/blink settings, and arrays for keep_original_skin and disabled_mobs.
3.	Hunger stops at 1 heart; natural regeneration stays at vanilla Normal rate.
4.	Inter mob pacifism: mobs do not attack each other. Wolves ignore sheep, zombies ignore skeletons, pillagers ignore villagers, etc.
5.	Hostile mobs spawn with custom skins (except those in keep_original_skin). Mobs with original skins still follow peaceful until provoked rules.
6.	All baby zombies, baby drowned, baby husks, and chicken jockeys are disabled from spawning. Spider jockeys use re skinned riders; skeleton horseman uses a re skinned skeleton rider. Hoglin jockey uses original hoglin/piglin skins and remains passive.
7.	Peaceful until provoked: mobs only attack the player if the player deals damage to them. Provocation lasts provocation_seconds ticks. Provoking resets the timer. Mobs target only the player who provoked them.
8.	Mobs retain all vanilla abilities: skeletons shoot arrows, strays apply slowness, husks inflict hunger, witches throw potions, wither skeletons apply wither, drowned throw tridents, endermen teleport and pick up blocks.
9.	Creeper overhaul: no explosions; no swell; configurable proximity hissing (bursts and pauses) and blinking overlay; optional cat avoidance and unprovoked hiss. Creepers drop gunpowder when appropriate.
10.	Endermen ignore eye contact (only provoked by damage).
11.	Re skinned mobs never burn in daylight unless they keep original skins.
12.	Iron golems do not attack re skinned mobs unless the player provokes them.
13.	Villagers, baby villagers and trading are untouched.
14.	Environmental hazards damage mobs as in vanilla; loot and XP drops remain unaltered.
15.	Multiplayer: server enforces behaviour; clients without the mod see vanilla skins but still get passive behaviour. Clients with the mod and resource packs see re skinned visuals.

Deliverables:
•	Source code structured properly under the Forge MDK layout (src/main/java and src/main/resources), with mixins and event handlers as needed to intercept mob AI, spawning and explosion events.
•	Configuration handling for the JSON file.
•	A mods.toml file registering the mod with modId peacefullynormal.
•	A default resource pack (or code hook) for the custom villager skins and creeper overlay, allowing players to override textures.

Goal: The resulting mod must pass every step in Test Plan v1.0, including behaviour toggles, hunger limits, inter mob pacifism, provocation windows, creeper hiss/blink behaviour, mob drops, and multiplayer compatibility.
