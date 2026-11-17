[![Donate](https://img.shields.io/badge/-%E2%99%A5%20Donate-%23ff69b4)](https://hmlendea.go.ro/fund.html)
[![Latest Release](https://img.shields.io/github/v/release/hmlendea/stellaris-ui-character-traits)](https://github.com/hmlendea/stellaris-ui-character-traits/releases/latest)
[![License](https://img.shields.io/github/license/hmlendea/stellaris-ui-character-traits)](https://github.com/hmlendea/stellaris-ui-character-traits/blob/master/LICENSE)

# Universum Infinitum - Character Traits

Mod that adds various new character traits to Stellaris.

## 📑 Table of Contents

- [Capabilities](#-capabilities)
- [Use Cases](#-use-cases)
- [Usage](#-usage)
- [Known Limitations](#-known-limitations)
- [System Requirements](#-system-requirements)
- [Installation](#-installation)
  - [Manual Installation](#manual-installation)
- [Localisation](#-localisation)
- [Compatibility](#-compatibility)
- [Privacy and Data](#-privacy-and-data)
- [Project Structure](#-project-structure)
  - [Directories](#directories)
- [Architecture](#-architecture)
- [Documentation](#-documentation)
- [FAQ](#-faq)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [Code of Conduct](#-code-of-conduct)
- [Related Projects](#-related-projects)
- [Security](#-security)
- [Support](#-support)
- [Project Engagement](#-project-engagement)
- [License](#-license)

## ✨ Capabilities

- Adds 47 leader traits to Stellaris across the admiral, general, governor, and ruler leader classes.
- Offers opposed traits as deliberate trade-offs, so a leader gains one benefit at the cost of another.
- Gates traits by empire ethics, empire authority, and the leader's existing traits.
- Withholds traits from hive-mind and machine-intelligence empires where their themes conflict with those empires.
- Reuses vanilla icon art where a trait mirrors a vanilla counterpart.
- Requires no new game: mod traits become available in existing saves.
- Remains compatible with other Stellaris mods, because it adds content under its own identifier namespace rather than replacing vanilla content.

## 🎯 Use Cases

- **Players:** Broaden the leader trait pool and make leader development choices more consequential.
- **Contributors:** Add, revise, or remove leader traits without breaking trait identity, localisation pairing, or icon resolution.
- **Maintainers:** Re-verify the mod against a supported Stellaris release before raising the declared version.

## 🚀 Usage

Install the mod from a distribution channel below and enable it in the Stellaris launcher's playset. No further configuration exists.

Once enabled, the mod's traits join the candidate pool for the leader classes they are scoped to. They appear in the leader trait interface when the empire's ethics and authorities, and the leader's existing traits, satisfy the trait's conditions. For example, a governor can be offered `Environmentalist` when the empire is eligible for it, and cannot be offered both `Gun Legaliser` and `Gun Prohibitor` at the same time.

## ⚠️ Known Limitations

- The declared supported game version is `3.2.*`; behaviour on any other game version is unverified.
- Only English localisation is supplied.
- Only 11 of the 47 traits declare an icon; the remainder use the game's default trait icon.
- Two traits currently display no description because of misspelled localisation keys.
- 37 shipped icon assets are not referenced by any trait definition.
- Traits cannot be added, removed, or revised during gameplay; changes require a restart.

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| Stellaris | `3.2.*` | Latest 3.2.x release |
| Operating system | N/A | Linux, macOS, or Windows |

## 📦 Installation

[![Obtain it from Steam Workshop](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/steam-workshop.png)](https://steamcommunity.com/sharedfiles/filedetails/?id=2048878128)
[![Obtain it from Nexus Mods](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/nexus.png)](https://nexusmods.com/stellaris/mods/90)
[![Obtain it from Paradox Mods](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/paradox-mods.png)](https://mods.paradoxplaza.com/mods/34606/Any)
[![Obtain it from GitHub](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/github.png)](https://github.com/hmlendea/stellaris-ui-character-traits/releases)

### Manual Installation

- Download the [latest release](https://github.com/hmlendea/stellaris-ui-character-traits/releases).
- Extract the archive contents into the game's mod directory.
- Enable the mod in the launcher's playset.

## 🌍 Localisation

The mod supplies English names and descriptions for every trait it adds. Trait names and descriptions are keyed by trait identifier, so a missing key displays the raw identifier instead of text.

| Language | Locale | Status |
|----------|--------|--------|
| English | `en` | Complete |

## 🧩 Compatibility

| Component | Supported Versions | Notes |
|-----------|--------------------|-------|
| Stellaris | `3.2.*` | Other game versions are unverified. |
| Operating system | Any supported by the game | The mod contains no executable code and no platform-specific paths. It is actively tested on Linux, including through Steam Play. |
| Other mods | Any | The mod adds content under its own `ui_trait_` identifier namespace and replaces no vanilla file. |

## 🛡️ Privacy and Data

Universum Infinitum - Character Traits does not request, collect, transmit, or persist personal data.

For the detailed description of how the application handles privacy and personal data, see the [Privacy Statement](./PRIVACY.md).

The mod consists of local game definitions, localisation, and image assets. It has no built-in personal-data transfer; interactions with distribution platforms are separate from mod execution.

## 🗂️ Project Structure

The repository is a single Stellaris mod: one descriptor at the repository root, one payload directory containing the mod content, and the repository policy documents.

### Directories

| Directory | Purpose |
|-----------|---------|
| `ui-character-traits/common/traits/` | Clausewitz leader trait definitions |
| `ui-character-traits/localisation/english/` | English trait names and descriptions |
| `ui-character-traits/gfx/interface/icons/traits/` | DDS trait icon assets |
| `docs/` | Repository knowledge base |

## 🏗️ Architecture

Universum Infinitum - Character Traits follows a declarative data-driven plugin architecture for Stellaris.

See the [Architecture Documentation](./ARCHITECTURE.md) for the system context, principal components, runtime flows, ownership boundaries, dependencies, constraints, and extension points.

## 📚 Documentation

The `docs/` directory contains the repository knowledge base: the content model, the trait catalogue, engine-facing behaviour, and the invariants a change must preserve.

| Resource | Description |
|----------|-------------|
| [Documentation index](./docs/INDEX.md) | Navigation aid for the complete knowledge base |
| [Quick start](./docs/quick-start.md) | Installation for players and local verification for contributors |
| [Architecture deep dive](./docs/architecture.md) | Content resolution pipeline, namespace behaviour, and override semantics |
| [Trait catalogue](./docs/components/trait-catalogue.md) | Complete reference of every trait, its effects, and its exclusions |
| [Data model](./docs/data-model.md) | Trait document schema and field vocabulary |
| [Behaviour](./docs/behaviour/trait-scoping.md) | Trait scoping, eligibility, exclusions, and modifiers |
| [Change guide](./docs/change-guide.md) | Safe modification procedures for each content area |
| [Invariants](./docs/invariants.md) | Properties that must remain true |
| [Open questions](./docs/ambiguities-and-open-questions.md) | Known defects, discrepancies, and unverifiable behaviour |

## ❓ FAQ

See the [Frequently Asked Questions](./docs/faq.md) for responses to frequently raised inquiries.

## 🩺 Troubleshooting

See the [Troubleshooting Guide](./docs/troubleshooting.md) for diagnostic procedures and resolutions to recurring problems.

## 🤝 Contributing

You are welcome to submit any suggestion, feedback, or modification to this project.

When doing so, please:
- Maintain cross-platform compatibility
- Submit focused pull requests that conform to the existing code style
- Maintain your branch synchronised with `master`
- Revise the documentation when functionality changes
- Raise a new [issue](https://github.com/hmlendea/stellaris-ui-character-traits/issues) for problems or suggestions

See the [Contributing Guidelines](./CONTRIBUTING.md) for details on how to report issues, suggest enhancements, and submit changes.

## 📜 Code of Conduct

See the [Code of Conduct](./CODE_OF_CONDUCT.md) for the standards of conduct expected in all project spaces.

## 🔗 Related Projects

- [Universum Infinitum - Deposit Blockers](https://github.com/hmlendea/stellaris-ui-deposit-blockers): Adds seven planet deposit blockers and one matching society technology to clear each of them.
- [Universum Infinitum - Flags](https://github.com/hmlendea/stellaris-ui-flags): Adds hundreds of new flag designs matching the vanilla flag style.
- [Universum Infinitum - Galaxy Sizes](https://github.com/hmlendea/stellaris-ui-galaxy-sizes): Adds six galaxy sizes ranging from 100 to 2,000 stars, with scaled generation defaults.
- [Universum Infinitum - Name Lists](https://github.com/hmlendea/stellaris-ui-name-lists): Provides numerous detailed name lists, including the Human - Extended variant.
- [Universum Infinitum - Planet Modifiers](https://github.com/hmlendea/stellaris-ui-planet-modifiers): Adds eight new planet modifiers with their own icons and English localisation.
- [Universum Infinitum - Prescripted Countries](https://github.com/hmlendea/stellaris-ui-prescripted-countries): Adds prescripted countries for players to select or for the AI to use.
- [Universum Infinitum - Species Names](https://github.com/hmlendea/stellaris-ui-species-names): Adds hundreds of new species names to the game.
- [Universum Infinitum - Species Traits](https://github.com/hmlendea/stellaris-ui-species-traits): Adds 58 custom species traits and extends several trait families with additional tiers.
- [Universum Infinitum - Star Names](https://github.com/hmlendea/stellaris-ui-star-names): Adds thousands of new names for stars, nebulas, asteroids, and black holes.

## 🔒 Security

Universum Infinitum - Character Traits distributes only local game definitions, localisation, and image assets.

For information on reporting security vulnerabilities, see the [Security Policy](./SECURITY.md).

## 💬 Support

For support, please [open an issue](https://github.com/hmlendea/stellaris-ui-character-traits/issues).

## 💝 Project Engagement

Discovered a problem with Universum Infinitum - Character Traits or have a suggestion for it? [Open an issue](https://github.com/hmlendea/stellaris-ui-character-traits/issues)!

If you find this project useful, consider [funding it](https://hmlendea.go.ro/fund.html) or starring ⭐️ it on GitHub, or giving it a thumbs up and adding it as a favourite on the [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2048878128)!

[![Donate](https://raw.githubusercontent.com/hmlendea/readme-assets/master/donate_generic.png)](https://hmlendea.go.ro/fund.html)

## 📄 License

This project is being distributed under the `GNU General Public License v3.0 or later`.
See [LICENSE](./LICENSE) for additional information.
