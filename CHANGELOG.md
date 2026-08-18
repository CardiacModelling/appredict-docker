# Changelog

Notable changes to `appredict-docker` in each version.

This repository builds three layered images, each `FROM` the previous one:

- `appredict-chaste-libs`
- `appredict-no-emulators`
- `appredict-with-emulators`

They share a single version number and are released together.

## [2.1.0] - 2026-08-17

### Added

- Multi-architecture builds. All three images are now published for
  `linux/amd64` and `linux/arm64` using the shared `docker/github-builder`
  reusable workflow.

### Changed

- Version labels and the inter-image `FROM` pins advanced to `2.1.0`.

### Unchanged

- Chaste stays at `2024.1` and ApPredict `v2024.1`.
- The bundled CellML model set and the lookup table manifest are unchanged.

## [2.0.0] - 2024-09-10

### Added

- Build arguments for the ApPredict and Chaste versions and for the build
  processor count.
- GitHub Actions to build and publish the images.

### Changed

- Upgraded to ApPredict 2024.1 and Chaste 2024.1.
- Rebased the images on Debian bullseye.
- Version labels advanced to `2.0.0`.
- Updated the license.

## [1.0.0] - 2023-07-21

First release from the standalone repository — the ApPredict images were split
out of the AP-Nimbus umbrella repository.

### Changed

- Rebased the images on Debian buster and switched to Debian packages for the
  dependencies, which enabled the move to the CMake build system.
- ApPredict is now checked out by tag rather than by branch, so image builds are
  reproducible.
- Renamed the images to match the documentation.

### Removed

- The legacy `default.py.patch`, which was used to patch Chaste's hostconfig for
  SCons, rewrite config paths, point the build at the installed dependencies,
  and set VTK off and CVODE on.

### Fixed

- `ApPredict.sh`, the wrapper that runs the `ApPredict` binary with the
  arguments it was given, is now made executable in the image.

## Earlier milestones

The Python 2 based images predate this repository. Their last state is tagged
`last_python2` (2020-07-23) in the AP-Nimbus umbrella repository.

[2.1.0]: https://github.com/CardiacModelling/appredict-docker/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/CardiacModelling/appredict-docker/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/CardiacModelling/appredict-docker/releases/tag/v1.0.0
