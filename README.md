© [Institute of Urban Water Management and Landscape Water Engineering](https://www.sww.tugraz.at), [Graz University of Technology](https://www.tugraz.at/home/) and [Markus Pichler](mailto:markus.pichler@tugraz.at)

# THIS IS A SNAPSHOT OF THE ORIGINAL README

Go to [GitLab](https://gitlab.com/markuspichler/swmm_api) to see the full source.

# 💡 Getting started

[![PyPI](https://img.shields.io/pypi/v/swmm-api.svg)](https://pypi.python.org/pypi/swmm-api)
[![pipeline status](https://gitlab.com/markuspichler/swmm_api/badges/main/pipeline.svg)](https://gitlab.com/markuspichler/swmm_api/-/commits/main)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![docs](https://img.shields.io/static/v1.svg?label=sphinx&message=documentation&color=blue)](https://markuspichler.gitlab.io/swmm_api)

[![PyPI - Downloads](https://img.shields.io/pypi/dd/swmm-api)](https://pypi.python.org/pypi/swmm-api)
[![PyPI - Downloads](https://img.shields.io/pypi/dw/swmm-api)](https://pypi.python.org/pypi/swmm-api)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/swmm-api)](https://pypi.python.org/pypi/swmm-api)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7054804.svg)](https://doi.org/10.5281/zenodo.7054804)
[![Gitter](https://badges.gitter.im/MarkusPic/swmm-api.svg)](https://gitter.im/MarkusPic/swmm-api?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)


With this package you can read INP-files, manipulate them and write new ones.
You can run swmm within the python api.
And you can read the RPT- and OUT-files as a pandas DataFrame for further analysis.

This package is based on the command line SWMM syntax. ([see Appendix D in the SWMM User Manual 5.2](https://www.epa.gov/system/files/documents/2022-04/swmm-users-manual-version-5.2.pdf))

## Install the package
```bash
pip install swmm-api
```

... to install the package with all dependencies for macros use:

```bash
pip install swmm-api[macros]
```

... to install the package with all dependencies for GIS I/O use (for Linux or for Windows using python >= 3.10):

```bash
pip install swmm-api[gis]
```

... and to install the package with all dependencies for macros and GIS I/O use (for Linux or for Windows using python >= 3.10):

```bash
pip install swmm-api[full]
```

To add the GIS functionality to **Windows**, I recommend using python with [Mamba](https://github.com/conda-forge/miniforge#mambaforge)
 (or [miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/))
and run `mamba install geopandas` to install the GIS dependencies (see [GeoPandas](https://geopandas.org/en/stable/getting_started.html)).

Installing GeoPandas and its dependencies now work on Windows since python version >= 3.10.

## 📖 Documentation
[Link](https://markuspichler.gitlab.io/swmm_api) to the documentation of the api and some example jupyter notebook.

## Alternative packages

R-language:

- **swmmr** / [GitHub](https://github.com/dleutnant/swmmr) / [cran](https://cran.r-project.org/web/packages/swmmr/index.html)

python:

- **swmmio** / [docs](https://swmmio.readthedocs.io/en/latest/) / [pypi](https://pypi.org/project/swmmio/) / [GitHub](https://github.com/aerispaha/swmmio) / simular to this package but more high-level approach (= slower for specific tasks)
- **GisToSWMM5** / [GitHub](https://github.com/AaltoUrbanWater/GisToSWMM5) / converting gis data to swmm model (also possible with swmm_api: `swmm_api.input_file.macro_snippets.gis_standard_import` and `swmm_api.input_file.macro_snippets.gis_export`)
- **swmmtoolbox** / [GitHub](https://github.com/timcera/swmmtoolbox) / Thanks to _Tim Cera_ for this package! I used his package to understand the .out-files but completely rewrote the reading process in this package.
- **swmmnetwork** / [GitHub](https://github.com/austinorr/swmmnetwork) / create graph network from swmm model (see `swmm_api.input_file.macros.inp_to_graph`)
- **SWMMOutputAPI** / [GitHub](https://github.com/bemcdonnell/SWMMOutputAPI) / read the output file (see `swmm_api.output_file.out`) / (OpenWaterAnalytics)
- **swmm-pandas** / [pypi](https://pypi.org/project/swmm-pandas/) / equal functionalities to this package, but not feature complete
- **swmmout** / [pypi](https://pypi.org/project/swmmout/) / [docs](https://swmmout.readthedocs.io/en/latest/) / simular to `swmmtoolbox` and `SWMMOutputAPI`
- **swmmtonetcdf** / [pypi](https://pypi.org/project/swmmtonetcdf/) / [GitHub](https://github.com/cbuahin/swmmtonetcdf)
- **hymo** / [GitHub](https://github.com/lucashtnguyen/hymo) Input and Report Reader (Lucas Nguyen)
- **shmm** / [GitHub](https://github.com/lucashtnguyen/shmm) Input Reader (Lucas Nguyen)
- **swmmreport** / [GitHub](https://github.com/lucashtnguyen/swmmreport) Report Reader (Lucas Nguyen)
- **swmmdoodler** / [GitHub](https://github.com/Geosyntec/swmmdoodler)

## Other SWMM-related packages

python:

- **pyswmm** / [pypi](https://pypi.org/project/pyswmm/) / [GitHub](https://github.com/OpenWaterAnalytics/pyswmm) / RTC, etc. / based on swmm-toolkit (OpenWaterAnalytics)
- **swmm-toolkit** / [pypi](https://pypi.org/project/swmm-toolkit/) / [GitHub](https://github.com/OpenWaterAnalytics/swmm-python) / by Michael Tryby (OpenWaterAnalytics)
- **SWMM5** / [pypi](https://pypi.org/project/SWMM5/) / [GitHub](https://github.com/asselapathirana/swmm5-python) / simular approach to swmm-toolkit (by Assela Pathirana)
- **SWMM-xsections-shape-generator** / [pypi](https://pypi.org/project/SWMM-xsections-shape-generator/) / tool to generate custom shapes (by me)
- **SWMM_EA** / [pypi](https://pypi.org/project/SWMM5_EA/) / usage of genetic algorithms with SWMM (by Assela Pathirana)
- **OSTRICH-SWMM** / [GitHub](https://github.com/ubccr/ostrich-swmm) / OSTRICH optimization software toolkit with SWMM

## Read, manipulate and write the INP-File

### Read the INP-File

```python

from swmm_api import read_inp_file, SwmmInput

inp = read_inp_file('inputfile.inp')  # type: swmm_api.SwmmInput
# or 
inp = SwmmInput.read_file('inputfile.inp')
# or
inp = SwmmInput('inputfile.inp')

```

### Getting information

```python
from swmm_api.input_file.section_labels import TIMESERIES

# getting a specific section of the inp-file

sec_timeseries = inp[TIMESERIES]  # type: swmm_api.input_file.helpers.InpSection
# or
sec_timeseries = inp.TIMESERIES  # type: swmm_api.input_file.helpers.InpSection

# getting a specific timeseries as pandas.Series
ts = inp[TIMESERIES]['regenseries'].pandas  # type: pandas.Series
```

### Manipulate the INP-File

```python
from swmm_api.input_file.section_labels import JUNCTIONS

# setting the elevation of a specific node to a new value

inp[JUNCTIONS]['J01'].elevation = 210
# or
inp.JUNCTIONS['J01'].elevation = 210
# or
inp.JUNCTIONS['J01']['elevation'] = 210
```

### Write the manipulated INP-File
```python
inp.write_file('new_inputfile.inp')
```

see [examples/inp_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/main/examples/inp_file_reader.ipynb)

see [examples/inp_file_structure.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/main/examples/inp_file_structure.ipynb)

see [examples/inp_file_macros.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/main/examples/inp_file_macros.ipynb)




## Run SWMM

Run SWMM with a specified executable.

```python
from swmm_api import swmm5_run
swmm5_run('new_inputfile.inp', swmm_lib_path=r'C:\path\to\runswmm.exe')
```

Or run SWMM with [pyswmm](https://github.com/OpenWaterAnalytics/pyswmm). This would be platform independent as pyswmm is compiled for all platforms.
Additionally, you gain the advantage of a progress bar.

```python
from swmm_api import swmm5_run
swmm5_run('new_inputfile.inp', progress_size=100)
```

```
swmm5 C:\path\to\new_inputfile.inp:  77%|███████▋  | 77/100 [00:03<00:01, 22.36it/s, 2007-02-16 08:46:27]
```

## Read the OUT-File
```python
from swmm_api import read_out_file
out = read_out_file('new_inputfile.out')   # type: swmm_api.SwmmOut
df = out.to_frame()  # type: pandas.DataFrame
```
see [examples/out_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/main/examples/out_file_reader.ipynb)


## Read the RPT-File
```python
from swmm_api import read_rpt_file
rpt = read_rpt_file('new_inputfile.rpt')  # type: swmm_api.SwmmReport
node_flooding_summary = rpt.node_flooding_summary  # type: pandas.DataFrame
```
see [examples/rpt_file_reader.ipynb](https://gitlab.com/markuspichler/swmm_api/-/blob/main/examples/rpt_file_reader.ipynb)

## 🗺️ GIS interactions

[`geopandas`](https://geopandas.org/) and its requirements (`Shapely`, `pyproj`, `Rtree`) must be installed! (not that easy on Windows)

```python
from swmm_api import SwmmInput
from swmm_api.input_file.macros.gis import write_geo_package, gpkg_to_swmm

inp = SwmmInput.read_file('inputfile.inp')

coords = inp.COORDINATES.geo_series  # type: geoandas.GeoSeries with points for all nodes
vertices = inp.VERTICES.geo_series  # type: geoandas.GeoSeries with lines for all links
polygons = inp.POLYGONS.geo_series  # type: geoandas.GeoSeries with polygons for all subcatchments

# create geopackage of all objects in inp file
write_geo_package(inp, gpkg_fn='geopackage.gpkg', driver='GPKG', label_sep='.', crs="EPSG:32633")

# read above written geopackage and convert it to inp-data
inp_new = gpkg_to_swmm('geopackage.gpkg', label_sep='.')
inp_new.write_file('new_inputfile.inp')
```

# ⚠️ Be Aware!

> As python is case-sensitive this API is also case-sensitive, but SWMM is case-insensitive. 
> This is important for the naming of the objects. 
> For example, you could create a junction 'a' and 'A' with this API, but SWMM would only consider one and ignore the other.

---

This documentation will be continuously extended and enhanced. 
If you have any question, don't hesitate to write the author and email or create an issue on GitLab or GitHub.

MORE INFORMATION COMING SOON

# Cite as

> *Pichler, Markus. (2022). swmm_api: API for reading, manipulating and running SWMM-Projects with python (0.3). Zenodo. https://doi.org/10.5281/zenodo.7054804*

# Publications mentioning `swmm-api`

- Baumann, H., Ravn, N. H., & Schaum, A. (2022). Efficient hydrodynamic modelling of urban stormwater systems for real-time applications. *Modelling, 3(4)*, 464–480. https://doi.org/10.3390/modelling3040030
- Farina, A., Di Nardo, A., Gargano, R., & Greco, R. (2022). Assessing the environmental impact of combined sewer overflows through a parametric study. *EWaS5*, 8. https://doi.org/10.3390/environsciproc2022021008
- Schilling, J., & Tränckner, J. (2022). Generate_swmm_inp: An open-source qgis plugin to import and export model input files for swmm. *Water, 14(14)*, 2262. https://doi.org/10.3390/w14142262
- Zhang, Z., Tian, W., & Liao, Z. (2023). Towards coordinated and robust real-time control: A decentralized approach for combined sewer overflow and urban flooding reduction based on multi-agent reinforcement learning. *Water Research, 229*, 119498. https://doi.org/10.1016/j.watres.2022.119498

