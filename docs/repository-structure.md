# Repository structure

## Absolute layout

```text
stellaris-ui-character-traits/
├── .github/
│   ├── cover.png                       # Repository/listing cover art (distribution metadata)
│   └── FUNDING.yml                     # Sponsorship configuration
├── .gitignore                          # Ignores **/*.zip (packaged release archives)
├── ARCHITECTURE.md                     # Root architecture document
├── CODE_OF_CONDUCT.md                  # Root policy document
├── CONTRIBUTING.md                     # Root contribution guide
├── LICENSE                             # GNU General Public License v3.0
├── PRIVACY.md                          # Root privacy statement
├── README.md                           # Root README
├── SECURITY.md                         # Root security policy
├── docs/                               # This documentation tree
├── ui-character-traits.mod             # Root descriptor (launcher entry point)
└── ui-character-traits/                # Mod payload directory
    ├── descriptor.mod                  # In-payload descriptor (byte-identical to root)
    ├── thumbnail.png                   # 400x400 RGBA PNG distribution thumbnail
    ├── common/
    │   └── traits/
    │       ├── ui-traits_leader.txt              # 1 class-agnostic trait
    │       ├── ui-traits_leader_admiral.txt      # 6 admiral traits
    │       ├── ui-traits_leader_general.txt      # 1 general trait
    │       ├── ui-traits_leader_governor.txt     # 34 governor traits
    │       └── ui-traits_leader_ruler.txt        # 5 ruler traits
    ├── gfx/
    │   └── interface/
    │       └── icons/
    │           └── traits/             # 45 DDS icon assets (flat, no subdirectories)
    └── localisation/
        └── english/
            └── ui-traits_l_english.yml # 48 name keys + 48 description keys
```

## Why the payload directory exists

The launcher resolves a mod body through the `path` field of a descriptor. Both descriptors declare `path="mod/ui-character-traits"`, which corresponds to the `ui-character-traits/` directory in this repository. Consequently:

- The `.mod` descriptor must stay at the repository root.
- The payload must remain in a directory whose name matches the `path` value's final segment.
- Content changes are invisible to the launcher until the payload is delivered through a distribution channel or a local mod directory.

## Content-area responsibilities

| Path | Shadowed vanilla target | Responsibility |
|------|------------------------|----------------|
| `common/traits/` | `common/traits/` | Adds trait definitions to the leader trait pool |
| `localisation/english/` | `localisation/english/` | Adds localisation keys to the English key space |
| `gfx/interface/icons/traits/` | `gfx/interface/icons/traits/` | Supplies image assets resolvable by path |

The files inside `common/traits/` are new, mod-namespaced files. Because Stellaris merges mod directories additively rather than replacing vanilla files that do not share a filename, these files add definitions rather than override vanilla trait files.

## File-naming conventions

| Convention | Observation |
|------------|-------------|
| Trait definition files | `ui-traits_leader[_<class>].txt`; class suffix matches the dominant class in the file |
| Localisation file | `ui-traits_l_english.yml` — `<prefix>_l_<language>.yml` |
| Icon files | Named after the trait's theme, not its full identifier (e.g. `ui_trait_berserker.dds` serves `ui_trait_admiral_berserker`) |
| Identifiers | snake_case with the `ui_trait_` prefix |

## Files not present

| Absent artefact | Consequence |
|-----------------|-------------|
| `.github/workflows/` | No CI, no automated validation, no release automation |
| Build or packaging scripts | Releases are produced manually and attached to Git tags |
| Test directories or harnesses | No automated verification of content consistency |
| `ROADMAP.md`, `CHANGELOG.md`, `SUPPORT.md`, `FAQ.md` | Those README conditions are unmet |
| Non-English localisation directories | The mod is English-only |

## Related documents

- [Repository overview](./repository-overview.md)
- [Architecture](./architecture.md)
- [Components](./components/)
