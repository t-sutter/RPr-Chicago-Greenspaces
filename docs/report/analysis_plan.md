# Reproduction of Middlebury College's GIS Green Space Access in Chicago Lab

### Author

- Tate Sutter\*, tsutter@middlebury.edu, @t-sutter, Middlebury College

\* Corresponding author and creator

### Abstract

This study is a *replication* of:

> [Week 07 Lab: Urban Environmental Justice of Green Space Access in Chicago](https://github.com/t-sutter/RPr-Chicago-Greenspaces/blob/main/docs/report/originalStudy.pdf), Human Geography with GIS, Middlebury College

The study replicates the lab *Urban Environmental Justice of Green Space Access in Chicago* within a Python coding language environment. The study reproduces an analysis of inhabitants' access to green space in Chicago. The original lab was performed in QGIS. The reproduction compares the geospatial tools of QGIS and the GeoPandas Python package and transitions the analysis from a graphical user interface (GUI) system to script based system. 

### Study metadata

- `Key words`: Urban Geography, Green Spaces, Chicago, Reproducibility, Open Science, Geospatial Python.
- `Subject`: Human Geography
- `Date created`: December 1, 2023. 
- `Date modified`: December 18, 2023.
- `Spatial Coverage`: Chicago, Illinois.
- `Spatial Resolution`: Census Block and Tract.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: 2010
- `Temporal Resolution`: This study does not address change over time. 

#### Original study spatio-temporal metadata

- `Spatial Coverage`: Chicago, Illinois.
- `Spatial Resolution`: Census Block and Tract.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: 2010
- `Temporal Resolution`: This study does not address change over time. 

## Study design

This study is a reproduction of an [observational lab](https://github.com/t-sutter/RPr-Chicago-Greenspaces/blob/main/docs/report/originalStudy.pdf) from the Middlebury College Department of Geography course Human Geography with GIS. The lab sought to replicate [*Wolch, Wilson and Fehrenbach's (2005)*](https://doi.org/10.2747/0272-3638.26.1.4) measurements of park space by racial groups at the census tract level in Los Angeles. The original lab deviates from *Wolch, Wilson, and Fehrenbach* initial study design. Chicago becomes the study extent. Access is grouped by racial majority group (>60%) per Census tract instead of varying racial breakdowns. The reproduction study contributes to the growing body of research working to improve [reproducibility](https://doi.org/10.1080/24694452.2020.1806029) and [replicability](https://doi.org/10.1080/24694452.2020.1806026) within GIS as a discipline and GIScience. The impermanence of public access to data, changes to GIS softwares, and lack of documentation of computational environments increases the difficulty to reproduce or replicate existing studies. 

In this reproduction study, I hypothesize that the original analysis performed in QGIS can be reproduced within a Python environment utilizing the GeoPandas geoprocessing package. To check my hypothesis, I compare the original results table with the one created in the reproduction.

## Materials and procedure

### Computational environment

The reproduction study is run on a 2020 MacBook Pro with a 2.3 GHz Quad-Core Intel Core i7 processor and 16 GB 3733 MHz LPDDR4X. The computer employs the Sonoma 14.2 macOS operating system. The analysis is performed in JupyterLab 4.0.8 and utilizes Python 3.

The most important packages used are geopandas and pandas. The reproduction is built upon the two.

```
# Import modules, define directories
from pyhere import here
import geopandas as gpd
import pandas as pd
import folium as fm
import matplotlib as mpl

# You can define your own shortcuts for file paths:
path = {
    "dscr": here("data", "scratch"),
    "drpub": here("data", "raw", "public"),
    "drpriv": here("data", "raw", "private"),
    "ddpub": here("data", "derived", "public"),
    "ddpriv": here("data", "derived", "private"),
    "rfig": here("results", "figures"),
    "roth": here("results", "other"),
    "rtab": here("results", "tables"),
    "dmet": here("data", "metadata")
} 
```

### Data and variables

The original lab and the reproduction study use the same data. All of the data is secondary data gathered from existing data sources. 

Each of the next subsections describes one data source.

#### Census Tracts 2010

**Standard Metadata**

- `Abstract`: Census tracts are the most commonly used of the US Census units of data aggregation. Census tracts average 4,000 inhabitants but can range between 1,200 and 8,000. 
- `Spatial Coverage`: City of Chicago.
- `Spatial Resolution`: Census Tracts.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: 2010. Estimate of April 1st.
- `Temporal Resolution`: The Census 2010 asked households to best answer the questions to be most accurate as of the 1st of April.
- `Lineage`: Data comes from the Census through Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 13.0 [Database]. Minneapolis: University of Minnesota. 2018. Data can be accessed at https://doi.org/10.18128/D050.V12.0. 
- `Distribution`: Data can be accessed through Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 13.0 [Database]. Minneapolis: University of Minnesota. 2018. Data can be accessed at https://doi.org/10.18128/D050.V12.0. 
- `Constraints`: The data is free to access for registered users. 
- `Data Quality`: The data is published as the official representation of demographics within the United States. The Census notes that there is a level of uncertainty inherent to the data.
- `Variables`: For each variable, enter the following information. If you have two or more variables per data source, you may want to present this information in table form (shown below)
  - `Label`: variable name as used in the data or code
  - `Alias`: intuitive natural language name
  - `Definition`: Short description or definition of the variable. Include measurement units in description.
  - `Type`: data type, e.g. character string, integer, real
  - `Accuracy`: e.g. uncertainty of measurements
  - `Domain`: Range (Maximum and Minimum) of numerical data, or codes or categories of nominal data, or reference to a standard codebook
  - `Missing Data Value(s)`: Values used to represent missing data and frequency of missing data observations
  - `Missing Data Frequency`: Frequency of missing data observations
  
  - N/A denotes not applicable. 

| Label | Alias | Definition | Type | Accuracy | Domain | Missing Data Value(s) | Missing Data Frequency |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| fid | Feature ID.| The fid is a feature ID for each row. This comes in as part of the imported .shapefile. | float64
 | N/A | 1-787 | N/A | N/A |
| STATEFP10 | State Identification Code. | This code is unique for Illinois. | object | N/A | N/A | N/A | N/A |
| COUNTYFP10 | County Identification Code. | This code is unique for a county within a state. | object | N/A | N/A | N/A | N/A |
| TRACTCE10 | Tract Identification Code. | This code is unique for a tract within a county. | object | N/A | N/A | N/A | N/A |
| GEOID10 | Geographic ID | GEOID10 is a unique identifier for the tract in the 2010 Census. It is a combination of the prior three codes.  | object | Each code is unique by tract. | N/A | N/A | N/A |
| NAME10 | Census tract name. | The tract name refers to the TRACTCE10. | object | N/A | N/A | N/A | N/A |
| NAMELSAD10 | Census tract name. | The tract name refers to the TRACTCE10 with a more descriptive title. | object | N/A | N/A | N/A | N/A |
| GISJOIN | GISJOIN | Same as the GEOID10 with a ‘G’ before each value. It is used to group smaller geometries into the tract scale. | object | N/A | N/A | N/A | N/A |
| PopTotal | Population Total | Total population in the tract. | float64 | N/A | 16498.0 | N/A | N/A |
| Latinx | Latinx | Latinx population in the tract. | float64 | N/A | 6699.0 | N/A | N/A |
| MedHouseVa | Median House Value | Median House Value in the tract. | float64 | N/A | 820200.0 | N/A | N/A |
| MedGrossRe | Median Gross Rent | Median gross rent in the tract |float64 | N/A | 1818.0 | N/A | N/A | N/A |
| pctWhite | Percent white | Percent of tract that identifies as non-Hispanic white. | float64 | 91.3 | N/A | N/A | N/A |
| pctBlack | Percent Black | Percent of tract that identifies as non-Hispanic Black. | float64 | 99.2 | N/A | N/A | N/A |
| pctLatinx | Percent Latinx | Percent of tract that identifies as Hispanic or Latino . | float64 | 98.7 | N/A | N/A | N/A |
| pctAsian | Percent Asian | Percent of tract that identifies as non-Hispanic Asian. | float64 | 88.8
 | N/A | N/A | N/A |
| majorGroup | Racial Majority Group | Racial group which makes up more then 60% of a tracts population. If no group makes up 60%, the tract is assigned ‘Mixed’. | object | ‘Black’, ‘White’, ‘Latinx’, ‘Asian’, ‘Mixed’ | N/A | N/A | N/A |
| cbdDist | Distance from the Central Business District | The variable measures the distance from Chicago’s central business district. It is calculated in a GIS. It appears to be in km. | float64 | 25.687 | N/A | N/A | N/A |
| cbdDir | Direction from the Central Business District | The direction of tracts from the central business district. It is calculated in a GIS. It appears to be in degrees. | float64 | 356.358 | N/A | N/A | N/A |
| geometry | Geometry | The variable denotes the geometries of each Census tract. | geometry | N/A | N/A | N/A | N/A |




#### Census Blocks 2010

**Standard Metadata**

- `Abstract`: Census blocks are the smallest unit of data released by the Census. Blocks are self-contained, bounded by visible (roads, railroads) and nonvisible (political boundaries, property lines) features, and do not have a population limit. 
- `Spatial Coverage`: City limits of Chicago, Illinois.
- `Spatial Resolution`: Census Block.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: 2010.
- `Temporal Resolution`: The Census 2010 asked households to best answer the questions to be most accurate as of the 1st of April.
- `Lineage`: Data comes from the Census through Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 13.0 [Database]. Minneapolis: University of Minnesota. 2018. Data can be accessed at https://doi.org/10.18128/D050.V12.0.
- `Distribution`: Data can be accessed through Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 13.0 [Database]. Minneapolis: University of Minnesota. 2018. Data can be accessed at https://doi.org/10.18128/D050.V12.0. 
- `Constraints`: The data is free to access for registered users.
- `Data Quality`: The data is published as the official representation of demographics within the United States. The Census notes that there is a level of uncertainty inherent to the data.
- `Variables`: For each variable, enter the following information. If you have two or more variables per data source, you may want to present this information in table form (shown below)
  - `Label`: variable name as used in the data or code
  - `Alias`: intuitive natural language name
  - `Definition`: Short description or definition of the variable. Include measurement units in description.
  - `Type`: data type, e.g. character string, integer, real
  - `Accuracy`: e.g. uncertainty of measurements
  - `Domain`: Expected range of Maximum and Minimum of numerical data, or codes or categories of nominal data, or reference to a standard codebook
  - `Missing Data Value(s)`: Values used to represent missing data and frequency of missing data observations
  - `Missing Data Frequency`: Frequency of missing data observations: not yet known for data to be collected

 - N/A denotes not applicable.

| Label | Alias | Definition | Type | Accuracy | Domain | Missing Data Value(s) | Missing Data Frequency |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| STATEFP10 | State Identification Code. | This code is unique for Illinois. | object | N/A | N/A | N/A | N/A |
| COUNTYFP10 | County Identification Code. | This code is unique for a county within a state. | object | N/A | N/A | N/A | N/A |
| TRACTCE10 | Tract Identification Code. | This code is unique for a tract within a county. | object | N/A | N/A | N/A | N/A |
| BLOCKCE10 | Block Identification Code. | This code is unique for a block within a tract. | object | N/A | N/A | N/A | N/A |
| GEOID10 | Geographic ID | GEOID10 is a unique identifier for the block in the 2010 Census. It is a combination of the prior four codes. | object | Each code is unique by block. | N/A | N/A | N/A |
| NAME10 | Census block name. | The block name refers to the BLOCKCE10 value. | object | N/A | N/A | N/A | N/A |
| MTFCC10 | N/A | N/A | object | N/A | ‘G5040’ | N/A | N/A |
| UR10 | N/A | N/A | object | N/A | ‘U’ | N/A | N/A |
| UACE10 | N/A | N/A | object | N/A | ‘16264’ | N/A | N/A |
| UATYP10 | N/A | N/A | object | N/A | ‘U’ | N/A | N/A |
| FUNCSTAT10 | N/A | N/A | object | N/A | ‘S’ | N/A | N/A |
| ALAND10 | Area Land within Block | Area of land within Census block. The units are unclear. | int64 | N/A | 4733129 | N/A | N/A |
| AWATER10 | Area Water within Block | Area of water within Census block. The units are unclear. | int64 | N/A | 4733129 | N/A | N/A |
| GEO.id | Geometry ID | The values are a the same as ‘GEOID10’ with ‘1000000US’ added to the beginning. (‘1000000US’+’GEOID10’) | object | N/A | N/A | N/A | N/A |
| GEO.displa | Census block name. | The tract name refers to the block with a descriptive title. | object | N/A | N/A | N/A | N/A |
| D001 | Total population | Total population of block. | int64 | N/A | 9798 | N/A | N/A |
| D002 | Hispanic or Latino | Hispanic or Latino population of a block.  | int64 | N/A | 1159 | N/A | N/A |
| D003 | Not Hispanic or Latino | Non-Hispanic or non-Latino population of a block. | int64 | N/A | 8639 | N/A | N/A |
| D004 | Not Hispanic or Latino: Population of one race | Non-Hispanic or non-Latino population of a block. | int64 | N/A | 8627 | N/A | N/A |
| D005 | Not Hispanic or Latino: Population of one race: White alone | The non-Hispanic or non-Latino white alone population of a block. | int64 | N/A | 1410 | N/A | N/A |
| D006 | Not Hispanic or Latino: Population of one race: Black or African American alone | The non-Hispanic or non-Latino Black or African American alone population of a block. | int64 | N/A | 7199 | N/A | N/A |
| D007| Not Hispanic or Latino: Population of one race: American Indian and Alaska Native alone | The non-Hispanic or non-Latino American Indian and Alaska Native alone population of a block. | int64 | N/A | 17 | N/A | N/A |
| D008| Not Hispanic or Latino: Population of one race: Asian alone | The non-Hispanic or non-Latino Asian alone population of a block. | int64 | N/A | 666 | N/A | N/A |
| D009 | Not Hispanic or Latino: Population of one race: Native Hawaiian and Other Pacific Islander alone | The non-Hispanic or non-Latino Native Hawaiian and Other Pacific Islander alone population of a block. | int64 | N/A | 12 | N/A | N/A |
| D010 | Not Hispanic or Latino: Population of one race: Some Other Race alone | The non-Hispanic or non-Latino Some Other Race alone population of a block | int64 | N/A | 32 | N/A | N/A |
| geometry | Geometry | The variable denotes the geometries of each Census block. | geometry | N/A | N/A | N/A | N/A |

#### Forests

**Standard Metadata**

- `Abstract`: Forest preserves within Chicago, Illinois.
- `Spatial Coverage`: City limits of Chicago, Illinois.
- `Spatial Resolution`: Meters.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: Unknown.
- `Temporal Resolution`: Unknown. 
- `Lineage`: Government Agency. Details unclear.
- `Distribution`: Unknown. 
- `Constraints`: Unknown.
- `Data Quality`: Unknown.
- `Variables`: For each variable, enter the following information. If you have two or more variables per data source, you may want to present this information in table form (shown below)
  - `Label`: variable name as used in the data or code
  - `Alias`: intuitive natural language name
  - `Definition`: Short description or definition of the variable. Include measurement units in description.
  - `Type`: data type, e.g. character string, integer, real
  - `Accuracy`: e.g. uncertainty of measurements
  - `Domain`: Expected range of Maximum and Minimum of numerical data, or codes or categories of nominal data, or reference to a standard codebook
  - `Missing Data Value(s)`: Values used to represent missing data and frequency of missing data observations
  - `Missing Data Frequency`: Frequency of missing data observations: not yet known for data to be collected

 - N/A denotes not applicable.

| Label | Alias | Definition | Type | Accuracy | Domain | Missing Data Value(s) | Missing Data Frequency |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| NAME | Name of Forest Preserve District of Cook County | These lands are part of the [Forest Preserve District of Cook County](https://fpdcc.com/) within the city of Chicago. | object | N/A | N/A | N/A | N/A |
| geometry | Geometry | The variable denotes the geometries of each forest preserves. | geometry | N/A | N/A | N/A | N/A |

#### Parks

**Standard Metadata**

- `Abstract`: Parks within Chicago, Illinois.
- `Spatial Coverage`: City limits of Chicago, Illinois.
- `Spatial Resolution`: Meters.
- `Spatial Reference System`: EPSG:6454
- `Temporal Coverage`: Unknown.
- `Temporal Resolution`: Unknown. 
- `Lineage`: Government Agency. Details unclear.
- `Distribution`: Unknown. 
- `Constraints`: Unknown.
- `Data Quality`: Unknown.
- `Variables`: For each variable, enter the following information. If you have two or more variables per data source, you may want to present this information in table form (shown below)
  - `Label`: variable name as used in the data or code
  - `Alias`: intuitive natural language name
  - `Definition`: Short description or definition of the variable. Include measurement units in description.
  - `Type`: data type, e.g. character string, integer, real
  - `Accuracy`: e.g. uncertainty of measurements
  - `Domain`: Expected range of Maximum and Minimum of numerical data, or codes or categories of nominal data, or reference to a standard codebook
  - `Missing Data Value(s)`: Values used to represent missing data and frequency of missing data observations
  - `Missing Data Frequency`: Frequency of missing data observations: not yet known for data to be collected

 - N/A denotes not applicable.

| Label | Alias | Definition | Type | Accuracy | Domain | Missing Data Value(s) | Missing Data Frequency |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| parkName | Park Name. | Name of Chicago park. | object | N/A | N/A | N/A | N/A |
| geometry | Geometry | The variable denotes the geometries of each park. | geometry | N/A | N/A | N/A | N/A |

### Prior observations  

At the time of this study pre-registration, the author has prior knowledge of the geography of the study region with regards to the replication phenomena to be studied. The author performed the original QGIS lab before this analysis. The reproduction follows the same workflow as the original lab. Mistakenly, the preregistration was written after the analysis was performed.

For all sources of data, the author had interacted with the data while running the QGIS lab. Deeper investigations involving data provenance had not occurred.

### Bias and threats to validity

Edge effects pose the greatest threats to validity of the original lab and reproduction study. Green spaces outside the city limits of Chicago are not considered. Chicago denizens living near the city limits may access green spaces outside of Chicago that are not included in parks.shp or forest.shp files. Including green spaces within a 0.25 mile distance from the city limits of Chicago could account for edge effects.

The initial lab design works to minimize occurrences of the modifiable areal unit problem (MAUP). Access is calculated at the Census’s smallest unit size, blocks. Employing blocks to calculate access and population measures forms a more accurate model of access to green spaces within Chicago. If tracts or block groups were used as the analysis’s base unit, the units could have contributed to the homogenization of Chicago’s heterogeneous housing landscape. 

The original lab and the reproduction do not account for spatial heterogeneity. Ignoring the reality of transportation infrastructure, private property, and other barriers to mobility, the analyses assume Chicago is an isotropic plane. Incorporating measures of mobility would improve and complicate the analyses. The simplification of Chicago’s geography decreases the validity of the results while still providing informative results. 

### Data transformations

Two data transformations are performed. Green Spaces are created by a union of Parks and Forest. The union is simplified into a single multipart polygon. There are numerous ways to measure green spaces; however, this approach was decided in the original study. Secondly, the tracts data is simplified and dissolved into ‘tractsMaj’. Tracts are grouped by their ‘majorGroup’ to aggregate population data into the five ‘majorGroup’ values. 

### Analysis

The analysis follows the workflow within the [lab results](https://github.com/t-sutter/RPr-Chicago-Greenspaces/blob/main/docs/report/labResults.pdf). Spatial joins, buffers, dissolves, and centroids performed. Any variations or important instances are noted within the code. The code is heavily commented to improve readability.

## Results

The results are presented in a table and saved as a .csv file. The original lab’s results are loaded into the script to compare with the reproduction’s results. 

## Discussion

I will condense and share the results of the analysis in the discussion.

I will discuss the success of the hypothesis and situate in larger conversations of reproducibility in GIS and accounting geographic threats to validity. 

## Integrity Statement

No other pre-registration exists for this study; however, the pre-registration was written after the reproduction had begun. The unorthodox order should not impact the results of the study. The reproduction followed the original study’s workflow which was created before the analysis was run. 

## Acknowledgements

This reproduction was completed for the Middlebury College Department of Geography course GEOG 361: Open GIScience in Fall 2023. The course was taught by Professor Joseph Holler, PhD.

This report is based upon the template for Reproducible and Replicable Research in Human-Environment and Geographical Sciences, DOI:[10.17605/OSF.IO/W29MQ](https://doi.org/10.17605/OSF.IO/W29MQ)

## References

Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. National Historical Geographic Information System: Version 13.0 [dataset]. Minneapolis, MN: IPUMS, 2018. https://doi.org/10.18128/D050.V13.0 

Tullis, Jason A., and Bandana Kar. “Where Is the Provenance? Ethical Replicability and Reproducibility in GIScience and Its Critical Applications.” Annals of the American Association of Geographers 111, no. 5 (July 29, 2021): 1318–28. https://doi.org/10.1080/24694452.2020.1806029.

Wilson, John P., Kevin Butler, Song Gao, Yingjie Hu, Wenwen Li, and Dawn J. Wright. “A Five-Star Guide for Achieving Replicability and Reproducibility When Working with GIS Software and Algorithms.” Annals of the American Association of Geographers 111, no. 5 (July 29, 2021): 1311–17. https://doi.org/10.1080/24694452.2020.1806026.
