# Configuration

## What configuration means here

The mod has no configuration file, no environment variables, no command-line options, no profiles, no precedence chain, and no secrets. It holds no user-settable options. What the term "configuration" maps to in this repository is the set of **content declarations that determine engine behaviour** — the descriptor fields and the trait document fields. Those are configuration in the sense that they control what the player experiences, but they are committed content, not runtime settings.

## Configuration surfaces

| Surface | Location | Controls | Overridable at runtime |
|---------|----------|----------|------------------------|
| Mod identity and version gate | `ui-character-traits.mod`, `ui-character-traits/descriptor.mod` | `name`, `path`, `tags`, `supported_version` | No |
| Trait identity and cost | Each trait block's identifier and `cost` | Which trait exists and its selection cost | No |
| Trait effect | Each trait's `modifier` block | Static effects while the trait is held | No |
| Trait availability | Each trait's `leader_trait`, `leader_class`, `leader_potential_add`, `opposites` | Where and when the trait can be obtained | No |
| Trait modification policy | Each trait's `modification` | Whether the trait can be added/removed through modification | No |
| Trait generation policy | Each trait's `initial`, `randomized` | Whether the trait can be assigned at generation | No |
| Trait appearance | Each trait's `icon` and the localisation keys | Displayed name, description, and art | No |
| Player-visible text | `localisation/english/ui-traits_l_english.yml` | Names and descriptions | No |

## Declared configuration values

| Field | Value | Effect if changed |
|-------|-------|-------------------|
| `name` | `Universum Infinitum - Character Traits` | Display name in the launcher and store listings |
| `path` | `mod/ui-character-traits` | Must match the payload directory name, or the mod fails to load |
| `tags` | `{ "Characters" }` | Launcher categorisation |
| `supported_version` | `3.2.*` | Compatibility gate; a mismatch marks the mod incompatible |
| `cost` | `1` in all 47 traits | All mod traits share the same selection cost |

## Absent configuration mechanisms

| Mechanism | Status |
|-----------|--------|
| Configuration files (`.ini`, `.json`, `.toml`, `.yaml` other than localisation) | Absent |
| `.env` or `.env.example` | Absent |
| Environment variables | Absent |
| Command-line options | Absent |
| Precedence rules | Absent; there is nothing to precedence-order |
| Named profiles or environments | Absent |
| Hot reload | Absent; content is parsed once at game start |
| Secret references or credential stores | Absent; the repository contains no secrets |
| Network ports | Absent; the mod opens no sockets |
| Runtime-validated configuration | Absent |

## Where actual variability lives

The only meaningful variability in behaviour comes from **engine-evaluated game state**, not from configuration:

| Variable input | Consumed by |
|----------------|-------------|
| Country ethics | 13 `leader_potential_add` declarations |
| Country authority | 20 `leader_potential_add` declarations |
| Leader's existing traits | 3 traits' eligibility |
| Leader class | Scope filtering for all 47 traits |
| Held traits | Offer subtraction via 37 `opposites` declarations |
| Game version | Vanilla identifier and icon reference resolution |
| Game language | Localisation selection (English only supplied) |

Changing these inputs changes which traits appear; no configuration file mediates them.

## Change procedure

Content values are changed by editing the content files directly. See the [change guide](./change-guide.md) for the per-area procedure and [Invariants](./invariants.md) for what must remain true.

## Related documents

- [Component: descriptor](./components/descriptor.md)
- [Data model](./data-model.md)
- [Build and deployment](./build-and-deployment.md)
- [Compatibility](./compatibility.md)
