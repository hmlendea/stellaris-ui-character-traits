# Component: icons

## Purpose

`ui-character-traits/gfx/interface/icons/traits/` supplies the DDS textures the leader trait interface renders for the mod's traits. A texture becomes live only when a trait definition names it in an `icon` field.

## Directory characteristics

| Property | Value |
|----------|-------|
| Path | `ui-character-traits/gfx/interface/icons/traits/` |
| Files | 45 DDS images |
| Subdirectories | none (flat) |
| Format | DDS (engine requirement; no runtime conversion) |
| Referenced by mod traits | 8 |
| Referenced as vanilla assets by path | 3 (`trait_natural_engineers.dds`, `trait_natural_physicists.dds`, `trait_natural_sociologists.dds`) — these are **not** shipped in this repository |
| Unreferenced shipped assets | 37 |

## Icon reference mechanism

A trait binds a texture through its `icon` field:

```text
icon = "gfx/interface/icons/traits/ui_trait_berserker.dds"
```

The engine resolves the path against the merged virtual filesystem of the base game plus all enabled mods. Two consequences follow:

1. A path shipped only by this mod resolves to the mod's file.
2. A path such as `gfx/interface/icons/traits/trait_natural_engineers.dds` resolves to the **base game's** asset, so the mod can reuse vanilla art without redistributing it.

Only 11 of 47 traits declare an `icon`. The remaining 36 inherit whatever default the engine applies to leader traits without an explicit icon. This means 37 of the 45 shipped DDS files are inert: no definition names them.

## Icon inventory

| File | Referenced by | Status |
|------|---------------|--------|
| `ui_trait_berserker.dds` | `ui_trait_admiral_berserker` | live |
| `ui_trait_crusader.dds` | `ui_trait_general_crusader` | live |
| `ui_trait_glass_cannon.dds` | `ui_trait_admiral_glass_cannon` | live |
| `ui_trait_guerillero.dds` | `ui_trait_admiral_guerillero` | live |
| `ui_trait_politically_connected.dds` | `ui_trait_leader_politically_connected` | live |
| `ui_trait_sniper.dds` | `ui_trait_admiral_sniper` | live |
| `ui_trait_stormer.dds` | `ui_trait_admiral_stormer` | live |
| `ui_trait_testudo.dds` | `ui_trait_admiral_testudo` | live |
| `ui_trait_governor_chemist.dds` | — | unused |
| `ui_trait_governor_consumer_industrialist.dds` | — | unused |
| `ui_trait_governor_corporatist.dds` | — | unused |
| `ui_trait_governor_cultural_interest.dds` | — | unused |
| `ui_trait_governor_deal_with_the_devil.dds` | — | unused |
| `ui_trait_governor_environmentalist.dds` | — | unused |
| `ui_trait_governor_familist.dds` | — | unused |
| `ui_trait_governor_fortifier.dds` | — | unused |
| `ui_trait_governor_green_energy_advocate.dds` | — | unused |
| `ui_trait_governor_guns_legaliser.dds` | — | unused |
| `ui_trait_governor_guns_prohibitor.dds` | — | unused |
| `ui_trait_governor_ideologue_authoritarian.dds` | — | unused |
| `ui_trait_governor_ideologue_egalitarian.dds` | — | unused |
| `ui_trait_governor_ideologue_materialist.dds` | — | unused |
| `ui_trait_governor_ideologue_militarist.dds` | — | unused |
| `ui_trait_governor_ideologue_pacifist.dds` | — | unused |
| `ui_trait_governor_ideologue_spiritualist.dds` | — | unused |
| `ui_trait_governor_ideologue_xenophile.dds` | — | unused |
| `ui_trait_governor_ideologue_xenophobe.dds` | — | unused |
| `ui_trait_governor_metallurgist.dds` | — | unused |
| `ui_trait_governor_miner.dds` | — | unused |
| `ui_trait_governor_moral_authority.dds` | — | unused |
| `ui_trait_governor_naturalist.dds` | — | unused |
| `ui_trait_governor_open_armed.dds` | — | unused |
| `ui_trait_governor_populist.dds` | — | unused |
| `ui_trait_governor_questionable_ethics.dds` | — | unused |
| `ui_trait_governor_racist.dds` | — | unused |
| `ui_trait_governor_robotics_magnate.dds` | — | unused |
| `ui_trait_governor_securist.dds` | — | unused (and its localisation is orphaned) |
| `ui_trait_governor_settler.dds` | — | unused |
| `ui_trait_governor_vicious_rumours.dds` | — | unused |
| `ui_trait_governor_war_industrialist.dds` | — | unused |
| `ui_trait_ruler_antique_collector.dds` | — | unused |
| `ui_trait_ruler_backroom_backstabber.dds` | — | unused |
| `ui_trait_ruler_efficient_bureaucrat.dds` | — | unused |
| `ui_trait_ruler_hardcore_bureaucrat.dds` | — | unused |
| `ui_trait_ruler_smoothtalking_charmer.dds` | — | unused |

## Naming convention

Icon filenames are **not** the trait identifiers. They use a shortened, theme-based name:

| Trait identifier | Icon filename |
|------------------|---------------|
| `ui_trait_admiral_berserker` | `ui_trait_berserker.dds` |
| `ui_trait_admiral_guerillero` | `ui_trait_guerillero.dds` |
| `ui_trait_admiral_glass_cannon` | `ui_trait_glass_cannon.dds` |
| `ui_trait_leader_politically_connected` | `ui_trait_politically_connected.dds` |

The reason the full-identifier convention was abandoned for admiral traits is not recorded; the three governor research traits instead reuse vanilla icons. A future contributor should not assume filename equals identifier.

## Other image assets

| Asset | Path | Role |
|-------|------|------|
| Mod thumbnail | `ui-character-traits/thumbnail.png` | 400x400 RGBA PNG; store/workshop listing image. Not interpreted by the engine as a trait icon. |
| Repository cover | `.github/cover.png` | GitHub listing cover art. Distribution metadata only. |

## Invariants

- Every `icon` value must resolve — either to a file under `gfx/interface/icons/traits/` in this mod, or to a base-game asset path that exists in the supported game version.
- Icon assets must be DDS. The engine does not convert other formats at runtime.
- Icon files must reside directly in `traits/`. Subdirectories would require matching path changes in every referencing trait.

## Related documents

- [Component: leader traits](./leader-traits.md)
- [Data model](./../data-model.md)
- [Change guide](./../change-guide.md)
- [Troubleshooting](./../troubleshooting.md)
