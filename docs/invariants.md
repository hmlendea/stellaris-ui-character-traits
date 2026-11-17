# Invariants

System-wide properties that must remain true for the mod to function. Each entry states the invariant, its evidence, the consequence of violation, and how it is currently enforced.

## 1. Identifier uniqueness

**Invariant.** Every trait identifier is unique within the mod and does not collide with a vanilla `leader_trait_*` identifier.

**Evidence.** All 47 identifiers use the `ui_trait_` prefix while vanilla leader traits use `leader_trait_`. No `ui_trait_` identifier duplicates another.

**Violation consequence.** Two documents sharing an identifier cause the later declaration to supersede the earlier one; the superseded trait's localisation and exclusion references then bind to the wrong definition.

**Enforcement.** Prefix convention only. No automated check exists.

## 2. Identifier immutability

**Invariant.** A released trait identifier never changes.

**Evidence.** Localisation keys, `opposites` entries, `leader_potential_add` `has_trait` references, icon filenames, and save data all reference identifiers by literal string.

**Violation consequence.** Renaming an identifier breaks its localisation binding (raw identifier displayed), breaks every `opposites` reference to it (exclusions become inert), and invalidates leaders in existing saves that hold the trait.

**Enforcement.** Manual review. See the [change guide](./change-guide.md) for the correct approach: add a new identifier instead.

## 3. Descriptor parity

**Invariant.** `ui-character-traits.mod` and `ui-character-traits/descriptor.mod` are byte-identical, and `path` matches the payload directory name.

**Evidence.** Both files contain the same four declarations.

**Violation consequence.** Divergence produces inconsistent version gates or an unresolvable `path`, depending on which installation shape the player used.

**Enforcement.** Manual; verifiable with a direct file comparison.

## 4. Localisation key pairing

**Invariant.** Every trait has a name key equal to its identifier and a description key equal to `<identifier>_desc`.

**Evidence.** 47 of 47 traits have name keys; 45 of 47 have correctly spelled description keys.

**Current violations.** `ui_trait_governor_consumer_industrialist` and `ui_trait_governor_war_industrialist` each lack a correctly spelled description key because the localisation uses `idsustrialist`. Additionally, `ui_trait_governor_securist` has a key pair with no trait definition.

**Violation consequence.** A missing name key shows the raw identifier; a missing description key shows no description.

**Enforcement.** Convention only.

## 5. Localisation encoding

**Invariant.** The localisation file is UTF-8 **with** a byte-order mark.

**Evidence.** Verified: `UTF-8 (with BOM) text`.

**Violation consequence.** An incorrect encoding can prevent the entire localisation file from loading, affecting all 96 keys simultaneously.

**Enforcement.** Editor configuration and review.

## 6. Icon resolvability

**Invariant.** Every `icon` value resolves to a file either shipped by the mod or present in the base game.

**Evidence.** 8 of 11 `icon` references resolve to shipped files; 3 reference vanilla paths (`trait_natural_engineers.dds`, `trait_natural_physicists.dds`, `trait_natural_sociologists.dds`) that the mod does not ship.

**Violation consequence.** An unresolvable icon yields a default or placeholder graphic.

**Enforcement.** Manual. The 3 vanilla references are a compatibility dependency, not a defect, provided the base game retains those assets.

## 7. Exclusion reference validity

**Invariant.** Every identifier in an `opposites` list exists — either as another mod trait or as a vanilla trait in the supported game version.

**Evidence.** 86 bare references to mod identifiers across 37 lists; all resolve. 14 references to 8 vanilla identifiers depend on the base game.

**Violation consequence.** An unresolved reference is inert: the intended exclusion silently does not occur.

**Enforcement.** Manual review against the target game version.

## 8. Scope consistency

**Invariant.** A trait's `leader_trait` pool value and `leader_class` list agree.

**Evidence.** All 47 definitions are internally consistent. The one `all`-pool trait compensates with an explicit class condition.

**Violation consequence.** A trait could be registered in a pool whose classes cannot receive it, or vice versa, making it unreachable or mis-scoped.

**Enforcement.** Convention.

## 9. Modification declaration consistency

**Invariant.** Governs the intentional split: every governor and ruler trait declares `modification = no`; the general and class-agnostic traits do not; no admiral trait declares the field.

**Evidence.** 34 governor + 5 ruler = 39 declarations, exactly matching the observed count.

**Violation consequence.** Inconsistent declaration lets some traits be added or removed through modification, changing the intended design.

**Enforcement.** Convention. Observe the pattern when adding traits by class.

## 10. Exhaustive omission is deliberate

**Invariant.** A trait may declare `modification`, `opposites`, `icon`, and `leader_potential_add` optionally; omission is a valid state rather than a defect.

**Evidence.** 8 traits omit `modification` (the 6 admiral traits, the general trait, and the class-agnostic trait); 10 omit `opposites`; 36 omit `icon`; 26 omit `leader_potential_add`.

**Violation consequence.** None — this invariant exists to prevent a future agent from "fixing" deliberate omissions.

**Enforcement.** Documentation. See [Component: leader traits](./components/leader-traits.md) for the observed distribution.

## 11. Declarative-only content

**Invariant.** No file in the repository contains executable logic, computed values, or dynamic behaviour.

**Evidence.** The corpus consists of literal field assignments and condition blocks. No variables, loops, or expressions appear.

**Violation consequence.** Unsupported constructs are ignored or rejected by the Clausewitz parser, or produce a parse failure that drops the affected trait.

**Enforcement.** Language constraints.

## 12. Additive composition

**Invariant.** The mod adds content and never replaces a vanilla file or definition.

**Evidence.** No filename in `common/traits/`, `localisation/english/`, or `gfx/interface/icons/traits/` matches a vanilla filename.

**Violation consequence.** Replacing a vanilla file would shadow base-game content and could break other mods and vanilla traits.

**Enforcement.** Naming convention — all trait files use the `ui-traits_` prefix.

## Verification status of invariants

| Invariant | Automatable | Currently automated |
|-----------|-------------|---------------------|
| Identifier uniqueness | Yes | No |
| Identifier immutability | Partially (via diff) | No |
| Descriptor parity | Yes | No |
| Localisation key pairing | Yes | No |
| Encoding | Yes | No |
| Icon resolvability | Yes (mod-side) | No |
| Exclusion reference validity | Yes (mod-side) | No |
| Scope consistency | Yes | No |
| Modification declaration consistency | Yes | No |
| Exhaustive omission legality | n/a | n/a |
| Declarative-only content | Partially | No |
| Additive composition | Yes | No |

Every automatable invariant is currently unchecked. See [Testing](./testing.md) for the checks a future contributor could introduce.

## Related documents

- [Testing](./testing.md)
- [Change guide](./change-guide.md)
- [Error handling](./error-handling.md)
- [ARCHITECTURE.md](../ARCHITECTURE.md)
