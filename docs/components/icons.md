# Component: icons

## Purpose

`ui-character-traits/gfx/interface/icons/traits/` supplies the DDS textures the leader trait
interface renders for the mod's traits, and `ui-character-traits/interface/` declares the
sprites that expose those textures to the engine. A texture becomes live only when a trait
definition names a sprite that resolves to it.

## Directory characteristics

| Property | Value |
|----------|-------|
| Texture path | `ui-character-traits/gfx/interface/icons/traits/` |
| Sprite definitions | `ui-character-traits/interface/ui_character_traits.gfx` |
| Texture files | 45 DDS images |
| Subdirectories | none (flat) |
| Format | DDS, uncompressed ARGB8888, 29x29 — the size the base game uses for leader trait icons |
| Traits with a declared icon | 47 of 47 |
| Sprites declared by this mod | 44 (one per referenced shipped texture) |
| Vanilla sprites reused | 3 (`GFX_leader_trait_engineering_focus`, `GFX_leader_trait_physics_focus`, `GFX_leader_trait_society_focus`) |
| Unreferenced shipped assets | 1 (`ui_trait_governor_securist.dds`) |

## Icon reference mechanism

Since Galactic Paragons, and therefore throughout Stellaris 4.x, leader trait icons are
declared through the `trait/icon` inline script rather than through a raw texture path. A
trait names a **sprite**, and the sprite maps to a texture file:

```text
inline_script = {
    script = trait/icon
    CLASS = official
    ICON = "GFX_ui_trait_governor_miner"
    RARITY = common
    COUNCIL = no
    TIER = 1
}
```

The sprite itself is declared in `interface/ui_character_traits.gfx`:

```text
spriteType = {
    name = "GFX_ui_trait_governor_miner"
    texturefile = "gfx/interface/icons/traits/ui_trait_governor_miner.dds"
}
```

`trait/icon` composes a layered icon: the shared trait background, the rarity glow and frame,
the trait artwork, the councilor frame, and the tier pips. The mod therefore ships no GUI
code; it supplies sprites and lets the vanilla script handle composition.

### Why the mod no longer uses a raw `icon = "…dds"` path

Before 4.x a trait could name a texture path directly. That field is no longer part of the
leader trait document: none of the vanilla 4.5 leader trait files use it. The current form is
the sprite indirection above.

### Tint handling

`trait/icon` tints the artwork layer with `trait_icon_default`. The base game's icons are
mostly greyscale masks, which is what that tint is designed for. The mod's icons are already
full-colour artwork, and the engine renders them correctly through the same script — the
vanilla set includes a handful of coloured icons (`storm_rider.dds`, `intemporal.dds`) that
rely on it too. No mod-specific icon script is therefore needed.

## Icon inventory

| Sprite | Texture | Used by |
|--------|---------|---------|
| `GFX_ui_trait_berserker` | `ui_trait_berserker.dds` | `ui_trait_admiral_berserker` |
| `GFX_ui_trait_guerillero` | `ui_trait_guerillero.dds` | `ui_trait_admiral_guerillero` |
| `GFX_ui_trait_glass_cannon` | `ui_trait_glass_cannon.dds` | `ui_trait_admiral_glass_cannon` |
| `GFX_ui_trait_sniper` | `ui_trait_sniper.dds` | `ui_trait_admiral_sniper` |
| `GFX_ui_trait_stormer` | `ui_trait_stormer.dds` | `ui_trait_admiral_stormer` |
| `GFX_ui_trait_testudo` | `ui_trait_testudo.dds` | `ui_trait_admiral_testudo` |
| `GFX_ui_trait_crusader` | `ui_trait_crusader.dds` | `ui_trait_general_faith_militant` |
| `GFX_ui_trait_politically_connected` | `ui_trait_politically_connected.dds` | `ui_trait_leader_politically_connected` |
| `GFX_leader_trait_engineering_focus` | vanilla | `ui_trait_governor_engineer` |
| `GFX_leader_trait_physics_focus` | vanilla | `ui_trait_governor_physicist` |
| `GFX_leader_trait_society_focus` | vanilla | `ui_trait_governor_sociologist` |
| `GFX_ui_trait_governor_<name>` | `ui_trait_governor_<name>.dds` | the remaining 31 governor traits |
| `GFX_ui_trait_ruler_<name>` | `ui_trait_ruler_<name>.dds` | the 5 ruler traits |

Every sprite name is formed mechanically as `GFX_` plus the texture filename stem, except for
the three governor research traits, which reuse vanilla focus art instead of the shipped
`ui_trait_governor_engineer/physicist/sociologist` textures.

## Known asset leftovers

`ui_trait_governor_securist.dds` has no trait definition and no sprite, because the trait it
was drawn for was never defined. Its localisation keys are likewise orphaned. The asset is
retained for a possible future trait rather than deleted.

## Naming convention

Icon filenames are **not** the trait identifiers. They use a shortened, theme-based name:

| Trait identifier | Icon filename |
|------------------|---------------|
| `ui_trait_admiral_berserker` | `ui_trait_berserker.dds` |
| `ui_trait_admiral_guerillero` | `ui_trait_guerillero.dds` |
| `ui_trait_admiral_glass_cannon` | `ui_trait_glass_cannon.dds` |
| `ui_trait_leader_politically_connected` | `ui_trait_politically_connected.dds` |

A future contributor should not assume filename equals identifier. The sprite name is the
stable contract; the texture path is an implementation detail behind it.

## Other image assets

| Asset | Path | Role |
|-------|------|------|
| Mod thumbnail | `ui-character-traits/thumbnail.png` | 400x400 RGBA PNG; store/workshop listing image. Not interpreted by the engine as a trait icon. |
| Repository cover | `.github/cover.png` | GitHub listing cover art. Distribution metadata only. |

## Invariants

- Every `ICON` value must name a sprite that exists — either in the mod's
  `interface/ui_character_traits.gfx` or in a base-game `.gfx` file.
- Every sprite the mod declares must point at a texture it actually ships.
- Icon textures must be DDS. The engine does not convert other formats at runtime.
- Icon textures must be 29x29 to match the base game's leader trait icon size; a different
  size scales unpredictably inside the layered icon.

## Related documents

- [Component: leader traits](./leader-traits.md)
- [Data model](./../data-model.md)
- [Change guide](./../change-guide.md)
- [Troubleshooting](./../troubleshooting.md)
