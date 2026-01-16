# Changelog

## s01162026 — System Build (2026-01-16)

### Overview
`s01162026` marks the completion of a full PalisadeOS system build. This release focuses on structural correctness, cross-architecture parity, and deterministic boot and recovery behavior. The project remains under development; this build is considered finished and frozen.

### Added
- Boot Options environment for:
  - ARM64
  - x86_64
- Recovery environment with GUI and input handling for:
  - ARM64
  - x86_64
- Architecture-specific linker scripts for ARM64 and x86_64
- Deterministic, freestanding build pipelines compatible with Termux
- Explicit stack protection handlers for x86_64 freestanding binaries

### Changed
- Enforced single-entry execution model using `_start` across all boot and recovery binaries
- Normalized init order between ARM64 and x86_64 implementations
- Removed duplicate kernel directory; `/NeoKern` is now the sole kernel tree
- Centralized control flow in entry files; GUI and trigger code are library-only

### Fixed
- Eliminated duplicate `main()` symbol linker errors
- Resolved architecture mismatches between object files and linker scripts
- Prevented host toolchain leakage (gcc/host libc) in cross builds
- Corrected recovery input handling to be state-driven and deterministic

### Removed
- Redundant kernel implementation
- Experimental or unused boot paths that violated entry discipline
- Implicit control-flow jumps inside non-entry components

### Notes
- This build prioritizes reliability, debuggability, and correctness over new features
- No new kernel features were introduced intentionally
- Future builds will build on this foundation without altering the established boot and recovery contracts
