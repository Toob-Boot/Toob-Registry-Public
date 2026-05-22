# Toob Registry

The official hardware registry for the [Toob-Boot](https://github.com/Toob-Boot) ecosystem.

This repository is a **read-only public mirror** of the production registry. It contains verified chip support packages, drivers, cryptographic backends, architecture ports, toolchain definitions, and RTOS integration hooks consumed by the [Toob CLI](https://github.com/Toob-Boot/Toob-CLI-Release).

## Contents

| Directory | Description |
|---|---|
| `arch/` | Architecture support (RISC-V, ARM Cortex-M, ...) |
| `chips/` | Chip support packages (startup, platform HAL, linker scripts) |
| `crypto/` | Cryptographic backends (Ed25519, SHA-256, Post-Quantum) |
| `drivers/` | Peripheral drivers (UART, Flash, WDT, RTC, Clock) |
| `integrations/` | RTOS integration hooks (Zephyr, ESP-IDF, Baremetal) |
| `soc/` | SoC vendor-specific headers and register maps |
| `toolchains/` | Cross-compiler definitions and download URLs |

## Usage

The Toob CLI syncs this registry automatically:

```bash
# Sync to latest stable registry version
toob registry sync

# Initialize a project for a specific chip
toob init --chip esp32c6

# Compile your project
toob compile
```

## Registry Index

The [`registry.json`](registry.json) file is the aggregated index of all packages. It is generated automatically and should not be edited manually.

The [`compatibility_matrix.json`](compatibility_matrix.json) tracks verified build combinations across the ecosystem.

## Contributing

Community contributions for new chips, drivers, and crypto backends are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

> **Important:** Pull requests submitted to this repository are validated and tested against the full compatibility matrix before being merged. Packages go through a staged review process (`dev` → `staging` → `stable`) to prevent supply-chain attacks.

## License

This project is licensed under the terms described in [LICENSE](LICENSE).
