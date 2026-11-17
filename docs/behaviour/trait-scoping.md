# Behaviour: trait scoping

## What scope means in 4.x

A leader trait is offered only when three things agree: the leader's **class**
(`commander`, `official`, `scientist`), the leader's **subclass** when Galactic Paragons is
installed, and the **eligibility conditions** in `leader_potential_add`. The old pre-4.x model,
in which a trait declared a pool (`leader_trait`) and a class list and the engine intersected
them, no longer exists.

The mod therefore expresses scope through two fields:

- `leader_class` — the classes the trait may appear for.
- `leader_potential_add` — conditions, including subclass tests such as
  `has_trait = subclass_commander_admiral`.

## Observed scope matrix

| `leader_class` | Subclass restriction | Traits |
|----------------|----------------------|--------|
| `{ commander }` | `subclass_commander_admiral` (or no Paragons) | 6 |
| `{ commander }` | `subclass_commander_general` (or no Paragons) | 1 |
| `{ official commander scientist }` | none | 34 |
| `{ commander scientist official }` | ruler or councilor subclass | 5 |
| `{ commander scientist official }` | not the ruler | 1 |

File placement matches the old class grouping for maintainability, but is not authoritative:
scope comes from the fields inside each block.

## Why `official commander scientist` for governor traits

In 4.x any leader class with `can_govern_planet = yes` can govern a colony, so a governor
trait that named only `official` would silently exclude the `commander_governor` and
`scientist_governor` subclasses the base game provides. Listing all three classes keeps the
traits available to every governor, which matches their pre-4.x behaviour when `governor` was
a class of its own.

## Admiral and general subclass gating

Fleet and army commanders are both `commander` leaders in 4.x; they are distinguished only by
subclass. The six admiral traits and the one general trait therefore use the vanilla pattern:

```text
leader_class = { commander }
leader_potential_add = {
    trait_is_crisis_faction_check = no
    OR = {
        has_paragon_dlc = no
        has_trait = subclass_commander_admiral
    }
}
```

The `has_paragon_dlc = no` leg keeps the traits attainable when the DLC is absent, because
without it no `commander` would carry a subclass and the traits would be unreachable. The
base game uses the same shape for its own subclass-gated traits.

## The class-agnostic trait

`ui_trait_leader_politically_connected` is the only trait available to all three classes and
the only one that excludes rulers:

```text
leader_class = { commander scientist official }
leader_potential_add = {
    trait_is_crisis_faction_check = no
    is_ruler = no
    NOT = {
        from = {
            has_ethic = "ethic_gestalt_consciousness"
        }
    }
}
```

`is_ruler` replaces the pre-4.x `NOT = { leader_class = ruler }` guard, because `ruler` is no
longer a class. The source retains its in-code note that meritocracy gating is still missing
(`# TODO: Also meritocracy`).

## Ruler traits as councilor traits

`ruler` is not a class in 4.x. Rulers are councilors, so the five ruler traits model their
effects with `councilor_modifier` — which the engine applies while the leader is on the
council, including when that leader is the empire ruler — and gate availability with:

```text
OR = {
    is_ruler = yes
    has_council_subclass = yes
    has_paragon_dlc = no
}
```

This mirrors how the base game models its own ruler-flavoured traits such as
`trait_ruler_deep_connections`, which are `councilor_modifier` traits gated on a councilor
subclass when Paragons is present.

## Effect of scope on eligibility evaluation

| Scope | Country context available inside `leader_potential_add` | Evidence |
|-------|--------------------------------------------------------|----------|
| Governor | Yes — `from = { ... }` tests authorities and leader traits; `FROM = { ... }` tests country ethics | 34 traits |
| Ruler | Yes — `from = { has_authority = "auth_hive_mind" }` | 2 traits |
| General | Yes — `FROM = { has_ethic = ... }` | 1 trait |
| Admiral | Only subclass gating; no country condition | 6 traits |
| Class-agnostic | Yes — `from = { has_ethic = ... }` | 1 trait |

`from` and `FROM` both appear in the corpus, sometimes within the same family: the research
traits use lowercase `from` while `ui_trait_governor_moral_authority` uses uppercase `FROM`.
The engine treats the casing as equivalent for these conditions, but the inconsistency is
recorded in [Open questions](./../ambiguities-and-open-questions.md) as a cleanup item rather
than a defect.

## Related documents

- [Data model](./../data-model.md)
- [Eligibility and exclusions](./eligibility-and-exclusions.md)
- [Component: leader traits](./../components/leader-traits.md)
- [Invariants](./../invariants.md)
