© [Institute of Urban Water Management and Landscape Water Engineering](https://www.sww.tugraz.at), [Graz University of Technology](https://www.tugraz.at/home/) and [Markus Pichler](mailto:markus.pichler@tugraz.at)

# THIS IS A SNAPSHOT OF THE ORIGINAL README

Go to [GitLab](https://gitlab.com/markuspichler/swmm_api) to see the full source.

# Getting started

[![PyPI](https://img.shields.io/pypi/v/swmm-api.svg)](https://pypi.python.org/pypi/swmm-api)
[![pipeline status](https://gitlab.com/markuspichler/swmm_api/badges/master/pipeline.svg)](https://gitlab.com/markuspichler/swmm_api/-/commits/master)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![docs](https://img.shields.io/static/v1.svg?label=sphinx&message=documentation&color=blue)](https://markuspichler.gitlab.io/swmm_api)

[![PyPI - Downloads](https://img.shields.io/pypi/dd/swmm-api)](https://pypi.python.org/pypi/swmm-api)
[![PyPI - Downloads](https://img.shields.io/pypi/dw/swmm-api)](https://pypi.python.org/pypi/swmm-api)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/swmm-api)](https://pypi.python.org/pypi/swmm-api)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5862141.svg)](https://doi.org/10.5281/zenodo.5862141)


With this package you can read INP-files, manipulate them and write new ones.
You can run swmm within the python api.
And you can read the RPT- and OUT-files as a pandas DataFrame for further analysis.

This package is based on the command line SWMM syntax. ([see Appendix D in the SWMM User Manual 5.1](https://www.epa.gov/water-research/storm-water-management-model-swmm-version-51-users-manual))

## Install the package:
```bash
pip install swmm-api
```

## Alternative packages

R-language:
- **swmmr** / [github](https://github.com/dleutnant/swmmr) / [cran](https://cran.r-project.org/web/packages/swmmr/index.html)

python: 
- **swmmio** / [docs](https://swmmio.readthedocs.io/en/latest/) / [pypi](https://pypi.org/project/swmmio/) / [github](https://github.com/aerispaha/swmmio) / 
- **GisToSWMM5** / [github](https://github.com/AaltoUrbanWater/GisToSWMM5) / converting gis data to swmm model (also possible with swmm_api: `swmm_api.input_file.macro_snippets.gis_standard_import` and `swmm_api.input_file.macro_snippets.gis_export`)
- **swmmtoolbox** / [github](https://github.com/timcera/swmmtoolbox) / Thanks to _Tim Cera_ for this package! I used his package to understand the .out-files but completely rewrote the reading process in this package.
- **swmmnetwork** / [github](https://github.com/austinorr/swmmnetwork) / create graph network from swmm model (see `swmm_api.input_file.macros.inp_to_graph`)
- **SWMMOutputAPI** / [github](https://github.com/bemcdonnell/SWMMOutputAPI) / read the output file (see `swmm_api.output_file.out`)

## Read, manipulate and write the INP-File

### Read the INP-File

```python
from swmm_api.input_file.section_labels import TIMESERIES
from swmm_api import read_inp_file

inp = read_inp_file('inputfile.inp')  # type: swmm_api.SwmmInput

sec_timeseries = inp[TIMESERIES]  # type: swmm_api.input_file.helpers.InpSection
ts = inp[TIMESERIES]['regenseries'].frame  # type: pandas.Series
```

### Manipulate the INP-File

```python
from swmm_api import read_inp_file, SwmmInput
from swmm_api.input_file.section_labels import JUNCTIONS

inp = read_inp_file('inputfile.inp')  # type: swmm_api.SwmmInput
# or 
inp = SwmmInput.read_file('inputfile.inp')

inp[JUNCTIONS]['J01'].Elevation = 210
```

### Write the manipulated INP-File
```python
inp.write_file('new_inputfile.inp')
```

see [examples/inp_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/master/examples/inp_file_reader.ipynb)

see [examples/inp_file_structure.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/master/examples/inp_file_structure.ipynb)

see [examples/inp_file_macros.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/master/examples/inp_file_macros.ipynb)




## Run SWMM
```python
from swmm_api import swmm5_run
swmm5_run('new_inputfile.inp')
```

## Read the OUT-File
```python
from swmm_api import read_out_file
out = read_out_file('new_inputfile.out')   # type: swmm_api.SwmmOut
df = out.to_frame()  # type: pandas.DataFrame
```
see [examples/out_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/master/examples/out_file_reader.ipynb)


## Read the RPT-File
```python
from swmm_api import read_rpt_file
rpt = read_rpt_file('new_inputfile.rpt')  # type: swmm_api.SwmmReport
node_flooding_summary = rpt.node_flooding_summary  # type: pandas.DataFrame
```
see [examples/rpt_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/master/examples/rpt_file_reader.ipynb)

## GIS interactions

[`geopandas`](https://geopandas.org/) and its requirements (`Shapely`, `pyproj`, `Rtree`) must be installed! (not that easy on Windows)

```python
from swmm_api import SwmmInput
from swmm_api.input_file.sections.map_geodata import geo_section_converter
from swmm_api.input_file.macros.gis import write_geo_package, gpkg_to_swmm

inp = SwmmInput.read_file('inputfile.inp', custom_converter=geo_section_converter)

coords = inp.COORDINATES.geo_series  # type: geoandas.GeoSeries with points for all nodes
vertices = inp.VERTICES.geo_series  # type: geoandas.GeoSeries with lines for all links
polygons = inp.POLYGONS.geo_series  # type: geoandas.GeoSeries with polygons for all subcatchments

# create geopackage of all objects in inp file
write_geo_package(inp, gpkg_fn='geopackage.gpkg', driver='GPKG', label_sep='.', crs="EPSG:32633")

# read above written geopackage and convert it to inp-data
inp_new = gpkg_to_swmm('geopackage.gpkg', label_sep='.')
inp_new.write_file('new_inputfile.inp')
```

MORE INFORMATION COMING SOON

## Cite as

> *Pichler, Markus. (2022). swmm_api: API for reading, manipulating and running SWMM-Projects with python (0.2.0.16). Zenodo. https://doi.org/10.5281/zenodo.5862141*
