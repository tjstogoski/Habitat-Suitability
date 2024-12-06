# Habitat-Suitability
Final project for Earth Analytics AY24.

## [Our changing climate is changing where key grassland species can live, and grassland management and restoration practices will need to take this into account.](https://www.frontiersin.org/articles/10.3389/fpls.2017.00730/full)

In this project, you will create a habitat suitability model for Sorghastrum nutans (or a plant species of your choice), a grass native to North America. [In the past 50 years, its range has moved northward](https://www.gbif.org/species/2704414). The model will be based on combining multiple data layers related to soil, topography, and climate. You will also demonstrate the coding skills covered in this class by creating a modular, reproducible workflow for the model.

## You will create a reproducible scientific workflow

Your workflow should:

1. **Define your study area:**  If you are using Sorghastrum nutans, you can download the [USFS National Grassland Units](https://data.fs.usda.gov/geodata/edw/edw_resources/shp/S_USA.NationalGrassland.zip) and select at least 2 as study sites.
2. **Fit a model:** For each grassland:
    1. **Download model variables** as raster layers covering your study area envelope, including:
        - At least one **soil** variable from the [POLARIS dataset](http://hydrology.cee.duke.edu/POLARIS/PROPERTIES/v1.0/)
        - Elevation from the SRTM (available from the [earthaccess API](https://github.com/nsidc/earthaccess/))
        - At least one **climate** variable from the [MACAv2 THREDDS data server](http://thredds.northwestknowledge.net:8080/thredds/reacch_climate_CMIP5_macav2_catalog2.html). Your project should compare two climate scenarios of your choice (e.g. different time periods, different emission scenarios). You can find a tutorial on how to access these climate data on [earthdatascience.org](https://www.earthdatascience.org/courses/use-data-open-source-python/hierarchical-data-formats-hdf/intro-to-MACAv2-cmip5-data/)
     2. **Calculate at least one derived **topographic** variable** (slope or aspect) to use in your model. You probably will wish to use the `xarray-spatial` library, which is available in the latest earth-analytics-python environment (but will need to be installed/updated if you are working on your own machine). Note that calculated slope may not be correct if you are using a CRS with units of *degrees*; you should re-project into a projected coordinate system with units of *meters*, such as the appropriate UTM Zone.
     3. **Harmonize your data** - make sure that the grids for each of your layers match up. Check out the [`ds.rio.reproject_match()` method](https://corteva.github.io/rioxarray/stable/examples/reproject_match.html#Reproject-Match) from `rioxarray`.
     4. **Build your model**. You can use any model you wish, so long as you explain your choice. However, if you are not sure what to do, we recommend building a **fuzzy logic** model (see below).
3. **Present your results** in at least one figure for each grassland/climate scenario combination.

## If you are unsure about which model to use, we recommend using a fuzzy logic model

To train a fuzzy logic habitat suitability model:

1. Research S. nutans, and find out what optimal values are for each variable you are using (e.g. soil pH, slope, and current climatological annual precipitation). 
2. For each **digital number** in each raster, assign a value from 0 to 1 for how close that grid square is to the optimum range (1=optimal, 0=incompatible). 
3. Combine your layers by multiplying them together. This will give you a single suitability number for each square. Check out this [article about raster math](https://www.earthdatascience.org/courses/use-data-open-source-python/intro-raster-data-python/raster-data-processing/subtract-rasters-in-python/) for more info.
4. Optionally, you may apply a threshold to make the most suitable areas pop on your map.

## You will be evaluated on your code AND how you present your results

I will use the following rubric:

| Description | Maximum Points |
| - | - |
| **GITHUB REPOSITORY** | 30  |
| Project is stored on GitHub | 3 |
| The repository has a README that introduces the project | 5 |
| The README also explains how to run the code | 5 |
| The README has a DOI badge at the top | 5 |
| The repository has a LICENSE | 2 |
| Repository is organized and there are not multiple versions of the same file in the repository | 5 |
| Repository files have machine and human-readable names | 5 |
| **CODE** | 120 |
| The code runs all the way through using the instructions from the README | 10 |
| The code follows the PEP-8 style standard | 10 |
| The code is well-documented with comments | 10 |
| The code uses functions and/or loops to be DRY and modular | 10 |
| Any functions have numpy-style docstrings | 10 |
| The code makes use of conditionals to cache data and/or computations, making efficient use of computing resources | 10 |
| The code contains a site map for the US National Grassland(s) used (1 ugrad, 2+ grad) | 10 |
| For each grassland (ugrad 1, grad 2+), the code downloads at least model variables as raster layers: soil, elevation, and climate (ugrad 1, grad 2 scenarios) | 10 |
| The code correctly calculates a derived topographic variable | 10 |
| The code harmonizes the raster data | 10 |
| For each climate scenario (1 ugrad, 2+ grad), the code builds a habitat suitability model | 10 |
| For each grassland/climate scenario combination, the code produces at least one (sub)figure displaying the results | 10 |
| Any unfinished components have detailed pseudocode or a flow diagram **explaining** how they could be finished in the future, and or a **complete** bug report explaining the problem | *up to 90 points, in place of other categories* |
| **WRITTEN ANALYSIS** | 50 |
| The notebook contains a project description | 10 |
| The notebook contains a researched site description | 10 |
| The notebook contains a data description and citation for each data source | 10 |
| The notebook contains a model description | 10 |
| The notebook contains a headline and description for each figure | 10 |


## Keep your eyes out for videos!

I won’t release a full demo of this, but you will have videos on writing pseudocode, accessing data sources, and any tricky problems that come up.