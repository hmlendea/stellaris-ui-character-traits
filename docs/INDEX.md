# Repository Documentation Index

Master index for the internal knowledge base of **Universum Infinitum - Character Traits**, a static-content Stellaris mod that adds leader traits for the admiral, general, governor, and ruler leader classes.

## Repository summary

The repository ships no executable code. Its entire behaviour is expressed as Clausewitz script trait definitions (`ui-character-traits/common/traits/*.txt`), English localisation (`ui-character-traits/localisation/english/ui-traits_l_english.yml`), and DDS icon assets (`ui-character-traits/gfx/interface/icons/traits/`). The Stellaris launcher registers the mod through `ui-character-traits.mod` and `ui-character-traits/descriptor.mod`; the game engine parses the content areas at startup and owns all trait eligibility, exclusion, modifier application, and presentation semantics. The documentation below reconstructs what the content is, how the engine consumes it, and which invariants a change must preserve.

## Root document map

| Document | Purpose |
|----------|---------|
| [README.md](../README.md) | Project purpose, installation channels, compatibility statement |
| [ARCHITECTURE.md](../ARCHITECTURE.md) | Authoritative high-level architecture; not reproduced under `docs/` |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | Contribution process and prerequisites |
| [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md) | Conduct standards for project spaces |
| [SECURITY.md](../SECURITY.md) | Vulnerability reporting and disclosure policy |
| [PRIVACY.md](../PRIVACY.md) | Personal-data handling statement |
| [LICENSE](../LICENSE) | GNU General Public License v3.0 |

`ROADMAP.md` does not exist in this repository.

## Start here

| If you need to... | Read |
|-------------------|------|
| Understand what the repository contains | [Repository overview](./repository-overview.md) |
| Find a specific file or content area | [Repository structure](./repository-structure.md) |
| Install the mod and see traits in game | [Quick start](./quick-start.md) |
| Add or change a leader trait | [Change guide](./change-guide.md) |
| Understand the engine-facing contracts | [Architecture](./architecture.md), [Invariants](./invariants.md) |
| Look up a specific trait | [Trait catalogue](./components/trait-catalogue.md) |

## Deep dive

| Area | Documents |
|------|-----------|
| Content components | [Descriptor](./components/descriptor.md), [Leader traits](./components/leader-traits.md), [Localisation](./components/localisation.md), [Icons](./components/icons.md) |
| Runtime semantics | [Trait scoping](./behaviour/trait-scoping.md), [Eligibility and exclusions](./behaviour/eligibility-and-exclusions.md), [Modifiers and effects](./behaviour/modifiers-and-effects.md) |
| Execution flows | [Game start and content loading](./flows/game-start-and-content-loading.md), [Leader trait acquisition](./flows/leader-trait-acquisition.md) |
| Data | [Data model](./data-model.md), [State and persistence](./state-and-persistence.md) |
| Delivery | [Build and deployment](./build-and-deployment.md), [Configuration](./configuration.md), [Compatibility](./compatibility.md) |
| Quality | [Testing](./testing.md), [Troubleshooting](./troubleshooting.md), [Open questions](./ambiguities-and-open-questions.md) |
| Context | [Design decisions](./design-decisions.md), [Dependencies](./dependencies.md), [Integrations](./integrations.md), [Security](./security.md), [Logging and diagnostics](./logging.md) |

## Documentation catalogue

| File | Description |
|------|-------------|
| [INDEX.md](./INDEX.md) | This master index and navigation aid |
| [repository-overview.md](./repository-overview.md) | Purpose, scope, boundaries, and entry points |
| [repository-structure.md](./repository-structure.md) | Source tree layout and content-area responsibilities |
| [architecture.md](./architecture.md) | Content architecture model, load pipeline, override semantics; complements root `ARCHITECTURE.md` |
| [quick-start.md](./quick-start.md) | Getting started for newcomers and contributors |
| [data-model.md](./data-model.md) | Trait document schema, field vocabulary, and identifier relationships |
| [build-and-deployment.md](./build-and-deployment.md) | Packaging, release channels, and versioning |
| [configuration.md](./configuration.md) | Effective configuration surfaces and their sources |
| [compatibility.md](./compatibility.md) | Game version, platform, mod, and encoding compatibility |
| [invariants.md](./invariants.md) | System-wide invariants that changes must preserve |
| [error-handling.md](./error-handling.md) | Failure modes and their engine-owned consequences |
| [logging.md](./logging.md) | Diagnostic surfaces (engine-owned) and the absence of repository logging |
| [security.md](./security.md) | Content integrity and supply-chain posture; complements root `SECURITY.md` |
| [testing.md](./testing.md) | Verification strategy and consistency checks |
| [change-guide.md](./change-guide.md) | How to modify each content area safely |
| [troubleshooting.md](./troubleshooting.md) | Common symptoms, causes, and resolutions |
| [faq.md](./faq.md) | Frequently asked questions |
| [design-decisions.md](./design-decisions.md) | Reconstructed design rationale |
| [dependencies.md](./dependencies.md) | External dependencies and the vanilla identifier coupling |
| [integrations.md](./integrations.md) | Launcher, engine, and distribution-platform boundaries |
| [state-and-persistence.md](./state-and-persistence.md) | Runtime state ownership and save-data coupling |
| [ambiguities-and-open-questions.md](./ambiguities-and-open-questions.md) | Unresolved items, known gaps, and documentation discrepancies |
| [documentation-maintenance.md](./documentation-maintenance.md) | Ownership and refresh policy for this tree |

### Directories

| Directory | Contents |
|-----------|----------|
| [components/](./components/) | Per-content-area deep dives |
| [behaviour/](./behaviour/) | Trait-pool, eligibility, and modifier semantics |
| [flows/](./flows/) | End-to-end engine execution flows |

### Documented absences

The following documentation areas are intentionally absent because no repository evidence supports them:

| Prescribed area | Reason for absence |
|-----------------|--------------------|
| `api-reference/` (per-controller endpoint reference) | The repository exposes no API, controller, or service. |
| `api-usage-examples.md` | No API exists. |
| `concurrency-and-scheduling.md` | No executable code, threads, or scheduling logic exists. |
| Migration and roadmap documents under `docs/` | `ROADMAP.md` does not exist; policy documents belong at the repository root. |

## Maintenance metadata

| Field | Value |
|-------|-------|
| Last reviewed | 2026-11-17 |
| Repository revision reviewed | `af12aaa` (`master`) |
| Content coverage | All 5 trait definition files, 1 localisation file, 45 icon assets, 2 descriptor files, 5 root documents, `.github/` assets, 2 workflows |
| Coverage status | Complete for content; no executable artefacts exist to document |
| Known gaps | Engine-internal parsing behaviour is described from the mod side only; vanilla identifiers are referenced but cannot be verified from this repository |
