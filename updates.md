# Voxel Game

A voxel sandbox and survival game built for the original Nintendo 3DS. The v1.1 update expands the world, adds survival and creative gameplay systems, and introduces a custom PICA200 renderer, audio playback, stronger persistence, and expanded development tooling.

## Features

### Procedural World

- Large world measuring **16,000 × 16,000 × 256** blocks.
- Five biomes: Plains, Forest, Desert, Snow Taiga, and Mountain.
- Seeded Perlin terrain, with biome placement derived from moisture and temperature fields.
- Lakes with sand shores, trees with biome-dependent density, biome-specific ground surfaces, and a snow line.
- Climbable mountain terrain spanning approximately 60–160 blocks in height.
- Random 32-bit seed selection at launch; generation is deterministic for a given seed.

### Blocks and Items

The content set expanded substantially in v1.1:

- **Blocks:** 4 → 43, including ores, 14 wool colours, metal blocks, gravel, mossy cobblestone, smooth stone, leaves, bedrock, crafting tables, and water.
- **Items:** 4 → 59, including weapons, mining tools, sticks, and iron ingots.

### Survival and Combat

- Health represented by hearts, including damaged-heart states, with 20 HP.
- Enemies with randomized skins, health, melee damage, spawn searching, and respawning after the relevant toggle is enabled.
- Sword-based melee combat.
- AK and shotgun firearms with magazines, ammunition display, cooldowns, and reloads.
- Pickaxe, axe, and shovel tool classes with mining speed affected by block class.
- A mining progress bar.

### Inventory, Crafting, and Creative Mode

- 3×3 crafting grid with recipe preview and output placed in the first available hotbar slot.
- Creative inventory grid.

### Controls and Presentation

- Crosshair and splash screen.
- Adjustable render distance from 3×3 to 7×7 chunks through the settings menu.

### Music

The game includes an in-game music system supporting MP3 audio. Tracks are decoded on the console, processed to fit a bounded memory budget, and played through a shuffled playlist sourced from `./music`.

### Saving and Settings

- Versioned save system (v12 in v1.1) with CRC32 validation.
- Atomic save replacement and validation of save data.
- Incompatible generator versions are rejected rather than loaded as compatible worlds.
- Settings persist in `settings.cfg`.

## v1.0 → v1.1

Version 1.1 is a substantial expansion over v1.0:

| Area | Change |
|---|---|
| World size | 1,024 → 16,000 blocks wide; height 64 → 256 |
| World streaming | Chunk cache expanded from 5×5 to 7×7; render distance made adjustable from 3×3 to 7×7 |
| Generation | Added five biomes, lakes, biome-specific surfaces, trees, and taller climbable mountains |
| Content | Blocks increased from 4 to 43; items increased from 4 to 59 |
| Gameplay | Added enemies, melee combat, firearms, health and healing, mining tools, drops and pickups, crafting, creative inventory, and touch controls |
| Audio | Added MP3 playback and a shuffled music playlist |
| Persistence | Save format advanced from v2 to v12 with checksums, validation, and atomic replacement |
| Binary size | Reported size increased from 445 KB to 1.15 MB |

## Engine

The game runs on a custom voxel engine with a hand-written PICA200 renderer, chunk-based world streaming, procedural generation, a background generation/meshing worker, custom memory accounting, and on-device performance instrumentation.

For implementation details, rendering architecture, memory constraints, persistence, and test/tooling notes, see NOVA-engine.md .

## Platform and Performance

The project targets original Nintendo 3DS hardware and its PICA200 GPU. Development is guided by a **30 FPS performance budget**. The engine includes an on-device overlay for FPS, frame time, CPU/GPU metrics, memory usage, and chunk/mesh counters.

