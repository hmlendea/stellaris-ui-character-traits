# Component: descriptor

## Purpose

The descriptor declares the mod's identity to the Stellaris launcher. It is the first file the launcher resolves and the only gate on whether the rest of the payload is loaded at all.

## Files

| File | Location | Role |
|------|----------|------|
| `ui-character-traits.mod` | Repository root | Discovered first by the launcher when the repository is used as a mod directory |
| `ui-character-traits/descriptor.mod` | Inside the payload | Read when the payload directory itself is registered or packaged |

The two files are **byte-identical**. Verified by direct comparison.

## Content

```text
name="Universum Infinitum - Character Traits"
path="mod/ui-character-traits"
tags={
    "Characters"
}
supported_version="v4.5.*"
```

## Field semantics

| Field | Value | Consumer | Effect |
|-------|-------|----------|--------|
| `name` | `Universum Infinitum - Character Traits` | Launcher, distribution listings | Display name in the playset interface and on store pages |
| `path` | `mod/ui-character-traits` | Launcher | Resolves the mod body. The final segment must match the payload directory name |
| `tags` | `Characters` | Launcher | Categorisation in the launcher's mod browser |
| `supported_version` | `v4.5.*` | Launcher | Compatibility gate. A mismatch marks the mod incompatible |

## Why two descriptors exist

The launcher supports two installation shapes:

1. A `<modname>.mod` file at a mod-root level alongside a payload directory, using `path` to locate the payload. This is the shape produced by extracting a release archive into the game's mod directory.
2. A self-describing payload directory containing its own `descriptor.mod`. This is the shape used when a platform registers the payload directly.

Supplying both makes the same payload usable in either shape without modification.

## Invariants

- Both descriptors must remain byte-identical. Divergence produces version-gate or path inconsistencies depending on which shape the player installed.
- `path` must agree with the payload directory name. Renaming `ui-character-traits/` without updating `path` makes the mod unloadable.
- `supported_version` is the only declared compatibility statement in the repository. See [Compatibility](./../compatibility.md).
- Neither descriptor may contain executable content. Both are declarative Clausewitz.

## Change procedure

1. Update the value in `ui-character-traits.mod`.
2. Apply the identical change to `ui-character-traits/descriptor.mod`.
3. Confirm the two files still compare equal.
4. Re-verify in the launcher that the mod registers and enables.

## Related documents

- [Repository structure](./../repository-structure.md)
- [Compatibility](./../compatibility.md)
- [Build and deployment](./../build-and-deployment.md)
