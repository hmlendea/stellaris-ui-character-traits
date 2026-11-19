# Build and deployment

## No build step

There is nothing to build. The repository ships source content directly: the files under `ui-character-traits/` are the deliverable, and the `.mod` descriptor at the root completes it. No compiler, bundler, packaging manifest, or asset pipeline exists.

| Build concern | Status |
|---------------|--------|
| Compilation | Not applicable |
| Bundling | Not applicable |
| Packaging script | Absent |
| Asset generation or conversion | Absent; DDS and PNG assets are committed as-is |
| Dependency restoration | Absent; no dependencies |
| Continuous integration | Release publication only; `.github/workflows/github-release.yml` attaches the GitHub release archive and `.github/workflows/steam-workshop-release.yml` publishes to Steam Workshop |

## Deployment unit

The deployment unit is:

```text
ui-character-traits.mod          (root descriptor)
ui-character-traits/             (payload directory)
├── descriptor.mod
├── thumbnail.png
├── common/traits/*.txt
├── gfx/interface/icons/traits/*.dds
└── localisation/english/*.yml
```

`.gitignore` excludes `**/*.zip`, so packaged release archives are not tracked.

## Delivery routes

| Route | Mechanism | Notes |
|-------|-----------|-------|
| Steam Workshop | Mod subscription and launcher sync | Item `2048878128`; `.github/workflows/steam-workshop-release.yml` publishes the tagged content automatically on a `v*.*.*` tag push or manual dispatch |
| Paradox Mods | Mod subscription and launcher sync | Channel metadata maintained outside the repository |
| Nexus Mods | Manual download and extraction | Channel metadata maintained outside the repository |
| GitHub Releases | Release archive download and manual extraction | Tags `v1.0`, `v1.0.1`, `v1.0.2` published; `.github/workflows/github-release.yml` builds `ui-character-traits_<version>.zip` from the published tag and attaches it |
| Local mod directory | Manual copy of descriptor and payload | Used for development verification |

The payload is identical for every channel. Only channel-presentation metadata differs, and none of it lives in the repository apart from `.github/cover.png` and `ui-character-traits/thumbnail.png`.

## Manual installation procedure

1. Obtain the release archive from a distribution channel.
2. Extract its contents into the Stellaris mod directory so that `ui-character-traits.mod` and the `ui-character-traits/` directory sit at the same level.
3. Enable the mod in the launcher playset.

## Development deployment loop

Because no build exists, verification requires copying content into a live installation:

1. Edit content in the working tree.
2. Copy `ui-character-traits.mod` and `ui-character-traits/` into the local Stellaris mod directory.
3. Launch the game with the mod enabled.
4. Verify in the leader trait interface.
5. Inspect the engine error log.

Steps 2-5 must be repeated after every change; there is no hot reload.

## Versioning

| Version source | Current value | Notes |
|----------------|---------------|-------|
| Git tags | `v1.0`, `v1.0.1`, `v1.0.2` | `v1.0` tagged 2020-04-05; `v1.0.1` and `v1.0.2` tagged 2021-12-12 and 2021-12-14 |
| GitHub releases | Three published releases: `1.0 - Initial release`, `v1.0.1`, `v1.0.2` | `v1.0.2` is the latest |
| Descriptor `supported_version` | `v4.5.*` | Independent of the release tag |

Release tags and the declared supported game version evolve independently, so they can disagree. A release tag identifies a snapshot of the mod; `supported_version` states which game version that snapshot targets.

## Release procedure

`.github/workflows/github-release.yml` automates the GitHub Releases side. It runs when a GitHub release is published, or on a manual dispatch with a `tag` input: it checks out the requested tag, strips the leading `v` from the tag to derive the version, writes that version into `version` in `ui-character-traits.mod` and `ui-character-traits/descriptor.mod` (inserting the line when absent), builds `ui-character-traits_<version>.zip` containing `ui-character-traits/` and `ui-character-traits.mod`, and attaches the archive to the release. No checksum is computed, and the release body is left as the maintainer wrote it.

`.github/workflows/steam-workshop-release.yml` automates the Steam Workshop side on a `v*.*.*` tag push or a manual dispatch with a `tag` input: it checks out the tag, strips the leading `v` to derive the version, writes that version into `version` in both descriptors, zips and extracts `ui-character-traits/` and `ui-character-traits.mod`, and uploads `release/ui-character-traits/` to Workshop item `2048878128` with a changenote linking the matching release tag. It requires the `STEAM_USERNAME`, `STEAM_PASSWORD`, and `STEAM_2FA_SEED` secrets.

Paradox Mods and Nexus Mods remain manual maintainer actions. To publish:

1. Update both descriptors' `supported_version` if targeting a new game-version family.
2. Tag the revision; `.github/workflows/steam-workshop-release.yml` publishes the tag to Steam Workshop, and publishing the GitHub release makes `.github/workflows/github-release.yml` write the version into both descriptors, build the archive, and attach it.
3. Upload the same content set manually to Paradox Mods and Nexus Mods so that no channel drifts.

The presence of `.gitignore`'s `**/*.zip` rule indicates release archives are produced as ZIP files outside version control, so the workflow's archive is never committed.

## Rollback

The only rollback mechanism is repository history and re-extraction of a prior release archive. There is no in-repo rollback tooling, and no migration mechanism for saves that already reference removed traits. See [State and persistence](./state-and-persistence.md).

## Operational characteristics

| Concern | Value |
|---------|-------|
| Process topology | None; content loaded by the game process |
| Runtime dependencies | None beyond the base game |
| Persistent state owned | None |
| Scaling behaviour | Not applicable |
| Health checks | Not applicable |
| Observability endpoints | Not applicable |
| Backup requirements | None at mod level; players' saves are their own responsibility |

## Related documents

- [Component: descriptor](./components/descriptor.md)
- [Configuration](./configuration.md)
- [Compatibility](./compatibility.md)
- [State and persistence](./state-and-persistence.md)
