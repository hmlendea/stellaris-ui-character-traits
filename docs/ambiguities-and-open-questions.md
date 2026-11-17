# Ambiguities and open questions

Unresolved items, verified defects, and documentation discrepancies. Each entry states the question or defect, the evidence, why it remains unresolved, and what would resolve it.

## Verified content defects

### 1. Two traits have no description

**Evidence.** `ui_trait_governor_consumer_industrialist` and `ui_trait_governor_war_industrialist` exist as trait definitions. Their description keys in `ui-traits_l_english.yml` are misspelled as `ui_trait_governor_consumer_idsustrialist_desc` (line 28) and `ui_trait_governor_war_idsustrialist_desc` (line 94). The name keys are spelled correctly, so the traits display a name but no description.

**Impact.** Two of 47 traits show an empty description in game.

**Resolution.** Rename the two keys to remove the extra `ds`.

### 2. One orphaned localisation pair

**Evidence.** `ui_trait_governor_securist` and `ui_trait_governor_securist_desc` exist in the localisation file (lines 86-87). No trait definition uses the identifier `ui_trait_governor_securist`. A matching icon file, `ui_trait_governor_securist.dds`, exists in the icon directory.

**Open question.** Was the trait definition removed and the localisation and icon left behind, or was the trait never defined despite its text and art being prepared?

**Impact.** The keys are inert; the icon is unused.

**Resolution.** Either add the missing trait definition or remove the key pair and the icon.

### 3. Unquoted exclusion list member

**Evidence.** Line 410 of `ui-traits_leader_governor.txt` contains, inside `ui_trait_governor_war_industrialist`'s `opposites` list:

```text
opposites = { "ui_trait_governor_ideologue_pacifist" "ui_trait_governor_corporatist" "ui_trait_governor_miner" "ui_trait_governor_environmentalist" ui_trait_governor_consumer_industrialist "ui_trait_governor_familist" "ui_trait_governor_robotics_magnate" }
```

The fourth-from-last member lacks surrounding quotes while all seven others have them.

**Open question.** Does the engine's parser accept an unquoted identifier in an `opposites` list?

**Impact.** If rejected, the unquoted member may be dropped or the block may fail to parse, removing the exclusion between `ui_trait_governor_war_industrialist` and `ui_trait_governor_consumer_industrialist`.

**Resolution.** Quote the member to match the other seven. This is safe regardless of parser behaviour.

### 4. Seven one-directional exclusion edges

**Evidence.** Seven exclusion edges are declared in only one direction:

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

### 5. Both `from` and `FROM` used in eligibility blocks

**Evidence.** The three research specialists use lowercase `from` (`from = { has_authority = ... }`, `from = { has_trait = ... }`), while `ui_trait_governor_moral_authority`, the ideologue traits, `ui_trait_general_crusader`, and `ui_trait_leader_politically_connected` use uppercase `FROM`. The two forms appear in the same file and, in the class-agnostic trait, within the same block.

**Open question.** Does the engine treat `from` and `FROM` identically for these condition subjects, or do they resolve to different scopes?

**Impact.** If they differ, some eligibility blocks may be testing the wrong country context.

**Resolution.** Consult the target game version's scripting reference, or observe the traits in game to confirm the intended gating occurs.

### 6. Whether `cost = 1` is deliberate parity with vanilla

**Evidence.** All 47 traits declare `cost = 1`. Vanilla leader trait costs vary.

**Open question.** Was uniformity chosen for balance reasons, as a placeholder pending balance work, or because the field is populated by a default?

**Impact.** None functional; the question matters only for future balance work.

**Resolution.** Repository history or maintainer statement. Not determinable from content.

### 7. Whether the 37 unreferenced icons are intentional

**Evidence.** 45 DDS files ship; 8 are referenced by traits that declare an `icon`. 37 are unused.

**Open question.** Were the icons authored for a design in which each trait declares its own art, and the `icon` lines were never added? Or were the files committed speculatively?

**Impact.** Payload bloat and potential contributor confusion. The icons do not affect behaviour.

**Resolution.** Maintainer statement. The icon set is otherwise fully consistent with the trait themes, which suggests intent rather than accident.

## Documentation discrepancies

### 8. `ARCHITECTURE.md` trait-scope counts

**Evidence.** `ARCHITECTURE.md` states that the trait scope counts are 34 governor, 6 admiral, 5 ruler, and 1 general, and that one trait declares the scope `{ admiral scientist general governor }` while excluding the ruler class through its eligibility condition. Direct content analysis confirms these figures: 34 governor-scoped, 6 admiral-scoped, 5 ruler-scoped, 1 general-scoped, plus 1 class-agnostic trait whose `leader_class` list is `{ admiral scientist general governor }`.

**Status.** Verified consistent. No discrepancy.

### 9. `ARCHITECTURE.md` claims about modification

**Evidence.** `ARCHITECTURE.md` states that 39 definitions set `modification = no`. Direct analysis confirms 39: 34 governor traits plus 5 ruler traits.

**Status.** Verified consistent. No discrepancy.

### 10. `ARCHITECTURE.md` claims about `opposites` and `leader_potential_add`

**Evidence.** `ARCHITECTURE.md` states 37 definitions declare `opposites` and 21 declare `leader_potential_add`. Direct analysis confirms 37 and 21 respectively.

**Status.** Verified consistent. No discrepancy.

### 11. `ARCHITECTURE.md` claims about icon references

**Evidence.** `ARCHITECTURE.md` states that 11 definitions declare an `icon` and that 34 of 45 shipped icons are unreferenced. Direct analysis confirms 11 `icon` declarations. Of those 11, three reference vanilla paths not shipped in the repository, so shipped icons referenced by mod traits number 8 and unreferenced shipped icons number **37**, not 34.

**Discrepancy.** The unreferenced shipped icon count is 37, not 34. The root document appears to have counted the three vanilla references as shipped icons.

**Resolution.** Correct the count in `ARCHITECTURE.md` centrally, or accept this document's figure as the verified one.

### 12. `ARCHITECTURE.md` claims about icon and localisation coverage gaps

**Evidence.** `ARCHITECTURE.md` states there are 3 localisation entries without matching trait definitions, 2 traits missing a description key, and 3 governor traits that reuse vanilla icons. Direct analysis confirms the 2 missing description keys and the 3 vanilla icon references. For orphaned entries, the verified figures are **1 orphaned name key** (`ui_trait_governor_securist`) and **3 orphaned description keys** (`ui_trait_governor_securist_desc`, `ui_trait_governor_consumer_idsustrialist_desc`, `ui_trait_governor_war_idsustrialist_desc`), totalling 4 orphaned entries.

**Discrepancy.** The figure of 3 matches the orphaned **description** key count but not the total orphaned entry count, which is 4.

**Resolution.** Clarify the counting basis in `ARCHITECTURE.md`, or treat this document's itemised list as authoritative.

### 13. `ARCHITECTURE.md` claim about traits omitting both fields

**Evidence.** `ARCHITECTURE.md` states: "Eight traits omit both `opposites` and `modification`, and five of those additionally declare `initial = yes` or `randomized = yes` in `ui-traits_leader.txt`."

Direct analysis finds:

| Measure | Verified value |
|---------|----------------|
| Traits omitting **both** `opposites` and `modification` | **1** — `ui_trait_general_crusader` |
| Traits declaring `initial` or `randomized` | **1** — `ui_trait_leader_politically_connected` |
| Traits omitting `opposites` | 10 |
| Traits omitting `modification` | 8 (the 6 admirals, the general trait, and the class-agnostic trait) |

The class-agnostic trait **does** declare `opposites` (`leader_trait_eager`) and **does not** declare `modification`, so it does not qualify as omitting both.

**Discrepancy.** Both figures in the root document are unsupported by the content. The verified values are 1 and 1 respectively.

**Resolution.** Correct the claim in `ARCHITECTURE.md`.

### 14. README compatibility statement versus descriptor version

**Evidence.** `README.md` states the mod is OS-agnostic and actively tested on Linux. The descriptor declares `supported_version="3.2.*"`. The README does not state a game version.

**Status.** No contradiction. The README's compatibility section addresses operating systems; the descriptor addresses game version.

### 15. `ARCHITECTURE.md` deployment table versioning claim

**Evidence.** `ARCHITECTURE.md` lists release tags `v1.0`, `v1.0.1`, and `v1.0.2` and notes that release tags and the declared supported game version evolve independently. `gh release list` confirms three published releases with those tags.

**Status.** Verified consistent. No discrepancy.

## Unverifiable from the repository

| Item | Why it cannot be verified here |
|------|-------------------------------|
| Whether the 8 referenced vanilla trait identifiers exist in game version 3.2.x | Requires a Stellaris installation |
| Whether the 3 referenced vanilla icon paths exist | Requires a Stellaris installation |
| Whether `from` and `FROM` are equivalent | Requires engine documentation or in-game observation |
| Whether `opposites` is symmetric | Requires engine documentation or in-game observation |
| Whether an unquoted `opposites` member parses | Requires engine documentation or in-game observation |
| The engine's default icon for a trait without an `icon` field | Requires in-game observation |
| Whether all 47 traits in fact appear in game | Requires a Stellaris installation |
| Whether any save has ever referenced a removed trait | Requires save data |
| The reason for the 37 unreferenced icons | Requires maintainer statement or repository history that is not present |

## Related documents

- [Error handling](./error-handling.md)
- [Invariants](./invariants.md)
- [Testing](./testing.md)
- [Component: icons](./components/icons.md)
- [Component: localisation](./components/localisation.md)
- [Behaviour: eligibility and exclusions](./behaviour/eligibility-and-exclusions.md)
