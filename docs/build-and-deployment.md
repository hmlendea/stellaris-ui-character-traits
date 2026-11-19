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
| Continuous integration | Absent; `.github/workflows/` does not exist |

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
| Steam Workshop | Mod subscription and launcher sync | Channel metadata maintained outside the repository |
| Paradox Mods | Mod subscription and launcher sync | Channel metadata maintained outside the repository |
| Nexus Mods | Manual download and extraction | Channel metadata maintained outside the repository |
| GitHub Releases | Release archive download and manual extraction | Tags `v1.0`, `v1.0.1`, `v1.0.2` published |
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

No release script or documented release procedure exists in the repository. Releasing is a manual maintainer action: tag the revision, package the payload, publish the release, and update channel listings. The presence of `.gitignore`'s `**/*.zip` rule indicates release archives are produced as ZIP files outside version control.

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
