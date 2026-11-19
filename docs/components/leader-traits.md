# Component: leader traits

## Purpose

`ui-character-traits/common/traits/` owns trait identity, modifiers, leader-class scope,
eligibility, exclusions, icon references, and selection weight for all 47 leader traits the
mod adds.

## Files

| File | Lines | Definitions | Scope declared by contained traits |
|------|-------|-------------|-----------------------------------|
| `ui-traits_leader.txt` | 43 | 1 | `{ commander scientist official }`, excluding rulers |
| `ui-traits_leader_admiral.txt` | 230 | 6 | `{ commander }`, restricted to the admiral subclass when Paragons is installed |
| `ui-traits_leader_general.txt` | 52 | 1 | `{ commander }`, restricted to the general subclass when Paragons is installed |
| `ui-traits_leader_governor.txt` | 1017 | 34 | `{ official commander scientist }` |
| `ui-traits_leader_ruler.txt` | 176 | 5 | `{ commander scientist official }`, councilor modifiers |

All five files are ASCII text.

## The 4.5 leader model

Stellaris 4.x replaced the old `admiral`, `general`, `governor` and `ruler` leader classes
with three classes — `commander`, `official` and `scientist` — plus Galactic Paragons
**subclasses**. Every vanilla 4.5 leader trait is scoped by `leader_class` and, where the
DLC is present, further narrowed by `has_trait = subclass_*` in `leader_potential_add`.

The mod follows the same pattern:

| Old concept | 4.5 expression used by this mod |
|-------------|-------------------------------|
| Admiral | `leader_class = { commander }` plus `subclass_commander_admiral` |
| General | `leader_class = { commander }` plus `subclass_commander_general` |
| Governor | `leader_class = { official commander scientist }`; the class itself governs planets |
| Ruler | `councilor_modifier`, gated on `is_ruler = yes` or a councilor subclass |

The `has_paragon_dlc = no` leg of the subclass conditions keeps every trait attainable when
the DLC is absent, matching the `OR = { has_paragon_dlc = no has_trait = subclass_… }`
shape the base game uses for its own subclass-gated traits.

## File organisation versus effective scope

Files are grouped by the old leader class for maintainability, but **effective scope is
determined solely by the `leader_class`, modifier-scope and `leader_potential_add` fields
inside each block**, not by the file the block lives in. A governor trait placed in the
admiral file would still be governor-scoped. File placement is not authoritative.

## Iterator summary

| Trait | File | Class | Modifier scope | Icon | Exclusions | Eligibility |
|-------|------|-------|----------------|------|-----------|-------------|
| `ui_trait_leader_politically_connected` | leader | c/s/o | `self_modifier` | shipped | 1 vanilla | ruler excluded; gestalt ethic excluded |
| `ui_trait_admiral_berserker` | admiral | commander | `fleet_modifier` | shipped | 3 vanilla + 1 mod | admiral subclass |
| `ui_trait_admiral_guerillero` | admiral | commander | `fleet_modifier` | shipped | 3 vanilla + 1 mod | admiral subclass |
| `ui_trait_admiral_glass_cannon` | admiral | commander | `fleet_modifier` | shipped | 1 vanilla + 1 mod | admiral subclass |
| `ui_trait_admiral_sniper` | admiral | commander | `fleet_modifier` | shipped | 1 mod | admiral subclass |
| `ui_trait_admiral_stormer` | admiral | commander | `fleet_modifier` | shipped | 1 mod | admiral subclass |
| `ui_trait_admiral_testudo` | admiral | commander | `fleet_modifier` | shipped | 1 mod | admiral subclass |
| `ui_trait_general_faith_militant` | general | commander | `army_modifier` | shipped | 2 vanilla | general subclass; spiritualist ethic |
| `ui_trait_governor_engineer` | governor | o/c/s | `planet_modifier` | vanilla | 1 mod | no Paragons; excludes intellectual, machine intelligence, physicist, sociologist |
| `ui_trait_governor_physicist` | governor | o/c/s | `planet_modifier` | vanilla | 1 mod | no Paragons; excludes intellectual, machine intelligence, engineer, sociologist |
| `ui_trait_governor_sociologist` | governor | o/c/s | `planet_modifier` | vanilla | 1 mod | no Paragons; excludes intellectual, machine intelligence, engineer, physicist |
| `ui_trait_governor_familist` | governor | o/c/s | `planet_modifier` | shipped | 1 mod | excludes hive mind |
| `ui_trait_governor_corporatist` | governor | o/c/s | `planet_modifier` | shipped | 4 mod | no governor focus |
| `ui_trait_governor_miner` | governor | o/c/s | `planet_modifier` | shipped | 4 mod | no governor focus |
| `ui_trait_governor_populist` | governor | o/c/s | `planet_modifier` | shipped | none | no governor focus |
| `ui_trait_governor_robotics_magnate` | governor | o/c/s | `planet_modifier` | shipped | 3 mod | no governor focus |
| `ui_trait_governor_environmentalist` | governor | o/c/s | `planet_modifier` | shipped | 4 mod | none |
| `ui_trait_governor_moral_authority` | governor | o/c/s | `planet_modifier` | shipped | 3 mod | excludes fanatic authoritarian, fanatic xenophobe, xenophobe, hive mind |
| `ui_trait_governor_ideologue_militarist` | governor | o/c/s | `planet_modifier` | shipped | 1 mod | excludes fanatic pacifist, hive mind |
| `ui_trait_governor_ideologue_pacifist` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic militarist, hive mind |
| `ui_trait_governor_ideologue_xenophobe` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic xenophile, hive mind |
| `ui_trait_governor_ideologue_xenophile` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic xenophobe, hive mind |
| `ui_trait_governor_ideologue_egalitarian` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic authoritarian, hive mind |
| `ui_trait_governor_ideologue_authoritarian` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic egalitarian, hive mind |
| `ui_trait_governor_ideologue_materialist` | governor | o/c/s | `planet_modifier` | shipped | 1 mod | excludes fanatic spiritualist, hive mind |
| `ui_trait_governor_ideologue_spiritualist` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | excludes fanatic materialist, hive mind |
| `ui_trait_governor_war_industrialist` | governor | o/c/s | `planet_modifier` | shipped | 7 mod | excludes fanatic pacifist |
| `ui_trait_governor_consumer_industrialist` | governor | o/c/s | `planet_modifier` | shipped | 6 mod | none |
| `ui_trait_governor_racist` | governor | o/c/s | `planet_modifier` | shipped | 3 mod | none |
| `ui_trait_governor_open_armed` | governor | o/c/s | `planet_modifier` | shipped | 2 mod | none |
| `ui_trait_governor_vicious_rumours` | governor | o/c/s | `planet_modifier` | shipped | 1 vanilla + 1 mod | none |
| `ui_trait_governor_deal_with_the_devil` | governor | o/c/s | `planet_modifier` | shipped | 1 vanilla + 1 mod | none |
| `ui_trait_governor_questionable_ethics` | governor | o/c/s | `planet_modifier` | shipped | 1 vanilla + 1 mod | excludes machine intelligence, hive mind |
| `ui_trait_governor_naturalist` | governor | o/c/s | `planet_modifier` | shipped | 1 vanilla + 4 mod | excludes machine intelligence |
| `ui_trait_governor_guns_legaliser` | governor | o/c/s | `planet_modifier` | shipped | 1 mod | none |
| `ui_trait_governor_guns_prohibitor` | governor | o/c/s | `planet_modifier` | shipped | 1 mod | none |
| `ui_trait_governor_cultural_interest` | governor | o/c/s | `planet_modifier` | shipped | 3 mod | no governor focus |
| `ui_trait_governor_fortifier` | governor | o/c/s | `planet_modifier` | shipped | none | none |
| `ui_trait_governor_settler` | governor | o/c/s | `planet_modifier` | shipped | none | no governor focus |
| `ui_trait_governor_chemist` | governor | o/c/s | `planet_modifier` | shipped | none | none |
| `ui_trait_governor_metallurgist` | governor | o/c/s | `planet_modifier` | shipped | none | none |
| `ui_trait_governor_green_energy_advocate` | governor | o/c/s | `planet_modifier` | shipped | none | excludes fanatic materialist |
| `ui_trait_ruler_backroom_backstabber` | ruler | c/s/o | `councilor_modifier` | shipped | none | ruler or councilor subclass; excludes hive mind |
| `ui_trait_ruler_smoothtalking_charmer` | ruler | c/s/o | `councilor_modifier` | shipped | none | ruler or councilor subclass; excludes hive mind |
| `ui_trait_ruler_antique_collector` | ruler | c/s/o | `councilor_modifier` | shipped | none | ruler or councilor subclass |
| `ui_trait_ruler_efficient_bureaucrat` | ruler | c/s/o | `councilor_modifier` | shipped | 1 mod | ruler or councilor subclass |
| `ui_trait_ruler_hardcore_bureaucrat` | ruler | c/s/o | `councilor_modifier` | shipped | 1 mod | ruler or councilor subclass |

`c/s/o` is shorthand for `commander scientist official`; `o/c/s` is
`official commander scientist`.

## Distribution statistics

| Property | Count |
|----------|-------|
| Definitions | 47 |
| With `opposites` | 38 |
| Without `opposites` | 9 |
| With `leader_potential_add` | 36 |
| With `selectable_weight` | 47 |
| With a declared icon | 47 (44 mod sprites, 3 vanilla sprites) |
| Declaring `leader_trait_type` | 0 (all are basic traits) |

## Structural rules

1. **No legacy class tokens.** `admiral`, `general`, `governor` and `ruler` are not valid
   `leader_class` values in 4.x. Only `commander`, `official` and `scientist` are used.
2. **Modifier scope is explicit.** Every trait names one of `fleet_modifier`, `army_modifier`,
   `planet_modifier`, `councilor_modifier` or `self_modifier`. The bare `modifier = { }`
   block, which applied to whatever the leader was assigned to, is no longer used — the
   vanilla corpus likewise has none.
3. **No `cost`, `modification`, `initial` or `randomized` fields.** These are pre-4.x leader
   trait fields. `cost` survives only in ruler-creation traits, which these are not.

## Distinctive traits

| Trait | Why it is distinctive |
|-------|----------------------|
| `ui_trait_leader_politically_connected` | Only class-agnostic trait; only trait that excludes rulers through a condition rather than a class list; the only user of `self_modifier` |
| `ui_trait_general_faith_militant` | Only army-scoped trait; only trait whose eligibility requires an ethic rather than excluding one; displayed as *Militant Faith* to avoid colliding with the vanilla `leader_trait_crusader` |
| `ui_trait_ruler_hardcore_bureaucrat` | Only trait whose entire effect is a negative modifier |
| `ui_trait_governor_war_industrialist` | Largest exclusion list (7 entries) and the most-frequently excluded target |
| `ui_trait_governor_naturalist` | Second-largest exclusion list (5 entries, 4 of them mod traits) |

## Related documents

- [Trait catalogue](./trait-catalogue.md) — full listing with localisation and modifiers
- [Data model](./../data-model.md) — field vocabulary
- [Eligibility and exclusions](./../behaviour/eligibility-and-exclusions.md)
- [Trait scoping](./../behaviour/trait-scoping.md)
- [Icons](./icons.md)
