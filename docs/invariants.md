# Invariants

System-wide properties that must remain true for the mod to function. Each entry states the invariant, its evidence, the consequence of violation, and how it is currently enforced.

## 1. Identifier uniqueness

**Invariant.** Every trait identifier is unique within the mod and does not collide with a vanilla `leader_trait_*` identifier.

**Evidence.** All 47 identifiers use the `ui_trait_` prefix while vanilla leader traits use `leader_trait_`. No `ui_trait_` identifier duplicates another, and none of the 4.5 vanilla trait identifiers is reused.

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

**Evidence.** 47 of 47 traits have name keys and 47 of 47 have correctly spelled description keys.

**Known orphan.** `ui_trait_governor_securist` has a name/description key pair with no trait definition. This is inert and does not violate the invariant; it is recorded as leftover content.

**Violation consequence.** A missing name key shows the raw identifier; a missing description key shows no description.

**Enforcement.** Convention only.

## 5. Localisation encoding

**Invariant.** The localisation file is UTF-8 **with** a byte-order mark.

**Evidence.** Verified: `UTF-8 (with BOM) text`.

**Violation consequence.** An incorrect encoding can prevent the entire localisation file from loading, affecting all 96 keys simultaneously.

**Enforcement.** Editor configuration and review.

## 6. Icon resolvability

**Invariant.** Every `ICON` value inside the `trait/icon` inline script names a sprite that exists — either declared by the mod in `interface/ui_character_traits.gfx` or by the base game — and every sprite the mod declares points at a texture it ships.

**Evidence.** 47 of 47 traits declare an icon. 44 reference sprites declared in the mod's own `.gfx` file, each mapping to one of the 44 shipped DDS assets; the remaining 3 reference vanilla sprites (`GFX_leader_trait_engineering_focus`, `GFX_leader_trait_physics_focus`, `GFX_leader_trait_society_focus`).

**Violation consequence.** An unresolvable sprite yields a placeholder or default icon.

**Enforcement.** Manual. The 3 vanilla sprite references are a compatibility dependency, not a defect, provided the base game retains those assets.

## 7. Exclusion reference validity

**Invariant.** Every identifier in an `opposites` list exists — either as another mod trait or as a vanilla trait in the supported game version.

**Evidence.** 75 references to mod identifiers across 38 lists; all resolve. 14 references to 8 vanilla identifiers depend on the base game.

**Violation consequence.** An unresolved reference is inert: the intended exclusion silently does not occur.

**Enforcement.** Manual review against the target game version.

## 8. Scope consistency

**Invariant.** A trait's `leader_class` list contains only classes valid in the supported game version, and where a subclass is required the `leader_potential_add` block admits leaders that cannot carry a subclass.

**Evidence.** All 47 definitions use only `commander`, `official` and `scientist`. The 7 subclass-gated traits all include a `has_paragon_dlc = no` leg so DLC-less players retain access.

**Violation consequence.** A trait scoped to a removed class (such as `admiral` or `governor`) or gated solely on a subclass would be unreachable.

**Enforcement.** Convention, plus the field vocabulary in [Data model](./data-model.md).

## 9. Modifier scoping

**Invariant.** Every trait declares exactly one explicitly scoped modifier block — `planet_modifier`, `fleet_modifier`, `army_modifier`, `councilor_modifier` or `self_modifier` — and never the unscoped `modifier = { }` form.

**Evidence.** 47 of 47 traits use a scoped block: 34 `planet_modifier`, 6 `fleet_modifier`, 5 `councilor_modifier`, 1 `army_modifier`, 1 `self_modifier`. No unscoped `modifier` block appears, matching the vanilla 4.5 corpus.

**Violation consequence.** An unscoped block applies to whatever object the leader happens to be assigned to, which in 4.x can silently apply a planet modifier to a fleet commander.

**Enforcement.** Convention; verifiable by inspecting for `modifier = {` without a scope prefix.

## 10. Exhaustive omission is deliberate

**Invariant.** A trait may omit `opposites` and `leader_potential_add`; omission is a valid state rather than a defect.

**Evidence.** 10 traits omit `opposites`; 11 omit `leader_potential_add`. Every trait declares an icon, a scoped modifier block and a `selectable_weight`.

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
