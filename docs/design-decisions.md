# Design decisions

Rationale reconstructed from repository evidence. Where a decision's reasoning is not evidenced, that is stated explicitly rather than inferred.

## Declarative content instead of any code

**Decision.** The mod ships only Clausewitz script, YAML localisation, and DDS assets. It contains no executable code, scripts, or tooling.

**Evidence.** No source file in any programming language exists; the entire content set is `.txt`, `.yml`, `.mod`, `.dds`, and `.png`.

**Rationale (evidenced).** Stellaris mods of this kind cannot execute code; the engine accepts only declarative content. The decision is imposed by the platform rather than chosen.

**Consequences.** Ownership is file-based and additive. No migration or compatibility logic can be expressed inside the mod. Security exposure is limited to content integrity. Verified by the absence of any code path in the repository.

## Identifiers prefixed `ui_trait_`

**Decision.** Every trait identifier carries the `ui_trait_` prefix, which vanilla content does not use.

**Evidence.** All 47 identifiers and all 96 localisation keys use the prefix; vanilla leader traits use `leader_trait_`.

**Rationale (evidenced).** The prefix namespaces the mod against vanilla content and against other mods, preventing accidental identifier collisions.

**Consequences.** The mod can reference vanilla identifiers safely by full name while its own identifiers remain unambiguous. The prefix also signals the mod family (`ui-*` refers to the Universum Infinitum collection) in a shared namespace.

## Files split by leader class

**Decision.** Trait definitions are split into a file per legacy leader class, plus one file for the class-agnostic trait.

**Evidence.** `ui-traits_leader.txt`, `_admiral.txt`, `_general.txt`, `_governor.txt`, `_ruler.txt`.

**Rationale (inferred).** File-per-class keeps a 47-trait corpus navigable and matches the class-scoped nature of most traits. The reasoning is not recorded in the repository.

**Consequences.** File placement is a maintenance convenience only; effective scope comes from the `leader_trait` and `leader_class` fields, so the two can drift. This is documented as an invariant to check.

## Two identical descriptor files

**Decision.** The descriptor is duplicated at the repository root and inside the payload, byte-identical.

**Evidence.** `ui-character-traits.mod` and `ui-character-traits/descriptor.mod` contain identical content.

**Rationale (inferred).** The two installation shapes the launcher supports — a root `.mod` file pointing at a payload directory, and a self-describing payload directory — each require a descriptor in a different location. Shipping both makes the same payload usable in either shape without modification.

**Consequences.** The duplication is a consistency hazard: the two files must be updated together, and nothing enforces that. Recorded as an invariant.

## English-only localisation

**Decision.** Only `localisation/english/` is supplied.

**Evidence.** No other language directory exists.

**Rationale (inferred).** The mod is developed in English and no translator contributions are evident in the repository history.

**Consequences.** Players using another game language see the mod's traits in English or as raw identifiers, depending on the engine's fallback. Adding a language requires a new directory and a matching `l_<language>:` block.

## Every trait costs the same

**Decision.** In the pre-4.x corpus all 47 traits declared `cost = 1`. That field has been
removed, because it does not exist in the 4.x leader trait schema.

**Evidence.** No trait block contains a `cost` field.

**Rationale (inferred).** A uniform cost lets the traits compete on effect and exclusion rather than on selection economy, and keeps the traits comparable to each other. The reasoning is not recorded.

**Consequences.** Mod traits may be cheaper or more expensive than functionally similar vanilla traits whose costs vary.

## Trade-off modifiers rather than pure benefits

**Decision.** Many traits pair a benefit with a liability, and opposed pairs use exact sign inversions of the same key set.

**Evidence.** Eight opposed pairs use mirrored modifier sets; for example `ui_trait_admiral_sniper` and `ui_trait_admiral_stormer` invert all four of the same keys, and `ui_trait_governor_questionable_ethics` and `ui_trait_governor_naturalist` invert all six.

**Rationale (evidenced by pattern).** The mirrored design makes opposing traits commensurable: choosing one is choosing its inverse, which makes the exclusion relationship meaningful rather than cosmetic.

**Consequences.** The design produces clear either/or decisions at the point a trait is offered.

## Two mechanisms for mutual exclusion

**Decision.** Some mutual exclusions use `opposites`; others use `leader_potential_add`.

**Evidence.** The three research specialists (`engineer`, `physicist`, `sociologist`) exclude each other through `leader_potential_add` conditions, and only declare `opposites = { "ui_trait_governor_naturalist" }`. Every other mutual exclusion uses `opposites`.

**Rationale (inferred).** The research specialists reuse the eligibility block to test for the vanilla `leader_trait_intellectual` at the same time, so expressing sibling exclusion in the same block avoids a second declaration. The reasoning is not recorded.

**Consequences.** Two mechanisms produce similar in-game results through different engine paths, which makes the exclusion graph harder to reason about statically. This is the single most confusing aspect of the content model and is documented in both [Eligibility and exclusions](./behaviour/eligibility-and-exclusions.md) and [Behaviour: trait scoping](./behaviour/trait-scoping.md).

## One class-agnostic trait

**Decision.** Exactly one trait, `ui_trait_leader_politically_connected`, sits in the `all` pool and reaches four leader classes.

**Evidence.** It is the only trait available to all three leader classes, the only one that
excludes the ruler through an `is_ruler = no` condition rather than a class list, and the only
one that uses a `self_modifier`.

**Rationale (inferred).** The trait's effect (`leaders_cost_mult = -0.8` with `species_leader_exp_gain = -0.25`) is conceptually leader-generic rather than class-specific, so it is offered wherever a leader can be recruited. Its eligibility block excludes rulers and gestalt consciousnesses to keep the design coherent.

**Consequences.** Because the pool is `all`, the ruler class cannot be excluded through `leader_class` alone, so a redundant eligibility guard is required. This coupling is fragile and recorded in [Behaviour: trait scoping](./behaviour/trait-scoping.md).

## Hive-mind exclusion as the default

**Decision.** Most governor traits and two ruler traits are unavailable to hive-mind empires.

**Evidence.** `auth_hive_mind` appears 13 times across eligibility blocks, more than any other single subject.

**Rationale (inferred).** Many of the traits model individualist social or economic behaviour — families, gun rights, immigration, ethics attraction — that does not map onto a gestalt consciousness. The reasoning is not recorded beyond the in-code TODO in `ui_trait_leader_politically_connected`.

**Consequences.** A contributor adding a governor trait must deliberately decide about hive-mind availability; the established precedent is exclusion.

## Three traits reuse vanilla icons rather than shipping new art

**Decision.** `ui_trait_governor_engineer`, `_physicist`, and `_sociologist` reference vanilla icon paths instead of shipping DDS files.

**Evidence.** Their `ICON` values point to `GFX_leader_trait_engineering_focus`, `GFX_leader_trait_physics_focus` and `GFX_leader_trait_society_focus`, which are vanilla sprites rather than textures shipped in this repository.

**Rationale (explicit, from the localisation text).** These traits are modelled directly on the vanilla `leader_trait_intellectual` family; their descriptions present them as renowned researchers of a specific field, mirroring the vanilla natural-engineers/physicists/sociologists traits. Reusing that art is therefore consistent.

**Consequences.** The traits depend on base-game assets existing in the supported version, which is a version-coupling risk.

## 37 icons committed but unreferenced

**Decision (or omission).** 37 of 45 shipped icons are not referenced by any trait definition.

**Evidence.** Only 8 shipped assets appear in `icon` fields.

**Rationale (inferred, uncertain).** The icons were authored for a design in which governor and ruler traits each had bespoke art. The trait definitions that would reference them either never declared `icon` or had their `icon` lines removed. The repository history does not record the reason.

**Consequences.** The payload carries roughly 37 dead assets. Their presence has no functional effect, but it obscures which art is in use and may mislead a contributor adding a trait into assuming an icon is already wired.

## No automated validation

**Decision.** The repository contains no build, test, or validation workflow. Its only workflows, `.github/workflows/github-release.yml` and `.github/workflows/steam-workshop-release.yml`, package the tagged content and publish it to GitHub Releases and Steam Workshop; they validate nothing.

**Evidence.** No build manifest, no test directory, and no validation workflow exist. `.github/workflows/` contains only `github-release.yml` and `steam-workshop-release.yml`.

**Rationale (inferred).** The content set is small enough to review by hand, and the mod predates the addition of the `.github/` directory, which originally contained only funding and cover assets.

**Consequences.** Two missing description keys, one orphaned localisation pair, and seven asymmetric exclusions exist undetected. This is the repository's largest maintenance risk. See [Testing](./testing.md).

## Documentation decisions

**Decision.** Root policy documents (`README.md`, `ARCHITECTURE.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `PRIVACY.md`) were added in 2026, after the mod's 2020-2021 development.

**Evidence.** Git history dates the policy-document commits to 2026-11-17 while the mod content dates to 2020-2021.

**Rationale (inferred).** Repository standardisation rather than a change in the mod's scope.

**Consequences.** Root documents describe a stable, essentially frozen content set. This `docs/` tree complements them with content-level detail rather than repeating them.

## Related documents

- [Architecture](./architecture.md)
- [Behaviour: modifiers and effects](./behaviour/modifiers-and-effects.md)
- [Behaviour: eligibility and exclusions](./behaviour/eligibility-and-exclusions.md)
- [Open questions](./ambiguities-and-open-questions.md)
