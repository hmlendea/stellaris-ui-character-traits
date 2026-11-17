# Compatibility

## Declared compatibility

The only compatibility statement in the repository is the descriptor field:

```text
supported_version="3.2.*"
```

The launcher uses it to decide whether the mod is compatible with the installed game version. The `3.2.*` pattern accepts any 3.2.x patch release.

## Compatibility matrix

| Boundary | Supported | Evidence | Notes |
|----------|-----------|----------|-------|
| Stellaris game version | `3.2.*` | Both descriptors | Behaviour on any other version is unverified |
| Operating system | All operating systems supported by the game | `README.md` compatibility section | The mod is content-only; no platform-specific code or paths exist. Actively tested on Linux, including via Steam Play. |
| Steam Workshop distribution | Supported | `README.md` badges, `SECURITY.md` supported-version table | |
| Paradox Mods distribution | Supported | `README.md` badges, `SECURITY.md` supported-version table | |
| Nexus Mods distribution | Supported | `README.md` badges, `SECURITY.md` supported-version table | |
| GitHub Releases distribution | Supported | `README.md` badges, `SECURITY.md` supported-version table | |
| Other mods | Expected compatible | `README.md` compatibility section | Additive composition and namespaced identifiers make collisions unlikely |
| Language | English only | `localisation/english/` is the sole localisation directory | |
| Image format | DDS for trait icons; PNG for thumbnail | `ui-character-traits/gfx/interface/icons/traits/`, `thumbnail.png` | DDS is an engine requirement with no runtime conversion |

## Version-coupled dependencies

The mod reads eight vanilla trait identifiers and three vanilla icon paths. Each is a coupling to a specific game version.

| Vanilla identifier | Referenced by | Kind |
|--------------------|---------------|------|
| `leader_trait_righteous` | 3 governor traits | Exclusion |
| `leader_trait_cautious` | 3 admiral traits | Exclusion |
| `leader_trait_scout` | 2 admiral traits | Exclusion |
| `leader_trait_nervous` | 2 admiral traits | Exclusion |
| `leader_trait_intellectual` | `ui_trait_governor_naturalist` (exclusion) and 3 research traits (eligibility) | Exclusion and eligibility |
| `leader_trait_governor_erudite` | `ui_trait_governor_naturalist` | Exclusion |
| `leader_trait_eager` | `ui_trait_leader_politically_connected` | Exclusion |
| `leader_trait_architectural_interest` | `ui_trait_governor_cultural_interest` | Exclusion |

| Vanilla icon path | Referenced by |
|-------------------|---------------|
| `gfx/interface/icons/traits/trait_natural_engineers.dds` | `ui_trait_governor_engineer` |
| `gfx/interface/icons/traits/trait_natural_physicists.dds` | `ui_trait_governor_physicist` |
| `gfx/interface/icons/traits/trait_natural_sociologists.dds` | `ui_trait_governor_sociologist` |

The mod also references vanilla authorities and ethics in eligibility conditions: `auth_hive_mind` (13 references), `auth_machine_intelligence` (5), and ten distinct ethic identifiers including `ethic_gestalt_consciousness`. If any of these is renamed or removed in a game update, the affected condition becomes inert or the trait becomes unreachable.

### Failure behaviour on version change

| Vanilla reference removed | Consequence |
|---------------------------|-------------|
| A trait identifier in `opposites` | Exclusion is inert; the two traits can coexist |
| A trait identifier in `has_trait` | Condition cannot match; trait availability changes |
| An authority or ethic identifier | Condition cannot match; gating silently disappears |
| An icon path | Icon falls back to a default graphic |

None of these produce a hard mod failure. They degrade silently, which is why re-verification is required on every supported-version change.

## Forward and backward compatibility

| Direction | Status |
|-----------|--------|
| Newer game version | Unverified. Requires manual re-validation of vanilla references. The descriptor would also need updating to admit the new version. |
| Older game version | Unverified. Identifiers and icons may not exist in earlier versions. |
| Save compatibility forward | Traits already granted persist by identifier; new traits appear as candidates. |
| Save compatibility backward | Removing a trait definition leaves saves referencing an unknown identifier. This is not recoverable in-repo. See [State and persistence](./state-and-persistence.md). |

## Encoding compatibility

| File type | Required encoding | Current state |
|-----------|-------------------|---------------|
| Trait definitions | ASCII is sufficient | ASCII (`common/traits/*.txt`) |
| Descriptors | ASCII is sufficient | ASCII |
| Localisation | **UTF-8 with BOM** | UTF-8 with BOM |
| Icons | Binary DDS | Binary DDS |
| Thumbnail | Binary PNG | PNG, 400x400, RGBA, non-interlaced |

The localisation BOM is not cosmetic: engine localisation readers can reject a file without it, which would remove all 96 keys at once.

## Related documents

- [Dependencies](./dependencies.md)
- [Integrations](./integrations.md)
- [Component: descriptor](./components/descriptor.md)
- [Testing](./testing.md)
