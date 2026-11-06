# Credits / Attribution

This project is built on the **Cat's Godot 4 Modular Souls-like Template**
(original: CC0 / Unlicense — see upstream README).

## Textures (PBR materials)

Source: [Poly Haven](https://polyhaven.com/) — **CC0 License** (no attribution required,
but credited here per our project policy). All downloaded at 2K resolution,
jpg format (diffuse / normal-GL / roughness). Displacement maps included but
not yet wired into the materials.

| Material slot | Poly Haven asset | URL |
|---|---|---|
| Wall (TinyBrick01) | medieval_blocks_03 | https://polyhaven.com/a/medieval_blocks_03 |
| Stone floor (TinyRock01) | cobblestone_floor_001 | https://polyhaven.com/a/cobblestone_floor_001 |
| Wood (TinyWood01) | plank_flooring_03 | https://polyhaven.com/a/plank_flooring_03 |
| Metal (TinyMetal01) | rusty_metal_02 | https://polyhaven.com/a/rusty_metal_02 |
| Barrel wood (TinyWood02) | brown_planks_04 | https://polyhaven.com/a/brown_planks_04 |

Notes:
- Normal maps use the OpenGL (`nor_gl`) orientation, matching Godot's convention.
- Roughness jpg maps are flagged `process/srgb=false` in their `.import` so they
  are read as linear data, not sRGB color.
- AO maps were not present in the 2K Blend bundles; ambient occlusion is handled
  by Godot's SDFGI instead.

### Wood variants (barrel vs crate)
- The barrel (`barrel01`) and crate (`crate01`) originally shared the same wood
  material (`TinyWood01` = plank_flooring_03). To make them visually distinct,
  the barrel's wood surface now uses a dedicated dark-oak PBR
  (`TinyWood02` = brown_planks_04), while the crate keeps the lighter
  weathered plank. Both are Poly Haven CC0, 2K jpg.

## License

Project code derived from the template: see upstream LICENSE (CC0 / Unlicense).
Textures: CC0 via Poly Haven.
