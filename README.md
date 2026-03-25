# xarrera

Schema validation for Xarray

[![CI](https://github.com/javgat/xarrera/actions/workflows/main.yaml/badge.svg)](https://github.com/javgat/xarrera/actions/workflows/main.yaml)
[![codecov](https://codecov.io/github/javgat/xarrera/graph/badge.svg?token=AZ7L4NMLK1)](https://codecov.io/github/javgat/xarrera)
[![MIT License](https://img.shields.io/badge/License-MIT-informational.svg)](https://opensource.org/licenses/MIT)

## Installation

Install xarrera from PyPI:

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

## Usage

xarrera's API is modeled after [Pandera](https://pandera.readthedocs.io/en/stable/). The `DataArraySchema` and `DatasetSchema` objects both have `.validate()` methods.

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

This is a very early prototype of a library. Some key things are missing:

1. Exceptions: Pandera accumulates schema exceptions and reports them all at once. Currently, we are a eagerly raising `SchemaErrors` when the are found.

## License

All the code in this repository is [MIT](https://choosealicense.com/licenses/mit/) licensed.

## History

This project was originally developed at [CarbonPlan](https://carbonplan.org/).
It was transferred to the [xarray-contrib](https://github.com/xarray-contrib) organization in August 2022.

Due to the inactivity in xarray-contrib, it was forked to xarrera in March 2026.
