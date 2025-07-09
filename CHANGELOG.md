# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2025-07-15

### Added

- The country can be an ISO 3166-1 country code

### Changed

- The field `positionName` was renamed to `position`
- The description of `name` has changed to only apply to individuals (for organizations use `organization`)
- Either `name` or `organization` is required (before: `name` was required)

### Deprecated

### Removed

### Fixed

- Fixed the address in the example

## [0.1.1] - 2023-05-17

### Fixed

- The `value` in the Info Object had a wrong data type listed in the README.

## [0.1.0] - 2023-05-12

### Changed

- Alignment with recent changes to contacts in OGC API - Records
- The structure has fundamentally changed, please see the [0.1.0] for details.

## [0.0.1] - 2023-04-25

- First release based on OGC API - Records

[Unreleased]: <https://github.com/stac-extensions/contacts/compare/v1.0.0...HEAD>
[1.0.0]: <https://github.com/stac-extensions/contacts/compare/v0.1.1...v1.0.0>
[0.1.1]: <https://github.com/stac-extensions/contacts/compare/v0.1.0...v0.1.1>
[0.1.0]: <https://github.com/stac-extensions/contacts/compare/v0.0.1...v0.1.0>
[0.0.1]: <https://github.com/stac-extensions/contacts/tree/v0.0.1>
