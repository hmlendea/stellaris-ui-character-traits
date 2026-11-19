# Trait catalogue

Complete reference of the 47 leader traits the mod adds, updated for the Stellaris 4.5
(Cygnus) leader system. Modifiers are listed as declared in the trait definition;
positive values are benefits and negative values are liabilities. Display names are the
English localisation values from `ui-traits_l_english.yml`.

Scope uses the post-4.x leader model: the legacy `admiral`, `general`, `governor` and
`ruler` classes no longer exist. Fleet commanders are `commander` leaders with the
`subclass_commander_admiral` subclass, army commanders use `subclass_commander_general`,
governors use `subclass_official_governor`, and rulers and other council members are
councilors.

## Admiral traits (6)

### `ui_trait_admiral_berserker`

| Property | Value |
|----------|-------|
| Display name | Berserker |
| Icon | `GFX_ui_trait_berserker` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_weapon_damage = 0.15`, `ship_disengage_chance_mult = -0.25` |
| Exclusions | `leader_trait_nervous`, `leader_trait_cautious`, `leader_trait_scout`, `ui_trait_admiral_guerillero` |
| Eligibility | admiral subclass (or no Paragons DLC) |

### `ui_trait_admiral_guerillero`

| Property | Value |
|----------|-------|
| Display name | Guerillero |
| Icon | `GFX_ui_trait_guerillero` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_speed_mult = 0.10`, `ship_fire_rate_mult = 0.10`, `ship_weapon_range_mult = -0.10`, `ship_disengage_chance_mult = 0.25` |
| Exclusions | `leader_trait_nervous`, `leader_trait_cautious`, `leader_trait_scout`, `ui_trait_admiral_berserker` |
| Eligibility | admiral subclass (or no Paragons DLC) |

### `ui_trait_admiral_glass_cannon`

| Property | Value |
|----------|-------|
| Display name | Glass Cannon |
| Icon | `GFX_ui_trait_glass_cannon` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_weapon_damage = 0.20`, `ship_hull_mult = -0.20` |
| Exclusions | `leader_trait_cautious`, `ui_trait_admiral_testudo` |
| Eligibility | admiral subclass (or no Paragons DLC) |

### `ui_trait_admiral_sniper`

| Property | Value |
|----------|-------|
| Display name | Sniper |
| Icon | `GFX_ui_trait_sniper` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_weapon_damage = 0.10`, `ship_weapon_range_mult = 0.10`, `ship_fire_rate_mult = -0.10`, `ship_speed_mult = -0.10` |
| Exclusions | `ui_trait_admiral_stormer` |
| Eligibility | admiral subclass (or no Paragons DLC) |

### `ui_trait_admiral_stormer`

| Property | Value |
|----------|-------|
| Display name | Stormer |
| Icon | `GFX_ui_trait_stormer` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_weapon_damage = -0.10`, `ship_weapon_range_mult = -0.10`, `ship_fire_rate_mult = 0.10`, `ship_speed_mult = 0.10` |
| Exclusions | `ui_trait_admiral_sniper` |
| Eligibility | admiral subclass (or no Paragons DLC) |

### `ui_trait_admiral_testudo`

| Property | Value |
|----------|-------|
| Display name | Testudo |
| Icon | `GFX_ui_trait_testudo` |
| Class | `commander` |
| Modifiers (fleet_modifier) | `ship_weapon_damage = -0.20`, `ship_hull_mult = 0.20` |
| Exclusions | `ui_trait_admiral_glass_cannon` |
| Eligibility | admiral subclass (or no Paragons DLC) |

## General trait (1)

### `ui_trait_general_faith_militant`

| Property | Value |
|----------|-------|
| Display name | Militant Faith |
| Icon | `GFX_ui_trait_crusader` |
| Class | `commander` |
| Modifiers (army_modifier) | `army_damage_mult = 0.075`, `army_morale = 0.15` |
| Exclusions | `leader_trait_crusader`, `leader_trait_crusader_2` |
| Eligibility | general subclass (or no Paragons DLC); ethics: ethic_fanatic_spiritualist, ethic_spiritualist |

## Governor traits (34)

### `ui_trait_governor_engineer`

| Property | Value |
|----------|-------|
| Display name | Engineer |
| Icon | `GFX_leader_trait_engineering_focus` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_engineering_research_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | authorities: auth_machine_intelligence |

### `ui_trait_governor_physicist`

| Property | Value |
|----------|-------|
| Display name | Physicist |
| Icon | `GFX_leader_trait_physics_focus` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_physics_research_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | authorities: auth_machine_intelligence |

### `ui_trait_governor_sociologist`

| Property | Value |
|----------|-------|
| Display name | Sociologist |
| Icon | `GFX_leader_trait_society_focus` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_society_research_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_naturalist` |
| Eligibility | authorities: auth_machine_intelligence |

### `ui_trait_governor_familist`

| Property | Value |
|----------|-------|
| Display name | Familist |
| Icon | `GFX_ui_trait_governor_familist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `logistic_growth_mult = 0.15` |
| Exclusions | `ui_trait_governor_war_industrialist` |
| Eligibility | authorities: auth_hive_mind |

### `ui_trait_governor_corporatist`

| Property | Value |
|----------|-------|
| Display name | Corporatist |
| Icon | `GFX_ui_trait_governor_corporatist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_energy_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_environmentalist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist`, `ui_trait_governor_cultural_interest` |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_miner`

| Property | Value |
|----------|-------|
| Display name | Miner |
| Icon | `GFX_ui_trait_governor_miner` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_minerals_produces_mult = 0.15` |
| Exclusions | `ui_trait_governor_environmentalist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist`, `ui_trait_governor_cultural_interest` |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_populist`

| Property | Value |
|----------|-------|
| Display name | Populist |
| Icon | `GFX_ui_trait_governor_populist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_unity_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_robotics_magnate`

| Property | Value |
|----------|-------|
| Display name | Robotics Magnate |
| Icon | `GFX_ui_trait_governor_robotics_magnate` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_pop_assembly_mult = 0.1`, `planet_pops_robotics_upkeep_mult = -0.05` |
| Exclusions | `ui_trait_governor_ideologue_spiritualist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist` |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_environmentalist`

| Property | Value |
|----------|-------|
| Display name | Environmentalist |
| Icon | `GFX_ui_trait_governor_environmentalist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_pops_consumer_goods_upkeep_mult = -0.10` |
| Exclusions | `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist` |
| Eligibility | none |

### `ui_trait_governor_moral_authority`

| Property | Value |
|----------|-------|
| Display name | Moral Authority |
| Icon | `GFX_ui_trait_governor_moral_authority` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_unity_produces_mult = 0.05`, `planet_stability_add = 5`, `pop_happiness = 0.05` |
| Exclusions | `ui_trait_governor_ideologue_authoritarian`, `ui_trait_governor_vicious_rumours`, `ui_trait_governor_deal_with_the_devil` |
| Eligibility | ethics: ethic_fanatic_authoritarian, ethic_fanatic_xenophobe, ethic_xenophobe; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_militarist`

| Property | Value |
|----------|-------|
| Display name | Militaristic Obsession |
| Icon | `GFX_ui_trait_governor_ideologue_militarist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_militarist_attraction_mult = 0.25`, `pop_ethic_pacifist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_pacifist` |
| Eligibility | ethics: ethic_fanatic_pacifist; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_pacifist`

| Property | Value |
|----------|-------|
| Display name | Peacebringer |
| Icon | `GFX_ui_trait_governor_ideologue_pacifist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_pacifist_attraction_mult = 0.25`, `pop_ethic_militarist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_militarist`, `ui_trait_governor_war_industrialist` |
| Eligibility | ethics: ethic_fanatic_militarist; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_xenophobe`

| Property | Value |
|----------|-------|
| Display name | Racial Cultist |
| Icon | `GFX_ui_trait_governor_ideologue_xenophobe` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_xenophobe_attraction_mult = 0.25`, `pop_ethic_xenophile_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_open_armed`, `ui_trait_governor_ideologue_xenophile` |
| Eligibility | ethics: ethic_fanatic_xenophile; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_xenophile`

| Property | Value |
|----------|-------|
| Display name | Alien Assimilator |
| Icon | `GFX_ui_trait_governor_ideologue_xenophile` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_xenophile_attraction_mult = 0.25`, `pop_ethic_xenophobe_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_open_armed`, `ui_trait_governor_ideologue_xenophobe` |
| Eligibility | ethics: ethic_fanatic_xenophobe; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_egalitarian`

| Property | Value |
|----------|-------|
| Display name | Socialism Preacher |
| Icon | `GFX_ui_trait_governor_ideologue_egalitarian` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_egalitarian_attraction_mult = 0.25`, `pop_ethic_authoritarian_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_moral_authority`, `ui_trait_governor_ideologue_authoritarian` |
| Eligibility | ethics: ethic_fanatic_authoritarian; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_authoritarian`

| Property | Value |
|----------|-------|
| Display name | Fascist Demagogue |
| Icon | `GFX_ui_trait_governor_ideologue_authoritarian` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_authoritarian_attraction_mult = 0.25`, `pop_ethic_egalitarian_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_moral_authority`, `ui_trait_governor_ideologue_egalitarian` |
| Eligibility | ethics: ethic_fanatic_egalitarian; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_materialist`

| Property | Value |
|----------|-------|
| Display name | Nihilistic Crusader |
| Icon | `GFX_ui_trait_governor_ideologue_materialist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_materialist_attraction_mult = 0.25`, `pop_ethic_spiritualist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_ideologue_spiritualist` |
| Eligibility | ethics: ethic_fanatic_spiritualist; authorities: auth_hive_mind |

### `ui_trait_governor_ideologue_spiritualist`

| Property | Value |
|----------|-------|
| Display name | Spiritual Preacher |
| Icon | `GFX_ui_trait_governor_ideologue_spiritualist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_spiritualist_attraction_mult = 0.25`, `pop_ethic_materialist_attraction_mult = -0.25` |
| Exclusions | `ui_trait_governor_robotics_magnate`, `ui_trait_governor_ideologue_materialist` |
| Eligibility | ethics: ethic_fanatic_materialist; authorities: auth_hive_mind |

### `ui_trait_governor_war_industrialist`

| Property | Value |
|----------|-------|
| Display name | War Industrialist |
| Icon | `GFX_ui_trait_governor_war_industrialist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_alloys_produces_mult = 0.10` |
| Exclusions | `ui_trait_governor_ideologue_pacifist`, `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_environmentalist`, `ui_trait_governor_consumer_industrialist`, `ui_trait_governor_familist`, `ui_trait_governor_robotics_magnate` |
| Eligibility | ethics: ethic_fanatic_pacifist |

### `ui_trait_governor_consumer_industrialist`

| Property | Value |
|----------|-------|
| Display name | Consumer Industrialist |
| Icon | `GFX_ui_trait_governor_consumer_industrialist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_consumer_goods_produces_mult = 0.10` |
| Exclusions | `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_environmentalist`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_familist`, `ui_trait_governor_robotics_magnate` |
| Eligibility | none |

### `ui_trait_governor_racist`

| Property | Value |
|----------|-------|
| Display name | Racist |
| Icon | `GFX_ui_trait_governor_racist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_xenophile_attraction_mult = -0.4`, `pop_ethic_xenophobe_attraction_mult = 0.1` |
| Exclusions | `ui_trait_governor_ideologue_xenophile`, `ui_trait_governor_ideologue_pacifist`, `ui_trait_governor_open_armed` |
| Eligibility | none |

### `ui_trait_governor_open_armed`

| Property | Value |
|----------|-------|
| Display name | Open-armed |
| Icon | `GFX_ui_trait_governor_open_armed` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `pop_ethic_xenophile_attraction_mult = 0.4`, `pop_ethic_xenophobe_attraction_mult = -0.1` |
| Exclusions | `ui_trait_governor_ideologue_xenophobe`, `ui_trait_governor_racist` |
| Eligibility | none |

### `ui_trait_governor_vicious_rumours`

| Property | Value |
|----------|-------|
| Display name | Vicious Rumours |
| Icon | `GFX_ui_trait_governor_vicious_rumours` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_unity_produces_mult = -0.05` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | none |

### `ui_trait_governor_deal_with_the_devil`

| Property | Value |
|----------|-------|
| Display name | Deal with the Devil |
| Icon | `GFX_ui_trait_governor_deal_with_the_devil` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_energy_produces_mult = 0.25`, `planet_crime_add = 25` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | none |

### `ui_trait_governor_questionable_ethics`

| Property | Value |
|----------|-------|
| Display name | Questionable Ethics |
| Icon | `GFX_ui_trait_governor_questionable_ethics` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_engineering_research_produces_mult = 0.075`, `planet_jobs_physics_research_produces_mult = 0.075`, `planet_jobs_society_research_produces_mult = 0.075`, `planet_stability_add = -2.5`, `pop_happiness = -0.05`, `logistic_growth_mult = -0.01` |
| Exclusions | `leader_trait_righteous`, `ui_trait_governor_moral_authority` |
| Eligibility | authorities: auth_hive_mind, auth_machine_intelligence |

### `ui_trait_governor_naturalist`

| Property | Value |
|----------|-------|
| Display name | Naturalist |
| Icon | `GFX_ui_trait_governor_naturalist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_jobs_engineering_research_produces_mult = -0.05`, `planet_jobs_physics_research_produces_mult = -0.05`, `planet_jobs_society_research_produces_mult = -0.05`, `planet_stability_add = 2.5`, `pop_happiness = 0.05`, `logistic_growth_mult = 0.01` |
| Exclusions | `leader_trait_intellectual`, `ui_trait_governor_engineer`, `ui_trait_governor_physicist`, `ui_trait_governor_sociologist`, `ui_trait_governor_questionable_ethics` |
| Eligibility | authorities: auth_machine_intelligence |

### `ui_trait_governor_guns_legaliser`

| Property | Value |
|----------|-------|
| Display name | Gun Legaliser |
| Icon | `GFX_ui_trait_governor_guns_legaliser` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `army_defense_damage_mult = 0.25`, `planet_army_build_speed_mult = 0.1`, `planet_stability_add = -5`, `planet_crime_add = 5` |
| Exclusions | `ui_trait_governor_guns_prohibitor` |
| Eligibility | none |

### `ui_trait_governor_guns_prohibitor`

| Property | Value |
|----------|-------|
| Display name | Gun Prohibitor |
| Icon | `GFX_ui_trait_governor_guns_prohibitor` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `army_defense_damage_mult = -0.25`, `planet_army_build_speed_mult = -0.1`, `planet_stability_add = 5`, `planet_crime_add = -5` |
| Exclusions | `ui_trait_governor_guns_legaliser` |
| Eligibility | none |

### `ui_trait_governor_cultural_interest`

| Property | Value |
|----------|-------|
| Display name | Cultural Interest |
| Icon | `GFX_ui_trait_governor_cultural_interest` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_amenities_mult = 0.10`, `planet_jobs_unity_produces_mult = 0.10` |
| Exclusions | `ui_trait_governor_corporatist`, `ui_trait_governor_miner`, `ui_trait_governor_war_industrialist`, `ui_trait_governor_consumer_industrialist` |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_fortifier`

| Property | Value |
|----------|-------|
| Display name | Fortifier |
| Icon | `GFX_ui_trait_governor_fortifier` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_building_stronghold_build_speed_mult = 0.40`, `army_defense_damage_mult = 0.25` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_settler`

| Property | Value |
|----------|-------|
| Display name | Settler |
| Icon | `GFX_ui_trait_governor_settler` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_district_city_build_speed_mult = 0.40`, `logistic_growth_mult = 0.25` |
| Exclusions | none |
| Eligibility | no vanilla governor focus |

### `ui_trait_governor_chemist`

| Property | Value |
|----------|-------|
| Display name | Chemist |
| Icon | `GFX_ui_trait_governor_chemist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_building_build_speed_mult = 0.25`, `planet_chemists_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_metallurgist`

| Property | Value |
|----------|-------|
| Display name | Metallurgist |
| Icon | `GFX_ui_trait_governor_metallurgist` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_building_build_speed_mult = 0.25`, `planet_metallurgists_produces_mult = 0.15` |
| Exclusions | none |
| Eligibility | none |

### `ui_trait_governor_green_energy_advocate`

| Property | Value |
|----------|-------|
| Display name | Green Energy Advocate |
| Icon | `GFX_ui_trait_governor_green_energy_advocate` |
| Class | `official commander scientist` |
| Modifiers (planet_modifier) | `planet_district_generator_build_speed_mult = -0.33`, `planet_pops_consumer_goods_upkeep_mult = -0.10` |
| Exclusions | none |
| Eligibility | ethics: ethic_fanatic_materialist |

## Ruler traits (5)

### `ui_trait_ruler_backroom_backstabber`

| Property | Value |
|----------|-------|
| Display name | Backroom Backstabber |
| Icon | `GFX_ui_trait_ruler_backroom_backstabber` |
| Class | `commander scientist official` |
| Modifiers (councilor_modifier) | `country_influence_produces_mult = 0.25`, `pop_government_ethic_attraction = 0.05` |
| Exclusions | none |
| Eligibility | ruler or councilor subclass; authorities: auth_hive_mind |

### `ui_trait_ruler_smoothtalking_charmer`

| Property | Value |
|----------|-------|
| Display name | Smooth-Talking Charmer |
| Icon | `GFX_ui_trait_ruler_smoothtalking_charmer` |
| Class | `commander scientist official` |
| Modifiers (councilor_modifier) | `country_trust_growth = 0.1` |
| Exclusions | none |
| Eligibility | ruler or councilor subclass; authorities: auth_hive_mind |

### `ui_trait_ruler_antique_collector`

| Property | Value |
|----------|-------|
| Display name | Antique Collector |
| Icon | `GFX_ui_trait_ruler_antique_collector` |
| Class | `commander scientist official` |
| Modifiers (councilor_modifier) | `science_ship_survey_speed = 0.25`, `ship_anomaly_generation_chance_mult = 0.25`, `ship_sensor_range_add = 1` |
| Exclusions | none |
| Eligibility | ruler or councilor subclass |

### `ui_trait_ruler_efficient_bureaucrat`

| Property | Value |
|----------|-------|
| Display name | Efficient Bureaucrat |
| Icon | `GFX_ui_trait_ruler_efficient_bureaucrat` |
| Class | `commander scientist official` |
| Modifiers (councilor_modifier) | `empire_size_add = -10` |
| Exclusions | `ui_trait_ruler_hardcore_bureaucrat` |
| Eligibility | ruler or councilor subclass |

### `ui_trait_ruler_hardcore_bureaucrat`

| Property | Value |
|----------|-------|
| Display name | Hardcore Bureaucrat |
| Icon | `GFX_ui_trait_ruler_hardcore_bureaucrat` |
| Class | `commander scientist official` |
| Modifiers (councilor_modifier) | `empire_size_add = 10` |
| Exclusions | `ui_trait_ruler_efficient_bureaucrat` |
| Eligibility | ruler or councilor subclass |

## Shared leader trait (1)

### `ui_trait_leader_politically_connected`

| Property | Value |
|----------|-------|
| Display name | Politically Connected |
| Icon | `GFX_ui_trait_politically_connected` |
| Class | `commander scientist official` |
| Modifiers (self_modifier) | `leaders_cost_mult = -0.5`, `species_leader_exp_gain = -0.25` |
| Exclusions | `leader_trait_eager` |
| Eligibility | not the ruler; excludes `ethic_gestalt_consciousness` |

## Cross-cutting structure

- **Six admiral traits** form three deliberate pairs of opposites: berserker/guerillero,
  sniper/stormer, and glass cannon/testudo. Berserker and guerillero additionally exclude
  each other and three vanilla traits (`leader_trait_nervous`, `leader_trait_cautious`,
  `leader_trait_scout`).
- **One general trait** (`ui_trait_general_faith_militant`, displayed as *Militant Faith*)
  is the only trait whose eligibility requires the presence of an ethic rather than its
  absence, and the only army-scoped trait. It intentionally does not reuse the vanilla
  `leader_trait_crusader` identifier, which in 4.x is a Galactic Paragons event trait.
- **Three research-specialist governor traits** (`engineer`, `physicist`, `sociologist`)
  are mutually exclusive through eligibility conditions, not through `opposites`. Each
  excludes the other two and vanilla `leader_trait_intellectual`, and all three reject
  machine-intelligence authorities. They are the only traits gated on `has_paragon_dlc = no`,
  because in 4.x the equivalent role is filled by the vanilla scientist focus traits.
- **Eight `ideologue_*` traits** form four opposed pairs on the authoritarian/egalitarian,
  militarist/pacifist, materialist/spiritualist, and xenophobe/xenophile axes. Every one
  excludes hive-mind authorities and opposes the fanatic ethic of the other side.
- **Four governor traits** (`corporatist`, `miner`, `populist`, `robotics_magnate`) and
  two more (`cultural_interest`, `settler`) require the leader to have no vanilla governor
  focus, so they never compete with the base game's focus traits for the same slot.
- **Five ruler traits** use a `councilor_modifier`, so their effects apply while the leader
  sits on the council (including as the empire ruler). Without Galactic Paragons they are
  available to any leader; with it they are reserved for the ruler or a councilor subclass.
- **One shared trait** (`ui_trait_leader_politically_connected`) applies to any commander,
  scientist or official that is not the current ruler, and opposes vanilla `leader_trait_eager`.

## Related documents

- [Leader traits component](./leader-traits.md)
- [Icons component](./icons.md)
- [Localisation component](./localisation.md)
- [Eligibility and exclusions](../behaviour/eligibility-and-exclusions.md)
- [Modifiers and effects](../behaviour/modifiers-and-effects.md)
