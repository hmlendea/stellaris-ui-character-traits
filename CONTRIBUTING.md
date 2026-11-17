[![Donate](https://img.shields.io/badge/-%E2%99%A5%20Donate-%23ff69b4)](https://hmlendea.go.ro/funding)

# Contributing to Universum Infinitum - Character Traits

This document covers the guidelines and processes for contributing to this project, including how to report issues, suggest enhancements, submit code changes, and follow project standards.

## 📑 Table of Contents

- [Contributing](#-contributing)
  - [Reporting Issues](#reporting-issues)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Code Contributions](#code-contributions)
    - [Prerequisites](#prerequisites)
    - [Development Setup](#development-setup)
    - [Making Changes](#making-changes)
    - [Pull Request Guidelines](#pull-request-guidelines)
  - [Documentation](#documentation)
- [Code of Conduct](#-code-of-conduct)
- [Security](#-security)
- [Donations](#-donations)
- [License](#-license)
- [Getting Assistance](#-getting-assistance)

## 🤝 Contributing

### Reporting Issues

- Search existing issues first.
- Use the issue templates if available.
- Provide clear reproduction steps.
- Include environment details.

### Suggesting Enhancements

- Check the existing discussions.
- Explain the use case and expected conduct.
- Consider the implementation complexity.

### Code Contributions

#### Prerequisites

- Stellaris installed for testing the mod
- A text editor with Clausewitz script and YAML support

#### Development Setup

```bash
# Clone the repository
git clone https://github.com/hmlendea/stellaris-ui-character-traits.git
cd stellaris-ui-character-traits

# Install dependencies
# No dependencies to install — the mod consists of static game definitions, localisation, and image assets
```

#### Making Changes

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes to the trait definitions in `ui-character-traits/common/traits/`, the localisation in `ui-character-traits/localisation/english/`, or the icons in `ui-character-traits/gfx/interface/icons/traits/`.
4. Verify the mod loads correctly by installing it locally and testing in Stellaris.
5. Commit with clear and descriptive messages.
6. Push to your fork.
7. Open a Pull Request.

#### Pull Request Guidelines

- Target the `master` branch.
- Keep PRs focused and atomic.
- Revise documentation if applicable.
- Include tests for any new functionality.
- Ensure the CI checks pass.

### Documentation

- Revise relevant docs for changes.
- Follow the documentation style guide.
- Preview changes locally if possible.

## 📜 Code of Conduct

This project follows the [Code of Conduct](./CODE_OF_CONDUCT.md).

## 🔒 Security

Report security vulnerabilities per the [Security Policy](./SECURITY.md).

## 💝 Donations

This project is developed and maintained during spare time. If you find it useful, consider [donating](https://hmlendea.go.ro/funding) and giving it a star ⭐️ on GitHub!

## 📄 License

By contributing, you agree that your contributions will be licensed under the GNU General Public License v3.0.

## ❓ Getting Assistance

- [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2048878128)
- [Paradox Mods](https://mods.paradoxplaza.com/mods/34606/Any)
- [Nexus Mods](https://nexusmods.com/stellaris/mods/90)
- [GitHub Issues](https://github.com/hmlendea/stellaris-ui-character-traits/issues)
- Check existing discussions and documentation first.
