[![Tests](https://img.shields.io/github/actions/workflow/status/javgat/xarrera/main.yaml?style=for-the-badge&label=Tests)](https://github.com/javgat/xarrera/actions/workflows/main.yaml)
[![codecov](https://img.shields.io/codecov/c/github/javgat/xarrera?style=for-the-badge&logo=codecov&token=AZ7L4NMLK1)](https://codecov.io/github/javgat/xarrera)
[![PyPI version shields.io](https://img.shields.io/pypi/v/xarrera.svg?style=for-the-badge)](https://pypi.org/project/xarrera/)
[![PyPI license](https://img.shields.io/pypi/l/xarrera.svg?style=for-the-badge)](https://pypi.python.org/project/xarrera/)

<div align="center">
    <h3>Xarrera</h3>
    <p align="center">
        Schema validation for Xarray
    </p>
    <br />
    <a href="https://xarrera.readthedocs.io/en/latest/"><strong>Explore the docs »</strong></a>
</div>

## About the project

Xarrera is an open source project that provides an API for performing data-format validation on Xarray objects.

## Getting Started

### Prerequisites

- Python >= 3.9

### Installation

Install Xarrera from PyPI:

```shell
pip install xarrera
```

Conda:

```shell
conda install -c conda-forge xarrera
```

Or install it from source:

```shell
pip install git+https://github.com/javgat/xarrera
```

Another option is cloning the repository and installing the python
package and its dependencies by using:

```sh
git clone https://github.com/javgat/xarrera.git
cd xarrera
pip install -e .
```

## Usage

Xarrera's API is modeled after [Pandera](https://pandera.readthedocs.io/en/stable/). The `DataArraySchema`
and `DatasetSchema` objects both have `.validate()` methods.

The basic usage is as follows:

```python
import numpy as np
import xarray as xr
from xarrera import DataArraySchema, DatasetSchema, CoordsSchema

da = xr.DataArray(np.ones(4, dtype='i4'), dims=['x'], name='foo')

schema = DataArraySchema(dtype=np.integer, name='foo', shape=(4, ), dims=['x'])

schema.validate(da)
```

You can also use it to validate a `Dataset` like so:

```
schema_ds = DatasetSchema({'foo': schema})

schema_ds.validate(da.to_dataset())
```

Each component of the Xarray data model is implemented as a stand alone class:

```python
from xarrera.components import (
    DTypeSchema,
    DimsSchema,
    ShapeSchema,
    NameSchema,
    ChunksSchema,
    ArrayTypeSchema,
    AttrSchema,
    AttrsSchema
)

# example constructions
dtype_schema = DTypeSchema('i4')
dims_schema = DimsSchema(('x', 'y', None))  # None is used as a wildcard
shape_schema = ShapeSchema((5, 10, None))  # None is used as a wildcard
name_schema = NameSchema('foo')
chunk_schema = ChunksSchema({'x': None, 'y': -1})  # None is used as a wildcard, -1 is used as
ArrayTypeSchema = ArrayTypeSchema(np.ndarray)

# Example usage
dtype_schema.validate(da.dtype)

# Each object schema can be exported to JSON format
dtype_json = dtype_schema.to_json()
```

## Roadmap

This is a very early prototype of a library, based on a library with multiple forks with small additions.
The following key things to do are:

- [ ] Contact former `xarray-schema` developers, forkers, and issue writers about `xarrera`.
- [ ] ...
- [ ] String comparison using regex [xarray-schema~#9](https://github.com/xarray-contrib/xarray-schema/issues/9)
- [ ] Accumulate schema exceptions and report them all at once.
      Currently, we are a eagerly raising `SchemaErrors` when the are found.
- [ ] Improve SchemaError reported information.
- [ ] Extract schema from xarray objects [xarray-schema~#45](https://github.com/xarray-contrib/xarray-schema/issues/45)

### Versioning

Version changes and descriptions are stored in the <a href="./CHANGELOG.md">CHANGELOG</a>.
This file is updated each time a new version is released.

## Contributing

### Development Guide

1. **Install npm (required for pre-commit hooks)**

   Some pre-commit hooks (e.g., for formatting or linting) depend on Node.js and npm.
   You can install them via your system package manager, or download from [nodejs.org](https://nodejs.org) (npm is included).

   For example, on Debian/Ubuntu:

   ```sh
   sudo apt update
   sudo apt install nodejs npm
   ```

   If you use conda, you can also install it with:

   ```shell
   conda install -c conda-forge nodejs
   ```

2. **Install Pre-commit Hooks**

   Install the `pre-commit` hooks to automatically check code styling:

   ```sh
   pre-commit install
   ```

3. **Install Python Dependencies**

   Install the python package dependencies listed in the `requirements.txt` file, preferably in a python virtual enironment:

   ```sh
   pip install -r requirements.txt
   # or
   pip install -e .
   ```

### Testing

1. **Install test dependencies**

   Install de development dependencies with:

   ```sh
   pip install -r dev-requirements.txt
   # or
   pip install -e ".[dev]"
   ```

2. **Run the style check**

   Run the `mypy` style check with:

   ```sh
   mypy xarrera tests
   ```

3. **Run the tests**

   Run the tests with:

   ```sh
   pytest
   ```

   Generate the coverage with

   ```sh
   pytest --cov=./ --cov-report=xml --verbose
   ```

## License

All the code in this repository is [MIT](https://choosealicense.com/licenses/mit/) licensed.

## History

This project was originally developed at [CarbonPlan](https://carbonplan.org/).
It was transferred to the [xarray-contrib](https://github.com/xarray-contrib) organization in August 2022.

Due to the inactivity in xarray-contrib, it was forked to Xarrera in March 2026.

## Authors

- **Javier Gatón Herguedas** - _Maintainer_ - [:octocat: @javgat](https://github.com/javgat) - [gaton@goa.uva.es](mailto:gaton@goa.uva.es)
- **Callan Gray** - _Contributor_ - [:octocat: @calgray](https://github.com/calgray)
- **Joe Hamman** - [CarbonPlan](https://carbonplan.org) - _Initial Work_ - [:octocat: @jhamman](https://github.com/jhamman)
- **Anderson Banihirwe** - [CarbonPlan](https://carbonplan.org) - _Initial Work_ - [:octocat @andersy005](https://github.com/andersy005) - [anderson@carbonplan.org](mailto:anderson@carbonplan.org)
- **Peter A. I. Forsyth** - _Initial Work_ - [:octocat: @paiforsyth](https://github.com/paiforsyth)
- **Oriana Chegwidden** - [CarbonPlan](https://carbonplan.org) - _Initial Work_ - [:octocat: @orianac](https://github.com/orianac)
- **Raphael Hagen** - [CarbonPlan](https://carbonplan.org) - _Initial Work_ - [raphael@carbonplan.org](mailto:raphael@carbonplan.org)
