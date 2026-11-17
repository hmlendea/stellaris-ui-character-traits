# Integrations

## Integration inventory

| Integration | Direction | Compatibility | Purpose | Required | Owner |
|-------------|-----------|---------------|---------|----------|-------|
| Stellaris launcher | Inbound | Stellaris 3.2.x | Registers the mod, validates `supported_version`, shows it in the playset | Required | External |
| Stellaris game engine | Inbound | Stellaris 3.2.x | Parses, resolves, and renders all mod content | Required | External |
| Steam Workshop | Inbound delivery | Platform-managed | Distributes the mod (item 2048878128) | One channel required | External |
| Paradox Mods | Inbound delivery | Platform-managed | Distributes the mod (mod 34606) | One channel required | External |
| Nexus Mods | Inbound delivery | Platform-managed | Distributes the mod (mod 90) | One channel required | External |
| GitHub Releases | Inbound delivery | Platform-managed | Distributes release archives | One channel required | External |
| Base-game content | Outbound reference | Version-coupled | Supplies 8 vanilla trait identifiers, 3 vanilla icon paths, and vanilla authority and ethic identifiers the mod reads | Required for the traits that reference them | External |

The mod initiates no outbound interaction at any point. Every integration is consumed by the mod or delivers the mod to a player.

## Integration contracts

### Launcher contract

| Aspect | Detail |
|--------|--------|
| Input | `ui-character-traits.mod` and/or `ui-character-traits/descriptor.mod` |
| Fields consumed | `name`, `path`, `tags`, `supported_version` |
| Validation | `supported_version` against the installed game version; `path` resolution to the payload |
| Failure semantics | Unreadable descriptor leaves the mod unregistered; version mismatch marks it incompatible; unresolvable `path` leaves the payload unused |
| Mod-side mitigation | None; the descriptor is declarative |

### Engine contract

| Aspect | Detail |
|--------|--------|
| Input | `common/traits/*.txt`, `localisation/english/*.yml`, `gfx/interface/icons/traits/*.dds` |
| Consumed semantics | Trait identity, cost, modifiers, scope, eligibility, exclusions, modification policy, generation policy, icon reference, localisation keys |
| Validation | Parsing, identifier registration, key binding, reference resolution |
| Failure semantics | Per-stage; see [Error handling](./error-handling.md) |
| Mod-side mitigation | Identifier pairing across definitions, localisation, and assets |

### Base-game content contract

| Aspect | Detail |
|--------|--------|
| Direction | The mod reads; it never writes |
| Read by identifier | 8 vanilla trait identifiers, 13 ethics, 2 authorities |
| Read by path | 3 vanilla icon paths |
| Validation available | None within the repository |
| Failure semantics | An unresolved reference is inert; the intended exclusion, condition, or icon silently does not apply |

## Platform integration boundaries

| Platform | What the repository supplies | What lives outside the repository |
|----------|------------------------------|----------------------------------|
| Steam Workshop | The payload and the descriptor | Item listing, description, tags, screenshots, version notes |
| Paradox Mods | The payload and the descriptor | Listing metadata |
| Nexus Mods | The payload and the descriptor | Listing metadata |
| GitHub Releases | The payload, the descriptor, Git tags, and release assets | Release notes beyond the tag annotation |

No platform-specific code, path, or behaviour exists in the mod. The same payload serves every channel.

## Absent integrations

| Integration type | Status |
|------------------|--------|
| Network APIs or webhooks | Absent |
| Databases or message queues | Absent |
| Authentication or identity providers | Absent |
| Telemetry, analytics, or crash reporting | Absent |
| Update checks or self-updating mechanism | Absent; distribution platforms manage updates |
| Other Stellaris mods | No declared dependency, no load-order requirement, no compatibility shim |
| Other Paradox games | Absent; the payload uses Stellaris directory conventions |

## Cross-mod interaction

The mod is additive and namespace-isolated, so it interoperates with other mods without declaring anything:

- All identifiers are prefixed `ui_trait_`, so another mod cannot accidentally collide within this mod's namespace.
- No file shares a vanilla filename, so the mod does not shadow vanilla files that another mod might also target.
- The `opposites` lists do reference vanilla identifiers, so another mod that alters those vanilla traits could change this mod's exclusion behaviour.
- If two mods both define the same `ui_trait_` identifier, the later-resolved definition wins; no cross-mod conflict detection exists on either side.

## Related documents

- [Dependencies](./dependencies.md)
- [Compatibility](./compatibility.md)
- [Security](./security.md)
- [ARCHITECTURE.md](../ARCHITECTURE.md)
