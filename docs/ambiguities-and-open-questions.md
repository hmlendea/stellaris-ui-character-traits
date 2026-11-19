# Ambiguities and open questions

Unresolved items, verified defects, and documentation discrepancies. Each entry states the question or defect, the evidence, why it remains unresolved, and what would resolve it.

## Verified content defects

### 1. Whether the orphaned `securist` localisation and icon are intentional

**Evidence.** `ui_trait_governor_securist` and `ui_trait_governor_securist_desc` exist in the
localisation file. No trait definition uses the identifier `ui_trait_governor_securist`. A
matching icon file, `ui_trait_governor_securist.dds`, exists in the icon directory but is
likewise unreferenced.

**Open question.** Was the trait definition removed and the localisation and icon left behind,
or was the trait never defined despite its text and art being prepared?

**Impact.** The keys and icon are inert.

**Resolution.** Either add the missing trait definition or remove the key pair and the icon.

### 2. Nine one-directional exclusion edges

**Evidence.** Nine exclusion edges are declared in only one direction:

| Declaring trait | Target | Target's own list |
|-----------------|--------|-------------------|
| `ui_trait_governor_ideologue_xenophile` | `ui_trait_governor_open_armed` | absent |
| `ui_trait_governor_ideologue_egalitarian` | `ui_trait_governor_moral_authority` | absent |
| `ui_trait_governor_consumer_industrialist` | `ui_trait_governor_familist` | absent |
| `ui_trait_governor_racist` | `ui_trait_governor_ideologue_xenophile` | absent |
| `ui_trait_governor_racist` | `ui_trait_governor_ideologue_pacifist` | absent |
| `ui_trait_governor_questionable_ethics` | `ui_trait_governor_moral_authority` | absent |
| `ui_trait_governor_naturalist` | `ui_trait_governor_questionable_ethics` | absent |

**Open question.** Does the engine treat `opposites` as symmetric or directional?

**Impact.** If directional, the number of exclusions actually enforced is smaller than the corpus suggests, and some traits intended to be exclusive can coexist.

**Resolution.** Determine the engine's semantics, then either add the reverse edges or document the one-directional intent.

### 3. Both `from` and `FROM` used in eligibility blocks

**Evidence.** The three research specialists use lowercase `from` (`from = { has_authority = ... }`, `from = { has_trait = ... }`), while `ui_trait_governor_moral_authority`, the ideologue traits, `ui_trait_general_faith_militant`, and `ui_trait_leader_politically_connected` use uppercase `FROM`. The two forms appear in the same file and, in the class-agnostic trait, within the same block.

**Open question.** Does the engine treat `from` and `FROM` identically for these condition subjects, or do they resolve to different scopes?

**Impact.** If they differ, some eligibility blocks may be testing the wrong country context.

**Resolution.** Consult the target game version's scripting reference, or observe the traits in game to confirm the intended gating occurs.

### 4. Whether the removed `cost = 1` field leaves balance parity intact

**Evidence.** The pre-4.x corpus declared `cost = 1` on all 47 traits. The 4.5 leader trait
schema no longer has a `cost` field; only ruler-creation traits declare one. The field was
therefore removed with no replacement.

**Open question.** Whether the mod should compensate for the loss of an explicit cost signal
through `selectable_weight`, and whether the current weights achieve the intended rarity.

**Impact.** Weighting is now the only lever on how often a trait is offered. If the weights
differ from the pre-4.x cost intent, relative rarity changes.

**Resolution.** Review the `selectable_weight` values against observed offer rates in game.

### 5. Whether the one unreferenced icon is intentional

**Evidence.** 45 DDS files ship; 44 are referenced by sprites declared in
`interface/ui_character_traits.gfx`, and 3 vanilla sprites are referenced instead of shipped
art. One shipped icon, `ui_trait_governor_securist.dds`, has no sprite and no trait.

**Open question.** Whether the icon was authored for a trait that was never defined, or is
speculative.

**Impact.** One inert asset. No behavioural effect.

**Resolution.** Either define the `securist` trait or remove the icon and its localisation pair.

## Documentation consistency

The documentation was reconciled with the content during the Stellaris 4.5 update:

- Trait scope, modifier scoping, exclusion counts, icon coverage and localisation coverage are
  stated identically in `README.md`, `ARCHITECTURE.md` and `docs/`.
- The former discrepancies recorded here (trait-scope counts, `modification` counts,
  `opposites`/`leader_potential_add` counts, icon-reference counts, and orphaned localisation
  counts) no longer exist; the documents were rewritten from the current content.
- Item 6 below is a non-contradiction retained for clarity, and item 7 records a verified claim.

### 6. README compatibility statement versus descriptor version

**Evidence.** `README.md` states the mod is OS-agnostic and actively tested on Linux. The
descriptor declares `supported_version="v4.5.*"`. The README's compatibility section addresses
operating systems, while the descriptor addresses game version.

**Status.** No contradiction.

### 7. `ARCHITECTURE.md` deployment table versioning claim

**Evidence.** `ARCHITECTURE.md` lists release tags `v1.0`, `v1.0.1`, and `v1.0.2` and notes
that release tags and the declared supported game version evolve independently. Three published
releases exist with those tags.

**Status.** Verified consistent.

## Unverifiable from the repository

| Item | Why it cannot be verified here |
|------|-------------------------------|
| Whether the 8 referenced vanilla trait identifiers and 3 vanilla sprites exist in game version 4.5.x | Requires a Stellaris installation |
| Whether `from` and `FROM` are equivalent | Requires engine documentation or in-game observation |
| Whether `opposites` is symmetric | Requires engine documentation or in-game observation |
| Whether all 47 traits in fact appear in game | Requires a Stellaris installation |
| Whether any save has ever referenced a removed trait | Requires save data |
| Whether the single unreferenced icon (`ui_trait_governor_securist.dds`) is intentional | Requires maintainer statement or repository history that is not present |

## Related documents

- [Error handling](./error-handling.md)
- [Invariants](./invariants.md)
- [Testing](./testing.md)
- [Component: icons](./components/icons.md)
- [Component: localisation](./components/localisation.md)
- [Behaviour: eligibility and exclusions](./behaviour/eligibility-and-exclusions.md)
