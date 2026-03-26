# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[//]: # "## [unreleased] - yyyy-mm-dd"

## [0.0.5] - 2026-03-26

### Added

- `DatasetSchema` validation now validates its coordinates (`CoordsSchema`).
  > Based on work by [@calgray](https://github.com/calgray) and [@garciampred](https://github.com/garciampred)
- Added dimension shape consistency validation across data variables and coordinates in `DatasetSchema`,
  and between `dims` and `shape` in `DataArraySchema`.
- Added support for Python 3.13.

## [0.0.4] - 2026-03-25

> **Note:** This release includes improvements originally developed in the upstream
> [`xarray-schema`](https://github.com/xarray-contrib/xarray-schema) project
> between version 0.0.3 and its main branch. `xarrera`'s contributions are the `DTypeSchema`
> change, the `pkg_resources` fix and the change in the supported Python versions.

### Added

- Complete JSON serialization/deserialization (methods `to_json()` and `from_json()`,
  `_json_schema` attribute, improved `.json` property) for all schema classes.
- Now supporting Python 3.11 and 3.12.

### Changed

- `DTypeSchema` now supports all NumPy abstract dtypes (e.g., `np.number`, `np.character`,
  etc.) instead of only a limited subset.

### Fixed

- Removed deprecated `pkg_resources` dependency to avoid errors with recent setuptools versions.
- Corrected validation in `ChunksSchema` when chunks are expected but the array is not chunked.
- `AttrSchema` correctly raises `SchemaError` instead of only instantiating it.
- Type hints and docstrings updated across several classes.

### Deleted

- Dropped support for Python 3.8

## [0.0.3] - 2022-04-06

Initial version that serves as the baseline for tracking changes in the change log since the fork
from `xarray-contrib/xarray-schema`.

[unreleased]: https://github.com/javgat/xarrera/compare/v0.0.5...HEAD
[0.0.5]: https://github.com/javgat/xarrera/compare/v0.0.4...v0.0.5"
[0.0.4]: https://github.com/javgat/xarrera/compare/0.0.3...v0.0.4"
[0.0.3]: https://github.com/javgat/xarrera/releases/tag/0.0.3
