# Change guide

Procedures for modifying each content area safely. Read [Invariants](./invariants.md) first; every procedure below exists to preserve those invariants.

## Adding a new leader trait

The full procedure, in order.

1. **Choose the identifier.** Format: `ui_trait_<class>_<theme>` for a class-scoped trait, or `ui_trait_leader_<theme>` for a class-agnostic trait. Verify it does not already exist anywhere in `common/traits/`.

2. **Add the trait block** to the file whose class suffix matches the trait's class:
   - Admiral → `ui-traits_leader_admiral.txt`
   - General → `ui-traits_leader_general.txt`
   - Governor → `ui-traits_leader_governor.txt`
   - Ruler → `ui-traits_leader_ruler.txt`
   - Class-agnostic → `ui-traits_leader.txt`

3. **Declare the mandatory fields.** Every existing trait declares `cost`, `modifier`, `leader_trait`, and `leader_class`:

   ```text
   ui_trait_governor_example = {
       cost = 1
       modifier = {
           planet_jobs_unity_produces_mult = 0.10
       }
       leader_trait = { governor }
       leader_class = { governor }
   }
   ```

4. **Set `leader_trait` and `leader_class` consistently.** Use the same class set in both, matching the file the trait was added to.

5. **Declare `opposites` if the trait conflicts with existing ones.** Every identifier listed must exist as a mod trait or a vanilla trait. Add the reverse edge to each referenced mod trait if the exclusion is intended to be mutual; see the note on directionality below.

6. **Declare `leader_potential_add` if the trait must be gated.** Follow the dominant pattern: exclude hive minds and machine intelligences unless there is a reason not to, and reject the fanatic form of any opposing ethic.

7. **Decide on `modification`.** Follow the class convention: governor and ruler traits declare `modification = no`; admiral, general, and class-agnostic traits do not declare the field.

8. **Add the localisation pair.** In `localisation/english/ui-traits_l_english.yml`, add the description entry immediately before the name entry, grouped with the trait's class:

   ```yaml
    ui_trait_governor_example_desc:0 "Description text.§!\n"
    ui_trait_governor_example:0 "Display Name"
   ```

   Both keys must match the identifier exactly, including spelling. Preserve the leading space, the `:0` marker, and the double quotes. Keep the file UTF-8 **with** BOM.

9. **Add or reuse an icon.** If the trait declares `icon`, either:
   - Add a DDS file to `gfx/interface/icons/traits/` and reference it by full path, or
   - Reference an existing vanilla icon path.

   Note the naming convention: icon filenames are theme-based and do not repeat the full trait identifier (for example `ui_trait_berserker.dds` serves `ui_trait_admiral_berserker`).

10. **Verify in game.** Deploy the descriptor and payload to the local mod directory, launch, and confirm the trait appears with the intended name, description, and icon, and that its eligibility and exclusions behave as intended.

11. **Update documentation.** Revise [Component: trait catalogue](./components/trait-catalogue.md), [Component: leader traits](./components/leader-traits.md), [Data model](./data-model.md) counts, and [Behaviour: eligibility and exclusions](./behaviour/eligibility-and-exclusions.md) statistics.

## Modifying an existing trait

| Change | Safe? | Notes |
|--------|-------|-------|
| Adjust a modifier value | Yes | Updates propagate on next load; no other file references values |
| Add or remove a modifier entry | Yes | Same as above |
| Change `cost` | Yes | |
| Change `icon` | Yes | Ensure the new path resolves |
| Add an entry to `opposites` | Yes | Ensure the identifier exists and consider the reverse edge |
| Remove an entry from `opposites` | Yes | Verify the exclusion was not load-bearing for balance intent |
| Change `leader_potential_add` | Yes | Re-verify in game |
| Change `leader_trait` or `leader_class` | Yes, with care | Both must stay in agreement; changing scope moves the trait between pools |
| Set or unset `modification` | Yes | Changes whether modification can add or remove it |
| Change `initial` or `randomized` | Yes | |
| **Rename the identifier** | **No** | Breaks localisation binding, every `opposites` reference, every `has_trait` reference, and existing saves. Add a new identifier and deprecate the old one instead. |
| **Delete the trait** | **No** | Saves referencing it break. See [State and persistence](./state-and-persistence.md). |

## Editing localisation

1. Open `localisation/english/ui-traits_l_english.yml` with an editor that preserves the UTF-8 BOM. Confirm the BOM is present after saving.
2. Preserve the entry form exactly: one leading space, `key:0 "value"`, double quotes.
3. When changing a trait identifier, update both its name key and its `_desc` key — and see the warning against renaming identifiers above.
4. Keep `§!` and `\n` sequences intact; `§!` closes the engine's colour block and `\n` inserts a line break.
5. When adding a trait, add **both** keys. A missing `_desc` key produces a trait with no description; a missing name key produces a raw identifier.

### Existing localisation defects

| Defect | Location | Fix |
|--------|----------|-----|
| `ui_trait_governor_consumer_idsustrialist_desc` misspelled | Line 28 | Rename to `ui_trait_governor_consumer_industrialist_desc` |
| `ui_trait_governor_war_idsustrialist_desc` misspelled | Line 94 | Rename to `ui_trait_governor_war_industrialist_desc` |
| `ui_trait_governor_securist` and `_desc` orphaned | Lines 86-87 | Either add a matching trait definition or remove the pair |

## Editing icons

1. Confirm the asset is DDS. The engine performs no runtime conversion.
2. Place it directly in `gfx/interface/icons/traits/`; subdirectories would require changing every referencing path.
3. Reference it from the trait's `icon` field using the full path `gfx/interface/icons/traits/<file>.dds`.
4. Ignore the prevailing trend of unused assets; do not add an icon the trait does not reference.

## Editing the descriptor

1. Change the value in `ui-character-traits.mod`.
2. Apply the identical change to `ui-character-traits/descriptor.mod`.
3. Verify the two files compare equal.
4. If changing `supported_version`, re-verify all vanilla references listed in [Dependencies](./dependencies.md).
5. If changing `path`, rename the payload directory to match.

## Adding a new localisation language

1. Create `localisation/<language>/` using the engine's language directory name.
2. Create `<prefix>_l_<language>.yml` with the matching `l_<language>:` root block.
3. Copy every key, translated. Missing keys fall back to showing the identifier.
4. Preserve UTF-8 encoding with BOM.

## Exclusions: the directionality caution

`opposites` declarations are not consistently symmetric in this corpus. Seven edges are declared in one direction only. Whether the engine treats the relationship as symmetric is unverified. When adding an exclusion:

- Declare it on **both** traits if mutual exclusion is intended, matching the pattern used by the admiral pairs and the ideologue pairs.
- Declare it on one trait only if the intent is intentionally one-sided, and note why.

## Documentation synchronisation

After any content change, review and update:

| Document | Update when |
|----------|-------------|
| [Component: trait catalogue](./components/trait-catalogue.md) | Any trait is added, removed, or modified |
| [Component: leader traits](./components/leader-traits.md) | Counts, the iterator table, or distribution statistics change |
| [Component: localisation](./components/localisation.md) | Keys are added, removed, or renamed |
| [Component: icons](./components/icons.md) | Icon assets or references change |
| [Data model](./data-model.md) | Field usage or counts change |
| [Behaviour documents](./behaviour/) | Eligibility, exclusions, modifiers, or scope change |
| [Invariants](./invariants.md) | An invariant is added, violated, or repaired |
| [Dependencies](./dependencies.md) | A vanilla reference is added or removed |
| [Compatibility](./compatibility.md) | `supported_version` changes or a vanilla reference fails to resolve |
| [Ambiguities and open questions](./ambiguities-and-open-questions.md) | A question is resolved or a new one arises |
| [README.md](../README.md) | Installation, compatibility, or privacy statements change |
| [ARCHITECTURE.md](../ARCHITECTURE.md) | Architecture, constraints, or extension points change |

## Related documents

- [Invariants](./invariants.md)
- [Testing](./testing.md)
- [Troubleshooting](./troubleshooting.md)
