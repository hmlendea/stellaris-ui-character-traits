# Component: localisation

## Purpose

`ui-character-traits/localisation/english/ui-traits_l_english.yml` supplies the English display name and description for every trait the mod adds. The engine binds these strings to trait identifiers at load time and renders them in the leader trait interface and tooltips.

## File characteristics

| Property | Value |
|----------|-------|
| Path | `ui-character-traits/localisation/english/ui-traits_l_english.yml` |
| Lines | 107 |
| Encoding | UTF-8 **with byte-order mark** (required) |
| Line endings | LF |
| Root block | `l_english:` |
| Entries | 96 (48 name keys + 48 description keys) |
| Comment headings | 5 |
| Blank lines | 4 |

## Structure

```yaml
l_english:

# Leader traits
 ui_trait_leader_politically_connected_desc:0 "..."
 ui_trait_leader_politically_connected:0 "Politically Connected"

# Admiral traits
 ui_trait_admiral_berserker_desc:0 "..."
 ui_trait_admiral_berserker:0 "Berserker"
...
```

| Element | Convention |
|---------|-----------|
| Entry indentation | Exactly one leading space |
| Version marker | `:0` after the key, before the quoted value |
| Quoting | Double quotes around every value |
| Description key | `<trait identifier>_desc` |
| Name key | `<trait identifier>` verbatim |
| Ordering | Description entry immediately precedes its name entry |
| Grouping | A comment heading precedes each leader-class group |

## In-string formatting

| Sequence | Meaning | Observed count |
|----------|---------|----------------|
| `§!` | Closes a vanilla Stellaris colour/style block opened elsewhere by the engine | 46 of 48 descriptions |
| `\n` | Line break | 48 of 48 descriptions |

`ui_trait_general_crusader_desc` and `ui_trait_ruler_hardcore_bureaucrat_desc` are the two descriptions that do not contain `§!`. The trailing `\n` on every description is a stylistic convention for spacing the tooltip body.

## Key coverage

| Category | Count |
|----------|-------|
| Trait definitions | 47 |
| Name keys present | 48 |
| Description keys present | 48 |
| Definitions with a matching name key | 47 of 47 |
| Definitions with a matching description key | 45 of 47 |
| Keys with no matching definition | 1 name key (`ui_trait_governor_securist`) |
| Description keys with no matching definition | 2 (caused by misspelling) |

### The three pairing defects

| Key | Problem |
|-----|---------|
| `ui_trait_governor_securist`, `ui_trait_governor_securist_desc` | Orphaned. No trait definition uses this identifier. Corresponding `ui_trait_governor_securist.dds` exists in the icon directory. |
| `ui_trait_governor_consumer_idsustrialist_desc` | Misspelled. The trait identifier is `ui_trait_governor_consumer_industrialist`, so the description key never binds and the trait shows no description. |
| `ui_trait_governor_war_idsustrialist_desc` | Misspelled in the same way. The trait identifier is `ui_trait_governor_war_industrialist`. |

Note that the **name keys** for both industrialist traits are spelled correctly (`ui_trait_governor_consumer_industrialist`, `ui_trait_governor_war_industrialist`); only the `_desc` keys are malformed. As a result both traits display a name but no description.

## Display names

| Identifier | Display name |
|------------|--------------|
| `ui_trait_leader_politically_connected` | Politically Connected |
| `ui_trait_admiral_berserker` | Berserker |
| `ui_trait_admiral_guerillero` | Guerillero |
| `ui_trait_admiral_glass_cannon` | Glass Cannon |
| `ui_trait_admiral_sniper` | Sniper |
| `ui_trait_admiral_stormer` | Stormer |
| `ui_trait_admiral_testudo` | Testudo |
| `ui_trait_general_crusader` | Crusader |
| `ui_trait_governor_chemist` | Chemist |
| `ui_trait_governor_consumer_industrialist` | Consumer Industrialist |
| `ui_trait_governor_corporatist` | Corporatist |
| `ui_trait_governor_cultural_interest` | Cultural Interest |
| `ui_trait_governor_deal_with_the_devil` | Deal with the Devil |
| `ui_trait_governor_engineer` | Engineer |
| `ui_trait_governor_environmentalist` | Environmentalist |
| `ui_trait_governor_familist` | Familist |
| `ui_trait_governor_fortifier` | Fortifier |
| `ui_trait_governor_green_energy_advocate` | Green Energy Advocate |
| `ui_trait_governor_guns_legaliser` | Gun Legaliser |
| `ui_trait_governor_guns_prohibitor` | Gun Prohibitor |
| `ui_trait_governor_ideologue_authoritarian` | Fascist Demagogue |
| `ui_trait_governor_ideologue_egalitarian` | Socialism Preacher |
| `ui_trait_governor_ideologue_materialist` | Nihilistic Crusader |
| `ui_trait_governor_ideologue_militarist` | Militaristic Obsession |
| `ui_trait_governor_ideologue_pacifist` | Peacebringer |
| `ui_trait_governor_ideologue_spiritualist` | Spiritual Preacher |
| `ui_trait_governor_ideologue_xenophile` | Alien Assimilator |
| `ui_trait_governor_ideologue_xenophobe` | Racial Cultist |
| `ui_trait_governor_metallurgist` | Metallurgist |
| `ui_trait_governor_miner` | Miner |
| `ui_trait_governor_moral_authority` | Moral Authority |
| `ui_trait_governor_naturalist` | Naturalist |
| `ui_trait_governor_open_armed` | Open-armed |
| `ui_trait_governor_physicist` | Physicist |
| `ui_trait_governor_populist` | Populist |
| `ui_trait_governor_questionable_ethics` | Questionable Ethics |
| `ui_trait_governor_racist` | Racist |
| `ui_trait_governor_robotics_magnate` | Robotics Magnate |
| `ui_trait_governor_securist` | Securist |
| `ui_trait_governor_settler` | Settler |
| `ui_trait_governor_sociologist` | Sociologist |
| `ui_trait_governor_vicious_rumours` | Vicious Rumours |
| `ui_trait_governor_war_industrialist` | War Industrialist |
| `ui_trait_ruler_antique_collector` | Antique Collector |
| `ui_trait_ruler_backroom_backstabber` | Backroom Backstabber |
| `ui_trait_ruler_efficient_bureaucrat` | Efficient Bureaucrat |
| `ui_trait_ruler_hardcore_bureaucrat` | Hardcore Bureaucrat |
| `ui_trait_ruler_smoothtalking_charmer` | Smooth-Talking Charmer |

## Text-quality defects in description values

The description strings contain several typographical errors unrelated to key binding. These affect only displayed text, not behaviour: `"sheild wall"` in `ui_trait_admiral_testudo_desc`, `"idustry"` and `"idsustrialist"` in the industrialist descriptions, `"enginner"` in `ui_trait_governor_engineer_desc`, `"pyhsics"` in `ui_trait_governor_physicist_desc`, `"authocracy"` in `ui_trait_governor_ideologue_authoritarian_desc`, and `"stauch"` in several descriptions. See [Open questions](./../ambiguities-and-open-questions.md).

## Language coverage

Only `localisation/english/` exists. Adding another language requires a new directory named `localisation/<language>/` containing a file using the corresponding `<prefix>_l_<language>.yml` convention and languages header.

## Related documents

- [Data model](./../data-model.md)
- [Component: leader traits](./leader-traits.md)
- [Change guide](./../change-guide.md)
- [Troubleshooting](./../troubleshooting.md)
