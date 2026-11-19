# Behaviour: modifiers and effects

## What a modifier block does

Every trait declares one explicitly scoped modifier block of scalar `key = value` pairs:

```text
fleet_modifier = {
    ship_weapon_damage = 0.15
    ship_disengage_chance_mult = -0.25
}
```

The engine applies these as static modifiers to the named scope while the leader holds the
trait. The scope is chosen once per trait: `planet_modifier` for governor traits,
`fleet_modifier` for admiral traits, `army_modifier` for the general trait, `councilor_modifier`
for ruler traits, and `self_modifier` for the one leader-intrinsic trait. The unscoped
`modifier` block is not used, because in 4.x it applies to whatever object the leader happens
to be assigned to. The content declares only the key and literal value; it cannot compute a
value, reference another trait's value, or apply a condition to a modifier.

## Corpus totals

| Property | Value |
|----------|-------|
| Total modifier entries | 98 |
| Distinct modifier keys | 50 |
| Traits with 1 modifier pair | 20 |
| Traits with 2 modifier pairs | 16 |
| Traits with 3 modifier pairs | 5 |
| Traits with 4 modifier pairs | 4 |
| Traits with 6 modifier pairs | 2 |
| Traits with no modifier block | 0 |

Distribution by count:

| Modifier count | Traits |
|----------------|--------|
| 1 | 20 |
| 2 | 16 |
| 3 | 5 |
| 4 | 4 |
| 6 | 2 |

The two six-modifier traits are `ui_trait_governor_questionable_ethics` and `ui_trait_governor_naturalist`, which are constructed as exact numerical inverses of one another:

| Key | `questionable_ethics` | `naturalist` |
|-----|----------------------|--------------|
| `planet_jobs_engineering_research_produces_mult` | `0.05` | `-0.05` |
| `planet_jobs_physics_research_produces_mult` | `0.05` | `-0.05` |
| `planet_jobs_society_research_produces_mult` | `0.05` | `-0.05` |
| `planet_stability_add` | `-2.5` | `2.5` |
| `pop_happiness` | `-0.05` | `0.05` |
| `logistic_growth_mult` | `-0.01` | `0.01` |

## Trade-off design pattern

Many traits pair a benefit with a liability rather than being purely positive. Representative examples, all verified from source:

| Trait | Benefit | Liability |
|-------|---------|-----------|
| `ui_trait_admiral_berserker` | `ship_weapon_damage = 0.15` | `ship_disengage_chance_mult = -0.25` |
| `ui_trait_admiral_glass_cannon` | `ship_weapon_damage = 0.20` | `ship_hull_mult = -0.20` |
| `ui_trait_admiral_sniper` | `ship_weapon_damage = 0.10`, `ship_weapon_range_mult = 0.10` | `ship_fire_rate_mult = -0.10`, `ship_speed_mult = -0.10` |
| `ui_trait_governor_deal_with_the_devil` | `planet_jobs_energy_produces_mult = 0.25` | `planet_crime_add = 25` |
| `ui_trait_governor_guns_legaliser` | `army_defense_damage_mult = 0.25`, `planet_army_build_speed_mult = 0.1` | `planet_stability_add = -5`, `planet_crime_add = 5` |
| `ui_trait_governor_vicious_rumours` | — | `planet_jobs_unity_produces_mult = -0.05` |
| `ui_trait_ruler_hardcore_bureaucrat` | — | `empire_size_add = 10` |
| `ui_trait_leader_politically_connected` | `leaders_cost_mult = -0.5` | `species_leader_exp_gain = -0.25` |

Opposed pairs are frequently built as exact sign inversions of the same key set:

| Pair | Keys | Direction |
|------|------|-----------|
| `ui_trait_governor_guns_legaliser` / `ui_trait_governor_guns_prohibitor` | `army_defense_damage_mult`, `planet_army_build_speed_mult`, `planet_stability_add`, `planet_crime_add` | all four signs inverted |
| `ui_trait_governor_ideologue_militarist` / `ui_trait_governor_ideologue_pacifist` | `pop_ethic_militarist_attraction_mult`, `pop_ethic_pacifist_attraction_mult` | both signs inverted |
| `ui_trait_governor_ideologue_xenophile` / `ui_trait_governor_ideologue_xenophobe` | `pop_ethic_xenophile_attraction_mult`, `pop_ethic_xenophobe_attraction_mult` | both signs inverted |
| `ui_trait_governor_ideologue_egalitarian` / `ui_trait_governor_ideologue_authoritarian` | `pop_ethic_egalitarian_attraction_mult`, `pop_ethic_authoritarian_attraction_mult` | both signs inverted |
| `ui_trait_governor_ideologue_materialist` / `ui_trait_governor_ideologue_spiritualist` | `pop_ethic_materialist_attraction_mult`, `pop_ethic_spiritualist_attraction_mult` | both signs inverted |
| `ui_trait_admiral_sniper` / `ui_trait_admiral_stormer` | `ship_weapon_damage`, `ship_weapon_range_mult`, `ship_fire_rate_mult`, `ship_speed_mult` | all four signs inverted |
| `ui_trait_admiral_glass_cannon` / `ui_trait_admiral_testudo` | `ship_weapon_damage`, `ship_hull_mult` | both signs inverted |
| `ui_trait_ruler_efficient_bureaucrat` / `ui_trait_ruler_hardcore_bureaucrat` | `empire_size_add` | sign inverted |

Four ideologue pairs aside, `ui_trait_admiral_berserker` / `ui_trait_admiral_guerillero` are the notable exception: they are exclusion-opposed yet **not** modifier-inverses. Berserker raises weapon damage and lowers disengage chance, while guerillero raises speed, fire rate, and disengage chance but lowers weapon range. They are alternative aggressive doctrines rather than mirror images.

## Value conventions

| Convention | Observation |
|------------|-------------|
| Multiplier keys | Suffixed `_mult`; values are fractions of 1, e.g. `0.15` = +15% |
| Additive keys | Suffixed `_add`; values are absolute, e.g. `planet_stability_add = 5`, `ship_sensor_range_add = 1`, `empire_size_add = -10` |
| Attraction keys | Unsuffixed `_attraction_mult`; fractions of 1 |
| Decimal style | Mixed two-decimal (`0.15`, `0.25`) and one-decimal (`0.1`, `0.4`, `-0.4`, `-0.05`) forms |
| Precision outlier | `army_damage_mult = 0.075` in `ui_trait_general_faith_militant` is the only three-decimal value |
| Sign | Always explicit for negatives; positives are unsigned |

## Effect locality

Modifier keys partition into three application scopes, and since 4.x this partition is stated
explicitly by the modifier block a trait uses:

| Scope | Keys | Block | Applies to |
|-------|------|-------|-----------|
| Ship / fleet | `ship_*`, `science_ship_survey_speed` | `fleet_modifier` | The leader's assigned fleet and its science vessels |
| Army | `army_*` | `army_modifier` | The armies the leader commands |
| Planet | `planet_*`, `pop_*` | `planet_modifier` | The colony the governor is assigned to |
| Country | `country_*`, `empire_size_add` | `councilor_modifier` | The empire while the leader sits on the council |
| Leader | `leaders_cost_mult`, `species_leader_exp_gain` | `self_modifier` | The leader itself |

Admiral traits use `fleet_modifier` with ship-scoped keys exclusively. The general trait uses
`army_modifier`. Governor traits use `planet_modifier` with planet- and pop-scoped keys. Ruler
traits use `councilor_modifier` with country-scoped keys, which is how 4.x models ruler effects,
because rulers are councilors rather than a leader class. The shared trait uses `self_modifier`. The
partition is therefore consistent and explicit.

## No conditional or scaling modifiers

No modifier value is conditional. The content cannot express "double this effect if the empire is militarist"; every value is a literal applied unconditionally while the trait is held. Conditional behaviour exists only in eligibility (whether the trait may be granted), never in the modifier itself.

## Related documents

- [Data model](./../data-model.md)
- [Behaviour: eligibility and exclusions](./eligibility-and-exclusions.md)
- [Component: trait catalogue](./../components/trait-catalogue.md)
- [Design decisions](./../design-decisions.md)
