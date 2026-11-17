# Quick start

## For players

1. Obtain the mod from a supported channel:
   - [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2048878128)
   - [Paradox Mods](https://mods.paradoxplaza.com/mods/34606/Any)
   - [Nexus Mods](https://nexusmods.com/stellaris/mods/90)
   - [GitHub Releases](https://github.com/hmlendea/stellaris-ui-character-traits/releases)
2. Enable the mod in the Stellaris launcher's playset. The launcher validates `supported_version="v4.5.*"`.
3. Start a game or load a save. Leader traits from the mod appear in the leader trait interface when their eligibility conditions are met.

### Manual installation

1. Download the [latest release](https://github.com/hmlendea/stellaris-ui-character-traits/releases).
2. Extract the archive contents into the game's mod directory.
3. Enable the mod in the launcher.

## For contributors

There is nothing to build, install, or compile. The workflow is edit, deploy locally, verify in game.

### Prerequisites

- A Stellaris installation matching the declared `supported_version` (`v4.5.*`) for in-game verification.
- A text editor with Clausewitz script and YAML syntax support.
- The ability to inspect or convert DDS images if you intend to create icons.

### Setup

```bash
git clone https://github.com/hmlendea/stellaris-ui-character-traits.git
cd stellaris-ui-character-traits
```

No dependency installation step exists: the repository contains only static content.

### Make a change

1. Fork the repository and create a branch from `master`.
2. Edit trait definitions in `ui-character-traits/common/traits/`.
3. Add or update localisation in `ui-character-traits/localisation/english/ui-traits_l_english.yml`.
4. Add or reuse an icon in `ui-character-traits/gfx/interface/icons/traits/` if the trait declares an `icon`.
5. Copy the `ui-character-traits/` payload and `ui-character-traits.mod` descriptor into your local Stellaris mod directory.
6. Launch the game and verify the trait in the leader trait interface.
7. Inspect the game error log for trait, localisation, or icon errors attributable to the mod.

### Before opening a pull request

- Target the `master` branch.
- Keep the change focused.
- Confirm the [invariants](./invariants.md) still hold:
  - Identifier unique across the mod and against vanilla `leader_trait_*`.
  - Name key and `_desc` key present for the trait.
  - Every `icon` path resolves.
  - Every `opposites` and `leader_potential_add` trait reference exists.
- Update affected documentation. See the [change guide](./change-guide.md).

## Where to go next

| Goal | Document |
|------|----------|
| Look up an existing trait | [Trait catalogue](./components/trait-catalogue.md) |
| Understand a field | [Data model](./data-model.md) |
| Understand eligibility | [Eligibility and exclusions](./behaviour/eligibility-and-exclusions.md) |
| Understand what breaks what | [Invariants](./invariants.md), [Troubleshooting](./troubleshooting.md) |
