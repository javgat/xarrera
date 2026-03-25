# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[//]: # "## [unreleased] - yyyy-mm-dd"

## [0.0.4] - 2026-03-25

### Changed

- `DTypeSchema` now supports all NumPy abstract dtypes (e.g., `np.number`, `np.character`,
  etc.) instead of only a limited subset.

### Fixed

- Removed deprecated `pkg_resources` dependency to avoid errors with recent setuptools versions.

## [0.0.3] - 2022-04-06

Initial version that serves as the baseline for tracking changes in the change log since the fork
from `xarray-contrib/xarray-schema`.

[unreleased]: https://github.com/javgat/xarrera/compare/v0.0.4...HEAD
[0.0.4]: https://github.com/javgat/xarrera/compare/0.0.3...v0.0.4"
[0.0.3]: https://github.com/javgat/xarrera/releases/tag/0.0.3
