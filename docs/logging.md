# Logging and diagnostics

## Repository logging

The repository emits **no** logs, metrics, traces, or telemetry. There is no logging framework, no log configuration, no log levels, no structured fields, no correlation identifiers, no sinks, no sampling, and no audit trail. This is a direct consequence of shipping static content rather than executable code.

| Logging concern | Status in this repository |
|-----------------|---------------------------|
| Logging framework | None |
| Log levels | Not applicable |
| Structured fields | Not applicable |
| Correlation identifiers | Not applicable |
| Sinks or destinations | Not applicable |
| Redaction or masking | Not applicable (no data is logged) |
| Retention or rotation | Not applicable |
| Sampling | Not applicable |
| Performance impact | None; content is parsed once at load |
| Error logging | None emitted by the mod |
| Audit logging | None emitted by the mod |
| Runtime level changes | Not supported |

## Available diagnostic surfaces

Diagnostics are supplied entirely by the game and the launcher.

| Surface | Location | Information |
|---------|----------|-------------|
| Launcher mod list | Stellaris launcher | Registration, name, version compatibility status |
| Stellaris error log | Game log directory (`logs/error.log` in the user data directory) | Parse errors, unresolved identifiers, localisation problems, asset errors |
| In-game leader trait interface | Leader detail panel and tooltips | Trait names, descriptions, icons as actually resolved |
| Game log | Game log directory | General load-time information |

No Stellaris installation path or log directory is declared in this repository; the location depends on the player's operating system and installation. See `Locations.md` in the agent home directory for any recorded path.

## What each surface reveals about this mod

| Symptom you can observe | Which surface reports it | What to conclude |
|-------------------------|--------------------------|------------------|
| Mod absent from the playset | Launcher mod list | Descriptor unreadable or `path` unresolvable |
| Mod marked incompatible | Launcher mod list | `supported_version="v4.5.*"` does not match the installed game |
| Raw `ui_trait_*` string shown as a trait name | In-game tooltip; error log | Missing localisation name key |
| Trait shows a name but no description | In-game tooltip | Missing or misspelled `_desc` key |
| Generic or placeholder trait icon | In-game interface | Unresolvable `icon` path |
| A trait never appears | In-game play | Eligibility condition excludes it, or an exclusion removes it |
| Two conflicting traits both offered | In-game play | Exclusion reference unresolved or direction-dependent |
| Localisation problems across all traits at once | Error log | Localisation file encoding or structure problem |

## Absence of repository tooling

There is no script, task, or validation workflow in this repository that validates trait definitions, localisation pairing, or icon references. The existing workflows, `.github/workflows/github-release.yml`, `.github/workflows/nexus-mods-release.yml`, and `.github/workflows/steam-workshop-release.yml`, package the tagged content and publish it to GitHub Releases, Nexus Mods, and Steam Workshop; they perform no consistency checking. All consistency checking is manual and in-game. This is the single largest maintenance risk of the repository and is recorded in [Testing](./testing.md) and [Ambiguities and open questions](./ambiguities-and-open-questions.md).

## Diagnostic commands available to a contributor

Because the content is plain text, standard text tooling serves as the diagnostic layer. No project-provided command exists; the following are generic operations a contributor can run for inspection:

| Goal | Operation |
|------|-----------|
| List all trait identifiers | Extract lines matching a trait block header from `common/traits/*.txt` |
| List all localisation keys | Extract non-description keys from the localisation file |
| Compare the two sets | Diff the extracted identifier list against the extracted key list |
| List all `icon` values | Extract `icon = "..."` values from the trait files |
| List shipped icons | List the contents of `gfx/interface/icons/traits/` |
| List all `opposites` members | Extract the contents of every `opposites` block |
| Verify descriptor parity | Compare the two descriptor files directly |

[Testing](./testing.md) consolidates these into the checks a contributor should perform.

## Related documents

- [Error handling](./error-handling.md)
- [Testing](./testing.md)
- [Troubleshooting](./troubleshooting.md)
