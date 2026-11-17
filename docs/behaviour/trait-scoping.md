# Behaviour: trait scoping

## What scope means

A trait's scope determines which leader trait pool the engine adds it to and which leader classes it can be offered to. Two fields express this, and they are independent:

- `leader_trait` — the pool the trait belongs to.
- `leader_class` — the classes the trait may appear for.

The engine evaluates both. A trait whose pool and class list disagree is a defect: the pool controls where the trait is considered, and the class list controls who may receive it.

## Observed scope matrix

| `leader_trait` | `leader_class` | Traits |
|----------------|----------------|--------|
| `all` | `{ admiral scientist general governor }` | 1 |
| `{ admiral }` | `{ admiral }` | 6 |
| `{ general }` | `{ general }` | 1 |
| `{ governor }` | `{ governor }` | 34 |
| `{ ruler }` | `{ ruler }` | 5 |

In every case the pool value and the class list agree. File placement also matches, except that `ui-traits_leader.txt` holds the `all`-pool trait rather than a class-suffixed file.

## The `all` pool trait

`ui_trait_leader_politically_connected` is the sole trait using `leader_trait = all`. Its class list is `{ admiral scientist general governor }`, which omits `ruler`. Because the pool is `all`, the engine would otherwise consider it for rulers; the trait therefore adds an eligibility guard:

```text
leader_potential_add = {
    NOT = {
        leader_class = ruler
    }
    NOT = {
        FROM = {
            has_ethic = "ethic_gestalt_consciousness"
        }
    }
}
```

Two mechanisms therefore constrain the same trait: the class list excludes `scientist`-adjacent classes it does not list, and the eligibility block excludes the ruler class it cannot express through the list because the pool is `all`. A future contributor changing this trait must keep both in agreement; dropping the condition would let rulers receive a trait whose intent is to exclude them, and the source carries an in-code comment noting that meritocracy gating is still missing (`# TODO: Also meritocracy`).

## Class-agnostic versus multi-class

The corpus contains no second multi-class trait. Any new multi-class trait should reuse the `all`-pool pattern plus an explicit class condition rather than listing classes it wants to reach, because `leader_class` is treated as a whitelist within the pool the trait is declared in.

## Effect of scope on eligibility evaluation

The `from`/`FROM` context available inside `leader_potential_add` differs by scope:

| Scope | Country context available | Evidence |
|-------|---------------------------|----------|
| Governor | Yes — `from = { ... }` used to test authorities and leader traits, and `FROM = { ... }` used to test country ethics | 20 governor traits |
| Ruler | Yes — `from = { has_authority = "auth_hive_mind" }` | 2 ruler traits |
| General | Yes — `FROM = { has_ethic = ... }` | 1 general trait |
| Admiral | Not used — no admiral trait declares eligibility | 0 of 6 |
| Class-agnostic | Yes — `FROM = { has_ethic = ... }` | 1 trait |

Both `from` and `FROM` appear in the corpus, sometimes within the same trait family (for example the three research traits use lowercase `from`, while `ui_trait_governor_moral_authority` uses uppercase `FROM`). Whether the engine treats them identically for these condition types is not verifiable from content alone; see [Open questions](./../ambiguities-and-open-questions.md).

## Related documents

- [Data model](./../data-model.md)
- [Eligibility and exclusions](./eligibility-and-exclusions.md)
- [Component: leader traits](./../components/leader-traits.md)
- [Invariants](./../invariants.md)
