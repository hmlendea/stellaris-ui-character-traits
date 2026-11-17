# Component: leader traits

## Purpose

`ui-character-traits/common/traits/` owns trait identity, cost, modifiers, leader-class scope, eligibility, exclusions, and icon references for all 47 leader traits the mod adds.

## Files

| File | Lines | Definitions | Scope declared by contained traits |
|------|-------|-------------|-----------------------------------|
| `ui-traits_leader.txt` | 24 | 1 | `all` pool, `{ admiral scientist general governor }` classes |
| `ui-traits_leader_admiral.txt` | 77 | 6 | `{ admiral }` |
| `ui-traits_leader_general.txt` | 21 | 1 | `{ general }` |
| `ui-traits_leader_governor.txt` | 653 | 34 | `{ governor }` |
| `ui-traits_leader_ruler.txt` | 72 | 5 | `{ ruler }` |

All five files are ASCII text.

## File organisation versus effective scope

Files are grouped by leader class for maintainability, but **effective scope is determined solely by the `leader_trait` and `leader_class` fields inside each block**, not by the file the block lives in. A governor trait placed in the admiral file would still be governor-scoped. This separation is deliberate but means file placement is not authoritative.

`ui-traits_leader.txt` holds the one class-agnostic trait; it is the only file whose name has no class suffix and whose trait declares `leader_trait = all`.

## Iterator summary

| Trait | File | Classes | Pool | Icon | Exclusions | Eligibility | `modification` | Modifiers |
|-------|------|---------|------|------|-----------|-------------|----------------|-----------|
| `ui_trait_leader_politically_connected` | leader | admiral, scientist, general, governor | `all` | shipped | 1 vanilla | ruler excluded; gestalt excluded | not set | 2 |
| `ui_trait_admiral_berserker` | admiral | admiral | admiral | shipped | 2 vanilla + 1 mod | none | not set | 2 |
| `ui_trait_admiral_guerillero` | admiral | admiral | admiral | shipped | 2 vanilla + 1 mod | none | not set | 4 |
| `ui_trait_admiral_glass_cannon` | admiral | admiral | admiral | shipped | 1 vanilla + 1 mod | none | not set | 2 |
| `ui_trait_admiral_sniper` | admiral | admiral | admiral | shipped | 1 mod | none | not set | 4 |
| `ui_trait_admiral_stormer` | admiral | admiral | admiral | shipped | 1 mod | none | not set | 4 |
| `ui_trait_admiral_testudo` | admiral | admiral | admiral | shipped | 1 mod | none | not set | 2 |
| `ui_trait_general_crusader` | general | general | general | shipped | none | spiritualist or fanatic spiritualist | not set | 2 |
| `ui_trait_governor_engineer` | governor | governor | governor | vanilla | 1 mod | excludes intellectual, machine intelligence, physicist, sociologist | no | 1 |
| `ui_trait_governor_physicist` | governor | governor | governor | vanilla | 1 mod | excludes intellectual, machine intelligence, engineer, sociologist | no | 1 |
| `ui_trait_governor_sociologist` | governor | governor | governor | vanilla | 1 mod | excludes intellectual, machine intelligence, engineer, physicist | no | 1 |
| `ui_trait_governor_familist` | governor | governor | governor | — | 1 mod | excludes hive mind | no | 1 |
| `ui_trait_governor_corporatist` | governor | governor | governor | — | 4 mod | none | no | 1 |
| `ui_trait_governor_miner` | governor | governor | governor | — | 4 mod | none | no | 1 |
| `ui_trait_governor_populist` | governor | governor | governor | — | none | none | no | 1 |
| `ui_trait_governor_robotics_magnate` | governor | governor | governor | — | 3 mod | none | no | 2 |
| `ui_trait_governor_environmentalist` | governor | governor | governor | — | 4 mod | none | no | 1 |
| `ui_trait_governor_moral_authority` | governor | governor | governor | — | 3 mod | excludes fanatic authoritarian, fanatic xenophobe, xenophobe, hive mind | no | 3 |
| `ui_trait_governor_ideologue_militarist` | governor | governor | governor | — | 1 mod | excludes fanatic pacifist, hive mind | no | 2 |
| `ui_trait_governor_ideologue_pacifist` | governor | governor | governor | — | 2 mod | excludes fanatic militarist, hive mind | no | 2 |
| `ui_trait_governor_ideologue_xenophobe` | governor | governor | governor | — | 2 mod | excludes fanatic xenophile, hive mind | no | 2 |
| `ui_trait_governor_ideologue_xenophile` | governor | governor | governor | — | 2 mod | excludes fanatic xenophobe, hive mind | no | 2 |
| `ui_trait_governor_ideologue_egalitarian` | governor | governor | governor | — | 2 mod | excludes fanatic authoritarian, hive mind | no | 2 |
| `ui_trait_governor_ideologue_authoritarian` | governor | governor | governor | — | 2 mod | excludes fanatic egalitarian, hive mind | no | 2 |
| `ui_trait_governor_ideologue_materialist` | governor | governor | governor | — | 1 mod | excludes fanatic spiritualist, hive mind | no | 2 |
| `ui_trait_governor_ideologue_spiritualist` | governor | governor | governor | — | 2 mod | excludes fanatic materialist, hive mind | no | 2 |
| `ui_trait_governor_war_industrialist` | governor | governor | governor | — | 7 mod | excludes fanatic pacifist | no | 1 |
| `ui_trait_governor_consumer_industrialist` | governor | governor | governor | — | 6 mod | none | no | 1 |
| `ui_trait_governor_racist` | governor | governor | governor | — | 3 mod | none | no | 1 |
| `ui_trait_governor_open_armed` | governor | governor | governor | — | 2 mod | none | no | 1 |
| `ui_trait_governor_vicious_rumours` | governor | governor | governor | — | 1 vanilla + 1 mod | none | no | 1 |
| `ui_trait_governor_deal_with_the_devil` | governor | governor | governor | — | 1 vanilla + 1 mod | none | no | 2 |
| `ui_trait_governor_questionable_ethics` | governor | governor | governor | — | 1 vanilla + 1 mod | excludes machine intelligence, hive mind | no | 6 |
| `ui_trait_governor_naturalist` | governor | governor | governor | — | 2 vanilla + 4 mod | excludes machine intelligence | no | 6 |
| `ui_trait_governor_guns_legaliser` | governor | governor | governor | — | 1 mod | none | no | 4 |
| `ui_trait_governor_guns_prohibitor` | governor | governor | governor | — | 1 mod | none | no | 4 |
| `ui_trait_governor_cultural_interest` | governor | governor | governor | — | 1 vanilla + 2 mod | none | no | 2 |
| `ui_trait_governor_fortifier` | governor | governor | governor | — | none | none | no | 2 |
| `ui_trait_governor_settler` | governor | governor | governor | — | none | none | no | 2 |
| `ui_trait_governor_chemist` | governor | governor | governor | — | none | none | no | 2 |
| `ui_trait_governor_metallurgist` | governor | governor | governor | — | none | none | no | 2 |
| `ui_trait_governor_green_energy_advocate` | governor | governor | governor | — | none | excludes fanatic materialist | no | 2 |
| `ui_trait_ruler_backroom_backstabber` | ruler | ruler | ruler | — | none | excludes hive mind authority | yes | 2 |
| `ui_trait_ruler_smoothtalking_charmer` | ruler | ruler | ruler | — | none | excludes hive mind authority | yes | 1 |
| `ui_trait_ruler_antique_collector` | ruler | ruler | ruler | — | none | none | yes | 3 |
| `ui_trait_ruler_efficient_bureaucrat` | ruler | ruler | ruler | — | 1 mod | none | yes | 1 |
| `ui_trait_ruler_hardcore_bureaucrat` | ruler | ruler | ruler | — | 1 mod | none | yes | 1 |

## Distribution statistics

| Property | Count |
|----------|-------|
| Definitions | 47 |
| With `opposites` | 37 |
| Without `opposites` | 10 |
| With `leader_potential_add` | 21 |
| With `modification = no` | 39 |
| With `icon` | 11 (8 shipped, 3 vanilla) |
| With `initial` and `randomized` | 1 |
| Declaring `cost = 1` | 47 |

## Distinctive traits

| Trait | Why it is distinctive |
|-------|----------------------|
| `ui_trait_leader_politically_connected` | Only class-agnostic trait; only `leader_trait = all`; only `initial`/`randomized`; only trait that excludes rulers through a condition rather than a class list |
| `ui_trait_general_crusader` | Only general trait; only trait whose eligibility requires an ethic rather than excluding one |
| `ui_trait_ruler_hardcore_bureaucrat` | Only trait whose entire effect is a negative modifier |
| `ui_trait_governor_naturalist` | Largest exclusion list (6 entries) and the trait others mutually exclude against |
| `ui_trait_governor_war_industrialist` | Second-largest exclusion list (7 entries) and the most-frequently excluded target |

## Related documents

- [Trait catalogue](./trait-catalogue.md) — full alphabetical listing with localisation
- [Data model](./../data-model.md) — field vocabulary
- [Eligibility and exclusions](./../behaviour/eligibility-and-exclusions.md)
- [Trait scoping](./../behaviour/trait-scoping.md)
- [Icons](./icons.md)
