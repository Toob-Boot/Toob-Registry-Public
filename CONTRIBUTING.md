# Contributing to Toob Registry

Thank you for your interest in contributing to the Toob hardware registry. This document describes the process for submitting new chips, drivers, cryptographic backends, and other packages.

## Before You Start

1. **Read the documentation.** Familiarize yourself with the [Toob-Boot](https://github.com/Toob-Boot/Toob-Loader) architecture and the package manifest format.
2. **Check existing packages.** Browse the repository to see the established patterns and quality standards.
3. **Open an issue first.** For new chip support or major driver additions, open a GitHub Issue to discuss the design before writing code.

## Package Structure

Every package lives in a category directory and contains a manifest file:

```
drivers/
  flash/
    my_new_driver/
      driver_manifest.json    ← required
      flash.c                 ← implementation
      flash.h                 ← optional header
```

### Manifest Requirements

- `name`: Unique, lowercase, no spaces (e.g. `my_spi_flash`)
- `version`: SemVer string (e.g. `1.0.0`)
- `author`: Your GitHub username or organization
- `description`: One-line summary of what the package provides

See existing manifests (e.g. `drivers/flash/esp_rom_spi/driver_manifest.json`) for reference.

## Pull Request Process

### 1. Fork & Branch

Fork this repository and create a feature branch:

```bash
git checkout -b add-stm32f4-chip
```

### 2. Add Your Package

Add your files in the correct category directory. Ensure your manifest validates against the registry schema.

### 3. Local Validation

If you have the Toob CLI installed, validate your changes locally:

```bash
toob registry validate
```

### 4. Submit the PR

Open a pull request against the `main` branch. The CI pipeline will automatically:

- Lint your C code with `clang-tidy`
- Validate your manifest schema
- Run a dry-run compatibility check against affected chips

### 5. Review & Staged Release

Your PR will be reviewed by the Toob core team. After approval:

1. **`dev`** — Your package is published in development stage (visible only to you).
2. **`staging`** — After code review, the package enters the compatibility matrix test cycle.
3. **`stable`** — Once all matrix tests pass, the package is promoted to stable and appears in the public registry index.

## Code Quality Standards

- **NASA Power of 10 (P10)** compliance is required for all safety-critical code (chips, crypto).
- **No dynamic memory allocation** in driver implementations.
- **All functions must have bounded execution time.**
- **Comments** should explain *why*, not *what*.
- Follow the coding style of existing packages in the same category.

## Security

- **Never include private keys, tokens, or credentials** in any file.
- **Cryptographic code** requires additional review by a core team member with crypto expertise.
- Packages with `chip_binding` restrictions are validated against the declared chip list.

## License

By contributing, you agree that your contributions will be licensed under the same license as this repository (see [LICENSE](LICENSE)).
