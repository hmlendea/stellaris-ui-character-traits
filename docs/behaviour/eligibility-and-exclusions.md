# Behaviour: eligibility and exclusions

Two independent mechanisms govern whether a leader can receive a trait. Both are declared in content and both are evaluated by the engine.

| Mechanism | Field | Effect |
|-----------|-------|--------|
| Eligibility | `leader_potential_add` | Gates whether the trait may be offered at all for a given leader and country |
| Exclusion | `opposites` | Removes traits that conflict with one another from the same offer |
| Construction gate | `modification` | Blocks adding or removing the trait through genetic or robotic modification |
| Generation gates | `initial`, `randomized` | Permit assignment at leader creation and during randomised assignment |

Understanding the distinction matters: a mutual pair expressed through `opposites` prevents coexistence, while the same intent expressed through `leader_potential_add` prevents the second trait from ever being offered. The two produce similar in-game results through different engine paths, and the corpus mixes them.

## Eligibility: 21 declarations

### By condition subject

| Subject tested | Distinct subjects | Traits relying on it |
|----------------|-------------------|----------------------|
| Leader class | `ruler` | 1 |
| Country authority | `auth_hive_mind`, `auth_machine_intelligence` | 20 |
| Country ethic | authoritarian, egalitarian, militarist, pacifist, materialist, spiritualist, xenophile, xenophobe (normal and fanatic forms), plus `ethic_gestalt_consciousness` | 13 |
| Existing leader trait | `leader_trait_intellectual`, and the mod's own research traits | 3 |

### Hive-mind exclusion dominance

`auth_hive_mind` is the most-tested single subject in the corpus: 13 references. It appears in every governor `ideologue_*` trait, in `ui_trait_governor_familist`, `ui_trait_governor_moral_authority`, `ui_trait_governor_questionable_ethics`, and in the two ruler traits that gate on `from = { has_authority = "auth_hive_mind" }`.

The pattern establishes that a large part of the corpus is unavailable to hive-mind empires. A contributor adding a governor trait should decide deliberately whether hive minds should receive it; the established precedent is exclusion.

### Machine-intelligence exclusion

`auth_machine_intelligence` is tested five times: in the three research-specialist traits, in `ui_trait_governor_questionable_ethics`, and in `ui_trait_governor_naturalist`. Its use is narrower than hive-mind exclusion and clusters around traits whose theme conflicts with machine empires (biological research, moral qualms).

### Ethic gating

Two shapes of ethic condition appear:

1. **Absence gating** — the trait is withdrawn when a specific ethic is present. `ui_trait_governor_ideologue_militarist` uses `NOT = { OR = { FROM = { has_ethic = "ethic_fanatic_pacifist" } ... } }`. This is the dominant pattern: each ideologue trait withdraws for the fanatic form of its opposite.
2. **Presence gating** — the trait requires an ethic to be present. Exactly one trait does this: `ui_trait_general_crusader` requires `ethic_spiritualist` or `ethic_fanatic_spiritualist`.

| Trait | Ethic requirement |
|-------|-------------------|
| `ui_trait_general_crusader` | requires spiritualist or fanatic spiritualist |
| `ui_trait_governor_moral_authority` | rejects fanatic authoritarian, fanatic xenophobe, xenophobe |
| `ui_trait_governor_ideologue_militarist` | rejects fanatic pacifist |
| `ui_trait_governor_ideologue_pacifist` | rejects fanatic militarist |
| `ui_trait_governor_ideologue_xenophobe` | rejects fanatic xenophile |
| `ui_trait_governor_ideologue_xenophile` | rejects fanatic xenophobe |
| `ui_trait_governor_ideologue_egalitarian` | rejects fanatic authoritarian |
| `ui_trait_governor_ideologue_authoritarian` | rejects fanatic egalitarian |
| `ui_trait_governor_ideologue_materialist` | rejects fanatic spiritualist |
| `ui_trait_governor_ideologue_spiritualist` | rejects fanatic materialist |
| `ui_trait_governor_war_industrialist` | rejects fanatic pacifist |
| `ui_trait_governor_green_energy_advocate` | rejects fanatic materialist |
| `ui_trait_leader_politically_connected` | rejects `ethic_gestalt_consciousness` |

Notice that the ideologue traits reject the **fanatic** form of the opposing ethic rather than the normal form. A normal-form opposing ethic does not withdraw the trait. This is a deliberate asymmetry: fanatic adherents are excluded, moderate ones are not.

### Existing-trait gating

The three research-specialist traits test for an existing leader trait:

```text
leader_potential_add = {
    NOT = {
        from = {
            OR = {
                has_trait = "leader_trait_intellectual"
                has_authority = "auth_machine_intelligence"
                has_trait = "ui_trait_governor_physicist"
                has_trait = "ui_trait_governor_sociologist"
            }
        }
    }
}
```

Each specialist rejects the vanilla `leader_trait_intellectual`, machine intelligence, and the two sibling specialists. This makes the three traits mutually exclusive **without** any `opposites` entry between them; each only declares `opposites = { "ui_trait_governor_naturalist" }`.

## Exclusions: 37 declarations

### Composition

| Reference type | Distinct targets | Occurrences |
|----------------|------------------|-------------|
| Mod traits (`ui_trait_*`) | 27 distinct | 86 |
| Vanilla traits (`leader_trait_*`) | 8 distinct | 14 |

The 8 vanilla targets, by frequency:

| Vanilla identifier | Referenced by |
|--------------------|---------------|
| `leader_trait_righteous` | `ui_trait_governor_vicious_rumours`, `ui_trait_governor_deal_with_the_devil`, `ui_trait_governor_questionable_ethics` |
| `leader_trait_cautious` | `ui_trait_admiral_berserker`, `ui_trait_admiral_guerillero`, `ui_trait_admiral_glass_cannon` |
| `leader_trait_scout` | `ui_trait_admiral_berserker`, `ui_trait_admiral_guerillero` |
| `leader_trait_nervous` | `ui_trait_admiral_berserker`, `ui_trait_admiral_guerillero` |
| `leader_trait_intellectual` | `ui_trait_governor_naturalist` |
| `leader_trait_governor_erudite` | `ui_trait_governor_naturalist` |
| `leader_trait_eager` | `ui_trait_leader_politically_connected` |
| `leader_trait_architectural_interest` | `ui_trait_governor_cultural_interest` |

### Integrity of the exclusion graph

| Check | Result |
|-------|--------|
| Unresolved `ui_trait_*` targets (identifier not defined) | none |
| Self-references | none |
| Duplicate entries within a single list | none |
| Vanilla targets (not defined in this repository) | 14 references to 8 identifiers — resolvable only against the base game |

Every mod-identifier target therefore resolves inside the repository. The vanilla targets cannot be validated here and are the primary compatibility risk described in [Compatibility](./../compatibility.md).

### Asymmetric exclusions

Seven exclusion edges are declared in one direction only. Their in-game effect depends on whether the engine treats `opposites` as symmetric or directional; this is not determinable from content. The edges are:

| Declaring trait | Target | Target's own list |
|-----------------|--------|-------------------|
| `ui_trait_governor_ideologue_xenophile` | `ui_trait_governor_open_armed` | does not include `ideologue_xenophile` (it lists `ideologue_xenophobe`, `racist`) |
| `ui_trait_governor_ideologue_egalitarian` | `ui_trait_governor_moral_authority` | does not include `ideologue_egalitarian` |
| `ui_trait_governor_consumer_industrialist` | `ui_trait_governor_familist` | does not include `consumer_industrialist` |
| `ui_trait_governor_racist` | `ui_trait_governor_ideologue_xenophile` | does not include `racist` |
| `ui_trait_governor_racist` | `ui_trait_governor_ideologue_pacifist` | does not include `racist` |
| `ui_trait_governor_questionable_ethics` | `ui_trait_governor_moral_authority` | does not include `questionable_ethics` |
| `ui_trait_governor_naturalist` | `ui_trait_governor_questionable_ethics` | does not include `naturalist` |

The `naturalist` / `questionable_ethics` pair is the clearest example. The two traits are thematic inverses — one trades research output for stability and growth, the other the reverse — and `ui_trait_governor_naturalist` names `ui_trait_governor_questionable_ethics` in its exclusion list. The reverse declaration is absent: `ui_trait_governor_questionable_ethics` lists only `leader_trait_righteous` and `ui_trait_governor_moral_authority`. If the engine treats `opposites` as directional, the pair is one-way in effect; if symmetric, the two are already mutually exclusive. The same question applies to the other six edges. This cannot be resolved from content alone and is recorded in [Open questions](./../ambiguities-and-open-questions.md).

### Fully-covered and uncovered areas

| Area | Traits | With `opposites` | Without |
|------|--------|------------------|---------|
| Admiral | 6 | 6 | 0 |
| General | 1 | 0 | 1 |
| Governor | 34 | 28 | 6 |
| Ruler | 5 | 2 | 3 |
| Class-agnostic | 1 | 1 | 0 |

The 10 traits without any exclusion are: `ui_trait_general_crusader`, `ui_trait_governor_chemist`, `ui_trait_governor_fortifier`, `ui_trait_governor_green_energy_advocate`, `ui_trait_governor_metallurgist`, `ui_trait_governor_populist`, `ui_trait_governor_settler`, `ui_trait_ruler_antique_collector`, `ui_trait_ruler_backroom_backstabber`, `ui_trait_ruler_smoothtalking_charmer`. Each is thematically non-conflicting with the rest of the corpus, so the absence is consistent rather than an omission.

## Modification and generation gates

| Field | Value | Count | Meaning |
|-------|-------|-------|---------|
| `modification` | `no` | 39 | Trait cannot be added or removed through genetic/robotic modification. Declared by the 34 governor traits and the 5 ruler traits. |
| `initial` | `yes` | 1 | `ui_trait_leader_politically_connected` may be assigned at leader generation |
| `randomized` | `yes` | 1 | `ui_trait_leader_politically_connected` may be drawn during randomised assignment |

Counting precisely: 34 governor + 5 ruler = 39, which exactly accounts for every `modification = no` in the corpus. The general trait and the class-agnostic trait do **not** declare the field, and no admiral trait does.

## Related documents

- [Behaviour: trait scoping](./trait-scoping.md)
- [Behaviour: modifiers and effects](./modifiers-and-effects.md)
- [Flow: leader trait acquisition](./../flows/leader-trait-acquisition.md)
- [Invariants](./../invariants.md)
