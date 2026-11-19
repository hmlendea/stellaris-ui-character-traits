# Repository overview

## Purpose

**Universum Infinitum - Character Traits** extends Stellaris with additional leader traits for the admiral, general, governor, and ruler leader classes. The repository exists to supply three coupled content artefacts that the Stellaris engine consumes at load time:

1. **Trait definitions** — Clausewitz script blocks declaring each trait's cost, modifiers, leader-class scope, eligibility conditions, and mutual exclusions.
2. **Localisation** — English display names and descriptions keyed by trait identifier.
3. **Icons** — DDS image assets referenced by trait definitions.

## Scope

The repository owns the following content, and nothing else:

| Owned | Evidence |
|-------|----------|
| 47 trait definitions across 5 files | `ui-character-traits/common/traits/` |
| 48 localisation name keys and 48 description keys in one English file | `ui-character-traits/localisation/english/ui-traits_l_english.yml` |
| 45 DDS icon assets | `ui-character-traits/gfx/interface/icons/traits/` |
| Mod identity and version gate | `ui-character-traits.mod`, `ui-character-traits/descriptor.mod` |
| Distribution thumbnail and cover art | `ui-character-traits/thumbnail.png`, `.github/cover.png` |

## Boundary

The repository deliberately does not own:

- **Trait behaviour semantics.** Eligibility evaluation, exclusion enforcement, modifier application, and trait acquisition are engine-owned. No logic can be expressed in the content.
- **Build, packaging, or release automation.** No build script or packaging manifest exists; `.github/workflows/github-release.yml` attaches the release archive to the GitHub release, and `.github/workflows/steam-workshop-release.yml` and `.github/workflows/nexus-mods-release.yml` publish the tagged content to Steam Workshop and Nexus Mods, while the Paradox Mods listing remains manual.
- **Test automation or consistency checking.** Verification is manual and in-game.
- **Platform metadata.** Steam Workshop, Paradox Mods, and Nexus Mods listing content is maintained outside the repository.
- **Localisation beyond English.** Only `localisation/english/` is present.

## Entry points

| Entry point | Consumed by | Purpose |
|-------------|-------------|---------|
| `ui-character-traits.mod` | Stellaris launcher | Repository-root descriptor the launcher discovers first |
| `ui-character-traits/descriptor.mod` | Stellaris launcher | In-payload descriptor read when the payload is registered as a mod |
| `ui-character-traits/common/traits/*.txt` | Stellaris engine | Trait definitions |
| `ui-character-traits/localisation/english/ui-traits_l_english.yml` | Stellaris engine | Display names and descriptions |
| `ui-character-traits/gfx/interface/icons/traits/*.dds` | Stellaris engine | Icon assets resolved through `icon` references |

The two descriptor files are byte-identical. Both declare `name="Universum Infinitum - Character Traits"`, `path="mod/ui-character-traits"`, `tags={ "Characters" }`, and `supported_version="v4.5.*"`.

## Intended audience

| Audience | What they need |
|----------|----------------|
| Players | Install through a distribution channel; enable in the launcher |
| Contributors | Add or revise traits while preserving identifier, localisation, and icon pairing |
| Maintainers | Re-validate vanilla identifier coupling whenever the supported game version changes |
| Future agents | Reconstruct trait semantics without re-parsing every content file |

## Identifier conventions

| Pattern | Meaning | Count |
|---------|---------|-------|
| `ui_trait_leader_*` | Class-agnostic leader traits | 1 |
| `ui_trait_admiral_*` | Admiral-scoped traits | 6 |
| `ui_trait_general_*` | General-scoped traits | 1 |
| `ui_trait_governor_*` | Governor-scoped traits | 34 |
| `ui_trait_ruler_*` | Ruler-scoped traits | 5 |

## Related documents

- [Repository structure](./repository-structure.md) — where each artefact lives
- [Data model](./data-model.md) — the trait document schema
- [Change guide](./change-guide.md) — modification procedure
- [ARCHITECTURE.md](../ARCHITECTURE.md) — authoritative system-level architecture
