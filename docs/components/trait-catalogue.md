# Trait catalogue

Complete reference of the 47 leader traits the mod adds. Modifiers are listed as declared in the trait definition; positive values are benefits and negative values are liabilities. Display names are the English localisation values from `ui-traits_l_english.yml`.

Legend: **Icon** — `shipped` = file in `gfx/interface/icons/traits/`, `vanilla` = base-game asset path, `—` = no `icon` field (engine default).

## Admiral traits (6)

### `ui_trait_admiral_berserker`

| Property | Value |
|----------|-------|
| Display name | Berserker |
| Icon | `shipped` — `ui_trait_berserker.dds` |
| Scope | `leader_trait = { admiral }`, `leader_class = { admiral }` |
| Modifiers | `ship_weapon_damage = 0.15`, `ship_disengage_chance_mult = -0.25` |
| Exclusions | `leader_trait_nervous`, `leader_trait_cautious`, `leader_trait_scout`, `ui_trait_admiral_guerillero` |
| Eligibility | none |
| Modification | field not declared |

### `ui_trait_admiral_guerillero`

| Property | Value |
|----------|-------|
| Display name | Guerillero |
| Icon | `shipped` — `ui_trait_guerillero.dds` |
| Scope | `{ admiral }` / `{ admiral }` |
| Modifiers | `ship_speed_mult = 0.10`, `ship_fire_rate_mult = 0.10`, `ship_weapon_range_mult = -0.10`, `ship_disengage_chance_mult = 0.25` |
| Exclusions | `leader_trait_nervous`, `leader_trait_cautious`, `leader_trait_scout`, `ui_trait_admiral_berserker` |
| Eligibility | none |
| Modification | field not declared |

### `ui_trait_admiral_glass_cannon`

| Property | Value |
|----------|-------|
| Display name | Glass Cannon |
| Icon | `shipped` — `ui_trait_glass_cannon.dds` |
| Scope | `{ admiral }` / `{ admiral }` |
| Modifiers | `ship_weapon_damage = 0.20`, `ship_hull_mult = -0.20` |
| Exclusions | `leader_trait_cautious`, `ui_trait_admiral_testudo` |
| Eligibility | none |
| Modification | field not declared |

### `ui_trait_admiral_sniper`

| Property | Value |
|----------|-------|
| Display name | Sniper |
| Icon | `shipped` — `ui_trait_sniper.dds` |
| Scope | `{ admiral }` / `{ admiral }` |
| Modifiers | `ship_weapon_damage = 0.10`, `ship_weapon_range_mult = 0.10`, `ship_fire_rate_mult = -0.10`, `ship_speed_mult = -0.10` |
| Exclusions | `ui_trait_admiral_stormer` |
| Eligibility | none |
| Modification | field not declared |

### `ui_trait_admiral_stormer`

| Property | Value |
|----------|-------|
| Display name | Stormer |
| Icon | `shipped` — `ui_trait_stormer.dds` |
| Scope | `{ admiral }` / `{ admiral }` |
| Modifiers | `ship_weapon_damage = -0.10`, `ship_weapon_range_mult = -0.10`, `ship_fire_rate_mult = 0.10`, `ship_speed_mult = 0.10` |
| Exclusions | `ui_trait_admiral_sniper` |
| Eligibility | none |
| Modification | field not declared |

### `ui_trait_admiral_testudo`

| Property | Value |
|----------|-------|
| Display name | Testudo |
| Icon | `shipped` — `ui_trait_testudo.dds` |
| Scope | `{ admiral }` / `{ admiral }` |
| Modifiers | `ship_weapon_damage = -0.20`, `ship_hull_mult = 0.20` |
| Exclusions | `ui_trait_admiral_glass_cannon` |
| Eligibility | none |
| Modification | field not declared |

The six admiral traits form three deliberate pairs of opposites: berserker/guerillero, sniper/stormer, and glass cannon/testudo. Berserker and guerillero additionally exclude each other and the same three vanilla traits.

## General trait (1)

### `ui_trait_general_crusader`

| Property | Value |
|----------|-------|
| Display name | Crusader |
| Icon | `shipped` — `ui_trait_crusader.dds` |
| Scope | `leader_trait = { general }`, `leader_class = { general }` |
| Modifiers | `army_damage_mult = 0.075`, `army_morale = 0.15` |
| Exclusions | none |
| Eligibility | `FROM = { OR = { has_ethic = "ethic_spiritualist" has_ethic = "ethic_fanatic_spiritualist" } }` |
| Modification | field not declared |

The only trait in the corpus whose eligibility requires the presence of an ethic rather than the absence of one, and the only general-class trait.

## Governor traits (34)

### `ui_trait_governor_engineer`

| Property | Value |
|----------|-------|
| Display name | Engineer |
| Icon | `vanilla` — `trait_natural_engineers.dds` |
| Modifiers | `planet_jobs_engineering_research_produces_mult = 0.30` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | excludes `leader_trait_intellectual`, `auth_machine_intelligence`, `ui_trait_governor_physicist`, `ui_trait_governor_sociologist` |

### `ui_trait_governor_physicist`

| Property | Value |
|----------|-------|
| Display name | Physicist |
| Icon | `vanilla` — `trait_natural_physicists.dds` |
| Modifiers | `planet_jobs_physics_research_produces_mult = 0.30` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | excludes `leader_trait_intellectual`, `auth_machine_intelligence`, `ui_trait_governor_engineer`, `ui_trait_governor_sociologist` |

### `ui_trait_governor_sociologist`

| Property | Value |
|----------|-------|
| Display name | Sociologist |
| Icon | `vanilla` — `trait_natural_sociologists.dds` |
| Modifiers | `planet_jobs_society_research_produces_mult = 0.30` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | excludes `leader_trait_intellectual`, `auth_machine_intelligence`, `ui_trait_governor_engineer`, `ui_trait_governor_physicist` |

The three research-specialist traits are mutually exclusive through eligibility conditions, not through `opposites`. Each excludes the other two and the vanilla `leader_trait_intellectual`, and all three reject machine-intelligence authorities. None of them declares a name/description pair problem except through the shared `ui_trait_governor_naturalist` exclusion.

### `ui_trait_governor_familist`

| Property | Value |
|----------|-------|
| Display name | Familist |
| Modifiers | `pop_growth_speed = 0.15` |
| Exclusions | `ui_trait_governor_war_industrialist` |
| Eligibility | excludes `auth_hive_mind` |

### `ui_trait_governor_corporatist`

| Property | Value |
|----------|-------|
| Display name | Corporatist |
| Modifiers | `planet_jobs_energy_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_environmentalist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist`, `ui_trait_governor_cultural_interest` |
| Eligibility | none |

### `ui_trait_governor_miner`

| Property | Value |
|----------|-------|
| Display name | Miner |
| Modifiers | `planet_jobs_minerals_produces_mult = 0.15` |
| Exclusions | identical list to `ui_trait_governor_corporatist` |
| Eligibility | none |

### `ui_trait_governor_populist`

| Property | Value |
|----------|-------|
| Display name | Populist |
| Modifiers | `planet_jobs_unity_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_robotics_magnate`

| Property | Value |
|----------|-------|
| Display name | Robotics Magnate |
| Modifiers | `pop_assembly_speed = 0.1`, `planet_pops_robotics_upkeep_mult = -0.05` |
| Exclusions | `ui_trait_governor_ideologue_spiritualist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist` |
| Eligibility | none |

### `ui_trait_governor_environmentalist`

| Property | Value |
|----------|-------|
| Display name | Environmentalist |
| Modifiers | `planet_pops_consumer_goods_upkeep_mult = -0.15` |
| Exclusions | `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist` |
| Eligibility | none |

### `ui_trait_governor_moral_authority`

| Property | Value |
|----------|-------|
| Display name | Moral Authority |
| Modifiers | `planet_jobs_unity_produces_mult = 0.05`, `planet_stability_add = 5`, `pop_happiness = 0.05` |
| Exclusions | `ui_trait_governor_ideologue_authoritarian`, `ui_trait_governor_vicious_rumours`, `ui_trait_governor_deal_with_the_devil` |
| Eligibility | excludes `ethic_fanatic_authoritarian`, `ethic_fanatic_xenophobe`, `ethic_xenophobe`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_militarist`

| Property | Value |
|----------|-------|
| Display name | Militaristic Obsession |
| Modifiers | `pop_ethic_militarist_attraction_mult = 0.25`, `pop_ethic_pacifist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_pacifist` |
| Eligibility | excludes `ethic_fanatic_pacifist`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_pacifist`

| Property | Value |
|----------|-------|
| Display name | Peacebringer |
| Modifiers | `pop_ethic_pacifist_attraction_mult = 0.25`, `pop_ethic_militarist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_militarist`, `ui_trait_governor_war_industrialist` |
| Eligibility | excludes `ethic_fanatic_militarist`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_xenophobe`

| Property | Value |
|----------|-------|
| Display name | Racial Cultist |
| Modifiers | `pop_ethic_xenophobe_attraction_mult = 0.25`, `pop_ethic_xenophile_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_open_armed`, `ui_trait_governor_ideologue_xenophile` |
| Eligibility | excludes `ethic_fanatic_xenophile`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_xenophile`

| Property | Value |
|----------|-------|
| Display name | Alien Assimilator |
| Modifiers | `pop_ethic_xenophile_attraction_mult = 0.25`, `pop_ethic_xenophobe_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_open_armed`, `ui_trait_governor_ideologue_xenophobe` |
| Eligibility | excludes `ethic_fanatic_xenophobe`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_egalitarian`

| Property | Value |
|----------|-------|
| Display name | Socialism Preacher |
| Modifiers | `pop_ethic_egalitarian_attraction_mult = 0.25`, `pop_ethic_authoritarian_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_moral_authority`, `ui_trait_governor_ideologue_authoritarian` |
| Eligibility | excludes `ethic_fanatic_authoritarian`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_authoritarian`

| Property | Value |
|----------|-------|
| Display name | Fascist Demagogue |
| Modifiers | `pop_ethic_authoritarian_attraction_mult = 0.25`, `pop_ethic_egalitarian_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_moral_authority`, `ui_trait_governor_ideologue_egalitarian` |
| Eligibility | excludes `ethic_fanatic_egalitarian`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_materialist`

| Property | Value |
|----------|-------|
| Display name | Nihilistic Crusader |
| Modifiers | `pop_ethic_materialist_attraction_mult = 0.25`, `pop_ethic_spiritualist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_spiritualist` |
| Eligibility | excludes `ethic_fanatic_spiritualist`, `auth_hive_mind` |

### `ui_trait_governor_ideologue_spiritualist`

| Property | Value |
|----------|-------|
| Display name | Spiritual Preacher |
| Modifiers | `pop_ethic_spiritualist_attraction_mult = 0.25`, `pop_ethic_materialist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_robotics_magnate`, `ui_trait_governor_ideologue_materialist` |
| Eligibility | excludes `ethic_fanatic_materialist`, `auth_hive_mind` |

Eight `ideologue_*` traits form four opposed pairs on the authoritarian/egalitarian, militarist/pacifist, materialist/spiritualist, and xenophobe/xenophile axes. Every one excludes hive-mind authorities and opposes the fanatic ethic of the other side.

### `ui_trait_governor_war_industrialist`

| Property | Value |
|----------|-------|
| Display name | War Industrialist |
| Modifiers | `planet_jobs_alloys_produces_mult = 0.1` |
| Exclusions | `ui_trait_governor_ideologue_pacifist`, `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_environmentalist`, `ui_trait_governor_consumer_industrialist`, `ui_trait_governor_familist`, `ui_trait_governor_robotics_magnate` |
| Eligibility | excludes `ethic_fanatic_pacifist` |

The largest exclusion list in the corpus. One of its entries (`ui_trait_governor_consumer_industrialist`) is declared without surrounding quotes; see [Open questions](./../ambiguities-and-open-questions.md).

### `ui_trait_governor_consumer_industrialist`

| Property | Value |
|----------|-------|
| Display name | Consumer Industrialist |
| Modifiers | `planet_jobs_consumer_goods_produces_mult = 0.1` |
| Exclusions | `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_environmentalist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_familist`, `ui_trait_governor_robotics_magnate` |
| Eligibility | none |

This trait has **no description key**. Its intended key was misspelled in the localisation file as `ui_trait_governor_consumer_idsustrialist_desc`.

### `ui_trait_governor_racist`

| Property | Value |
|----------|-------|
| Display name | Racist |
| Modifiers | `planet_immigration_pull_mult = -0.4` |
| Exclusions | `ui_trait_governor_ideologue_xenophile`, `ui_trait_governor_ideologue_pacifist`, `ui_trait_governor_open_armed` |
| Eligibility | none |

### `ui_trait_governor_open_armed`

| Property | Value |
|----------|-------|
| Display name | Open-armed |
| Modifiers | `planet_immigration_pull_mult = 0.4` |
| Exclusions | `ui_trait_governor_ideologue_xenophobe`, `ui_trait_governor_racist` |
| Eligibility | none |

### `ui_trait_governor_vicious_rumours`

| Property | Value |
|----------|-------|
| Display name | Vicious Rumours |
| Modifiers | `planet_jobs_unity_produces_mult = -0.05` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | none |

### `ui_trait_governor_deal_with_the_devil`

| Property | Value |
|----------|-------|
| Display name | Deal with the Devil |
| Modifiers | `planet_jobs_energy_produces_mult = 0.25`, `planet_crime_add = 25` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | none |

### `ui_trait_governor_questionable_ethics`

| Property | Value |
|----------|-------|
| Display name | Questionable Ethics |
| Modifiers | `planet_jobs_engineering_research_produces_mult = 0.05`, `planet_jobs_physics_research_produces_mult = 0.05`, `planet_jobs_society_research_produces_mult = 0.05`, `planet_stability_add = -2.5`, `pop_happiness = -0.05`, `pop_growth_speed = -0.01` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | excludes `auth_machine_intelligence`, `auth_hive_mind` |

### `ui_trait_governor_naturalist`

| Property | Value |
|----------|-------|
| Display name | Naturalist |
| Modifiers | `planet_jobs_engineering_research_produces_mult = -0.05`, `planet_jobs_physics_research_produces_mult = -0.05`, `planet_jobs_society_research_produces_mult = -0.05`, `planet_stability_add = 2.5`, `pop_happiness = 0.05`, `pop_growth_speed = 0.01` |
| Exclusions | `leader_trait_intellectual`, `leader_trait_governor_erudite`, `ui_trait_governor_engineer`, `ui_trait_governor_physicist`, `ui_trait_governor_sociologist`, `ui_trait_governor_questionable_ethics` |
| Eligibility | excludes `auth_machine_intelligence` |

The inverse of `ui_trait_governor_questionable_ethics`: research output falls while stability, happiness, and growth rise.

### `ui_trait_governor_guns_legaliser`

| Property | Value |
|----------|-------|
| Display name | Gun Legaliser |
| Modifiers | `army_defense_damage_mult = 0.25`, `planet_army_build_speed_mult = 0.1`, `planet_stability_add = -5`, `planet_crime_add = 5` |
| Exclusions | `ui_trait_governor_guns_prohibitor` |
| Eligibility | none |

### `ui_trait_governor_guns_prohibitor`

| Property | Value |
|----------|-------|
| Display name | Gun Prohibitor |
| Modifiers | `army_defense_damage_mult = -0.25`, `planet_army_build_speed_mult = -0.1`, `planet_stability_add = 5`, `planet_crime_add = -5` |
| Exclusions | `ui_trait_governor_guns_legaliser` |
| Eligibility | none |

### `ui_trait_governor_cultural_interest`

| Property | Value |
|----------|-------|
| Display name | Cultural Interest |
| Modifiers | `planet_amenities_mult = 0.10`, `planet_culture_workers_produces_mult = 0.10` |
| Exclusions | `leader_trait_architectural_interest`, `ui_trait_governor_corporatist`, `ui_trait_governor_miner` |
| Eligibility | none |

### `ui_trait_governor_fortifier`

| Property | Value |
|----------|-------|
| Display name | Fortifier |
| Modifiers | `planet_building_stronghold_build_speed_mult = 0.40`, `army_defense_damage_mult = 0.25` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_settler`

| Property | Value |
|----------|-------|
| Display name | Settler |
| Modifiers | `planet_district_city_build_speed_mult = 0.40`, `planet_colony_development_speed_mult = 0.25` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_chemist`

| Property | Value |
|----------|-------|
| Display name | Chemist |
| Modifiers | `planet_building_chemical_plant_build_speed_mult = 0.40`, `planet_chemists_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | none |

Defined with a double space before the `=` in the block header (`ui_trait_governor_chemist  = {`).

### `ui_trait_governor_metallurgist`

| Property | Value |
|----------|-------|
| Display name | Metallurgist |
| Modifiers | `planet_building_foundry_1_build_speed_mult = 0.40`, `planet_metallurgists_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | none |

Defined with a double space before the `=` in the block header.

### `ui_trait_governor_green_energy_advocate`

| Property | Value |
|----------|-------|
| Display name | Green Energy Advocate |
| Modifiers | `planet_district_generator_build_speed_mult = -0.33`, `planet_pops_consumer_goods_upkeep_mult = -0.10` |
| Exclusions | none |
| Eligibility | excludes `ethic_fanatic_materialist` |

## Ruler traits (5)

### `ui_trait_ruler_backroom_backstabber`

| Property | Value |
|----------|-------|
| Display name | Backroom Backstabber |
| Modifiers | `country_influence_produces_mult = 0.25`, `pop_government_ethic_attraction = 0.05` |
| Exclusions | none |
| Eligibility | excludes `auth_hive_mind` authority |

### `ui_trait_ruler_smoothtalking_charmer`

| Property | Value |
|----------|-------|
| Display name | Smooth-Talking Charmer |
| Modifiers | `country_trust_growth = 0.1` |
| Exclusions | none |
| Eligibility | excludes `auth_hive_mind` authority |

### `ui_trait_ruler_antique_collector`

| Property | Value |
|----------|-------|
| Display name | Antique Collector |
| Modifiers | `science_ship_survey_speed = 0.25`, `ship_anomaly_generation_chance_mult = 0.25`, `ship_sensor_range_add = 1` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_ruler_efficient_bureaucrat`

| Property | Value |
|----------|-------|
| Display name | Efficient Bureaucrat |
| Modifiers | `country_admin_cap_add = 10` |
| Exclusions | `ui_trait_ruler_hardcore_bureaucrat` |
| Eligibility | none |

### `ui_trait_ruler_hardcore_bureaucrat`

| Property | Value |
|----------|-------|
| Display name | Hardcore Bureaucrat |
| Modifiers | `country_admin_cap_add = -10` |
| Exclusions | `ui_trait_ruler_efficient_bureaucrat` |
| Eligibility | none |

The only trait whose complete effect is a negative modifier, paired as the explicit opposite of `ui_trait_ruler_efficient_bureaucrat`.

## Class-agnostic trait (1)

### `ui_trait_leader_politically_connected`

| Property | Value |
|----------|-------|
| Display name | Politically Connected |
| Icon | `shipped` — `ui_trait_politically_connected.dds` |
| Scope | `leader_trait = all`, `leader_class = { admiral scientist general governor }` |
| Modifiers | `leaders_cost_mult = -0.8`, `species_leader_exp_gain = -0.25` |
| Exclusions | `leader_trait_eager` |
| Eligibility | excludes `leader_class = ruler`; excludes `ethic_gestalt_consciousness` |
| Extra fields | `initial = yes`, `randomized = yes` |
| Modification | field not declared |

The only trait that reaches the admiral, scientist, general, and governor pools simultaneously, the only trait with `initial`/`randomized`, and the only trait that excludes the ruler class through a condition instead of its `leader_class` list. It carries an in-source TODO noting that meritocracy is not yet considered.

## Unused localisation

`ui_trait_governor_securist` and its description exist in the localisation file but have **no matching trait definition**. See [Open questions](./../ambiguities-and-open-questions.md).

## Related documents

- [Component: leader traits](./leader-traits.md) — statistics and file organisation
- [Component: localisation](./localisation.md)
- [Behaviour: eligibility and exclusions](./../behaviour/eligibility-and-exclusions.md)
- [Behaviour: modifiers and effects](./../behaviour/modifiers-and-effects.md)
