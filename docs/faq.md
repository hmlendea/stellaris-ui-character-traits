# Frequently asked questions

## What does this mod do?

It adds 47 leader traits to Stellaris, mapped onto the 4.x leader model: fleet commanders, army commanders, governors, and councilors. Names include Berserker, Guerillero, Glass Cannon, Sniper, Stormer, Testudo, Crusader, Corporatist, Environmentalist, Moral Authority, Naturalist, Racist, Open-armed, Peacebringer, Fascist Demagogue, Antique Collector, and Efficient Bureaucrat, among others. See the [trait catalogue](./components/trait-catalogue.md) for the complete list.

## Does the mod require a new game?

No. Enabling the mod makes its traits available as candidates in existing saves as well as new ones.

## Is the mod compatible with other mods?

Yes, in practice. The mod is additive and uses the `ui_trait_` identifier prefix, so it does not claim vanilla identifiers or shadow vanilla files. The one caveat is that its exclusion lists reference vanilla trait identifiers, so another mod that alters those vanilla traits could change this mod's exclusion behaviour.

## Does it work on macOS and Windows?

The mod is content-only, with no executable code and no platform-specific paths, so it works wherever the game does. Development and testing are performed on Linux.

## Which game version is supported?

`v4.5.*`, declared in both descriptor files. Behaviour on other versions is unverified.

## Why are some traits not appearing?

Three reasons, in order of likelihood:

1. **Scope** — the trait is not scoped to that leader class. For example, `ui_trait_admiral_berserker` appears only for `commander` leaders on the admiral subclass.
2. **Eligibility** — a condition is not met. Most governor traits exclude hive-mind empires, for example.
3. **Exclusions** — the leader already holds a trait listed in the candidate's `opposites`.

See [Eligibility and exclusions](./behaviour/eligibility-and-exclusions.md).

## Why does a trait have no description?

All 47 traits now have correctly spelled description keys. The two previously misspelled
`idsustrialist` keys were corrected during the 4.5 update. One orphaned key pair remains
(`ui_trait_governor_securist`) for a trait that was never defined; see
[Open questions](./ambiguities-and-open-questions.md).

## Why does a trait have no icon?

Only 11 of 47 traits declare an `icon`; the remaining 36 inherit the engine's default. This is intentional rather than a defect — the author only added icons for the admiral and general traits plus the class-agnostic trait.

## Why are there 45 icons but only 8 are used?

The icon filename is not the trait identifier, so a naive match does not find them. Eight of the shipped icons are referenced by traits that declare an `icon`. The remaining 37 are committed assets that no definition currently names. See [Component: icons](./components/icons.md).

## Can I add my own trait?

Yes. See the [change guide](./change-guide.md). The short version: add a trait block to the file matching the leader class, add a name key **and** a `_desc` key to the localisation file, optionally add an icon, then verify in game.

## Can I rename a trait?

No. Identifiers are effectively immutable because localisation keys, `opposites` entries, `has_trait` references, icon filenames, and existing saves all reference them by literal string. Add a new identifier and deprecate the old trait instead.

## Why can't I modify some traits?

They no longer can, and this is a 4.x change rather than a mod setting. The mod previously declared `modification = no` on governor and ruler traits; that field no longer exists in the 4.x leader trait schema, so it was removed.

## Do the traits have the same cost as vanilla traits?

The 4.x leader trait schema has no `cost` field, so mod traits are weighted by
`selectable_weight` instead. They reuse the base game's own weight variables and inline
scripts, so they are offered at the same tier as the vanilla traits they sit beside.

## Does the mod collect any data?

No. It requests, collects, transmits, and persists no personal data and has no telemetry. See [PRIVACY.md](../PRIVACY.md).

## Does the mod send anything to the network?

No. It contains no network logic. Distribution platforms handle delivery separately from mod execution.

## How do I uninstall it?

Disable it in the launcher and remove it from the mod directory. Note that saves already holding mod traits may fail to resolve them afterwards.

## How do I report a bug?

Open an [issue](https://github.com/hmlendea/stellaris-ui-character-traits/issues). For security concerns, follow [SECURITY.md](../SECURITY.md) instead of a public issue.

## Where is the architecture documented?

See [ARCHITECTURE.md](../ARCHITECTURE.md) for the authoritative high-level architecture and [Architecture (content model deep dive)](./architecture.md) for the load pipeline and override semantics.

## Related documents

- [Quick start](./quick-start.md)
- [Troubleshooting](./troubleshooting.md)
- [Change guide](./change-guide.md)
- [Open questions](./ambiguities-and-open-questions.md)
