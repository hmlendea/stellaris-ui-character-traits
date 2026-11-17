# State and persistence

## State owned by the mod

None. The mod owns no mutable runtime state, allocates nothing, and writes nothing. Its content is read once by the engine at game start and is immutable thereafter.

| State category | Owner | Location |
|----------------|-------|----------|
| Trait definitions | Engine (derived from content) | In-memory trait pool |
| Localisation strings | Engine (derived from content) | In-memory key space |
| Icon textures | Engine (loaded from assets) | In-memory texture cache |
| Which traits a leader holds | Engine, persisted in save data | Player's save game |
| Which mods are enabled | Launcher configuration | Launcher playset file |
| Mod files on disk | Filesystem | Player's mod directory |

## Why this matters

Because the mod holds no state, it cannot corrupt, migrate, or validate anything. Every stateful consequence of the mod's content — a leader possessing a trait, that trait's modifiers being applied — is engine-owned and persisted by the engine, not by the mod.

## Save-data coupling

The mod's most significant persistence consequence is indirect. A granted trait is recorded in the save by its **identifier string**. This creates two hazards:

| Scenario | Effect |
|----------|--------|
| A trait is removed from the content while a save holds it | The save references an identifier the engine no longer knows. The trait cannot be resolved or displayed correctly. |
| A trait identifier is renamed | Existing saves reference the old identifier, which no longer resolves. Localisation and exclusions break as well. |
| `supported_version` is raised and the game updates | Saves carrying the trait may load, but the vanilla references the trait depends on may have changed. |

This is why [identifier immutability](./invariants.md) is a hard invariant rather than a style preference: a rename is effectively a data migration, and the repository provides no migration mechanism.

## Enabling and disabling the mod

| Action | Effect |
|--------|--------|
| Enable the mod and start a new game | Mod traits become candidates subject to scope and eligibility |
| Enable the mod and load an existing save | Mod traits become candidates for leaders in that save |
| Disable the mod and load a save holding mod traits | The save references traits the engine cannot resolve; behaviour depends on the engine's handling of unknown trait identifiers |
| Remove the mod files | Same as disabling, permanently for that installation |

No transition is validated or guarded by the mod, because the mod cannot execute code.

## Caching

No repository-side caching exists. The engine caches parsed definitions, localisation keys, and textures for the duration of the session; that cache is discarded when the game exits. A content change therefore requires a game restart to take effect.

## Concurrency

Not applicable. The mod defines no threads, no asynchronous work, no locks, and no shared mutable state. All engine-side concurrency is engine-owned and outside the mod's boundary.

## Backup and recovery

| Concern | Repository responsibility |
|---------|--------------------------|
| Player save backups | None |
| Mod content backups | Git history is the only mechanism |
| Rollback of a content change | Revert the commit or re-extract a prior release archive |
| Recovery from a removed trait | Re-add the definition with the identical identifier, or accept that affected saves reference an unknown trait |

## Related documents

- [Invariants](./invariants.md)
- [Build and deployment](./build-and-deployment.md)
- [Data model](./data-model.md)
- [Error handling](./error-handling.md)
