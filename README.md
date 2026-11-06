
# Cat's Godot 4 Souls-Like Template & Asset Pack

**NOTICE! VERSION 3.0 IS PENDING RELEASE WHICH WILL BE A TOTALLY DIFFERENT CODEBASE AND APPROACH, THIS OLD VERISON IS PENDING TO BE REPLACED BY IT ENTIRELY**

Version 2.0.0

IF YOU NEED THE NON-ROOT VERSION, CHECK THE RELEASES FOR ANY v1.x.x bundle.


![Controller Screenshot](https://raw.githubusercontent.com/catprisbrey/Cats-Godot4-Modular-Souls-like-Template/main/screenshots/combat.png)

[YouTube Overview Video](https://www.youtube.com/watch?v=6WdAxzw8pnE)

A highly modular, loosely coupled soulslike game template/asset pack for the Godot Engine. It's driven heavily using signals and loose code, and the tree uses an animation library to drive it's animations. This allows you to swap in your own compatible models and animations quickly and not break the logic of the code. All you need is  a  model with a standard Godot/Unity/Mixamo etc, skeleton mapped into Godot at import.

All CC0 content free to be used as you wish without attribution. Although I'll very gratefully be attributed in credits and/or humbly accept your donations.

This template uses assets created entirely by myself, or from Kenney Assets. Nothing from Mixamo, etc to muddy up the licensing waters.

## Features

The accumulation of about a years worth of testing. It features a lot of the classic mechanics for soulslike games:

- Root motion driven player and enemies
- Primary weapon
- Offhand gadgets 
- Consumable items
- Enemy targeting
- Enemy knockback
- Blocking / perfect parry
- Dodge rolling
- Sprinting
- Ladder Movement
- Lever activated intractables
- Enemys with multiple states and pathfinding
- Ragdoll death
- Joystick and Keyboard controls based off Elden Ring/Bloodborne

## Assets:

- Rigged Low poly male and female model
- Low resolution textures
- Lots of sound effects and music
- 110+ animations
- Gridmap/Meshlibrary
- Flexible nested animation state trees


## License

[Creative Commons, but be cool about it](https://choosealicense.com/licenses/unlicense)
Consider donating me a coffee or crediting/thanking me in a game you make with it :)

---

# 本地工作笔记（本项目追加，不影响上游 CC0/Unlicense）

> 本目录是 catprisbrey/Cats-Godot4-Modular-Souls-like-Template 的本地工作副本。
> 规划：自己动手做类魂游戏，fork 后自己也开源、不闭源。

## A. 环境 / 路径（本机踩坑后定稿）

| 项 | 路径 |
|---|---|
| Godot 4.7.2 便携版（exe 直装，绿色） | `E:\gamedev\engine\Godot_v4.7.2-stable_win64.exe` |
| 项目根目录 | `E:\gamedev\soulslike-template\Cats-Godot4-Modular-Souls-like-Template-main\` |
| 主场景 | `res://demo_level/world_castle.tscn` |
| 含 GridMap 的 demo 场景 | `res://demo_level/stagingCSG.tscn` |

- **C 盘别装东西**：本机 C 只剩 ~33G，Godot 与项目全放 E 盘。
- 机器：Ryzen 5 5600 / 16G / RX 6750 GRE 10G。Godot 4 + 低面数 CC0 路线很轻，不用降档。

## B. 已修复的上游 Bug（重要，clone 下来就会炸）

**现象**：导入 `demo_level/gridmap/tilemap_basic.glb` 时报
`ERROR: Cannot open file 'res://gridmap/gridmap_materials/TinyBrick01.tres'`（TinyBrick01/02）。

**根因**：材质/贴图实际在 `res://demo_level/gridmap/gridmap_materials/`，`gridmap_basic.tres`(MeshLibrary) 引用路径也正确；
唯独 `tilemap_basic.glb.import` 里 **7 处** `use_external/path` 写成少一级 `demo_level/` 的
`res://gridmap/gridmap_materials/...`，导致 GLB 导入找不到材质 → 主场景那个 GridMap 块缺材质。

**修复**：`demo_level/gridmap/tilemap_basic.glb.import` 中 7 行 `res://gridmap/gridmap_materials/`
全部改为 `res://demo_level/gridmap/gridmap_materials/`（补 `demo_level/` 一级）。
删旧缓存 `.godot/imported/tilemap_basic.glb-*.scn` 后重导，stderr 无 TinyBrick/gridmap/Failed loading 报错，
`import.err` 不再生成 → 导入干净。

> 上游打包路径写死漏一级目录（作者本机路径结构不同没暴露）。正式 fork 时建议把这个 fix 一并带上 / 提 PR。

## C. 引擎与「至臻」配置思路

- **不选 UE5/Lumen（吃 32G 不现实）、不选 Unity HDRP（偏重）**，锁定 **Godot 4（Forward+）**。
- 「至臻完美」≠ 堆多边形：参考《黑暗之魂重制版》——几何其实是 PS3 低模，重置版主要做
  **①贴图拉到 2K 未压缩 PBR ②重做光照和雾**，质感 90% 来自 2K 贴图 + 打光 + 雾。
- 出魂系氛围的开关：SDFGI（实时全局光照）、体积雾/距离雾、Poly Haven HDRI（真实天光灵魂）、法线/粗糙/AO 齐全。
- 显存预算：一套 2K PBR ≈ 64MB，50 套 ≈ 3.2GB，不到 10G 显存三分之一；关键道具可上 4K；1080p 原生稳。

## D. 素材来源（CC0 / 免费，已核实存在）

**几何 / 模型（中世纪奇幻 + 纯中世纪写实 两条都收）**
- Kenney RPG / Medieval / Fantasy（**CC0**，免署名）
- Quaternius Medieval Village + LowPoly Medieval Weapons（免费近 CC0）
- OpenGameArt：Castle Kit（混）、CC0 Buildings Kit（**CC0**）
- itch.io：Free Medieval 3D People；CC0 tagged Medieval 筛选页
- BlendSwap：3D Medieval；Sketchfab：CC0 标签中世纪模型

**PBR 材质 / HDRI**：ambientCG（**CC0**）、Poly Haven（**CC0** PBR+HDRI+模型）、cc0-textures.com（备用）
**音乐 / 音效**：Free Music Archive / ccMixter / Freesound（混 CC，**注意 NC 不能商用**）

**雷区**：CC-BY 要留 CREDITS/ATTRIBUTION；CC-BY-NC 不能商用。流程：fork 跑通灰盒 → 照清单统一换皮 → 留 CREDITS。

## E. fork / 再分发协议速查（自己做开源）

- MIT/BSD/Apache：任意开源协议发，留 LICENSE + 声明。
- GPL/AGPL：必须同协议开源（传染性）。
- LGPL/MPL：改库部分开源。
- CC0：随便用。
- 无 LICENSE：不能发修改版（无再分发授权），只可本地学或去要授权。

## F. 下一步（待办）

- [ ] 本机双击 Godot 跑灰盒，确认 `world_castle` 手感（主场景 GridMap 材质已修）。
- [ ] 照第 D 节清单统一换皮，整批同调性。
- [ ] 写 CREDITS 文件。
- [ ] （可选）正式 fork + 把这个 import 路径 fix 提 PR 回上游。

