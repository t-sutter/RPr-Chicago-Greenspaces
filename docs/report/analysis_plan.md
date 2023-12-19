# Reproduction of Middlebury College's GIS Green Space Access in Chicago Lab

### Authors

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

This study is a reproduction of an [observational lab](https://github.com/t-sutter/RPr-Chicago-Greenspaces/blob/main/docs/report/originalStudy.pdf) from the Middlebury College Department of Geography course Human Geography with GIS. The lab sought to replicate [*Wolch, Wilson and Fehrenbach's (2005)*](https://doi.org/10.2747/0272-3638.26.1.4) measurements of park space by racial groups at the census tract level. The original lab deviates from *Wolch, Wilson, and Fehrenbach* initial study design. The reproduction study contributes to the growing body of research working to improve [reproducibility](https://doi.org/10.1080/24694452.2020.1806029) and [replicability](https://doi.org/10.1080/24694452.2020.1806026) within GIS as a discipline or GIScience. The impermanence of public access to data, changes to GIS softwares, and lack of documentation of computational environments increases the difficulty to reproduce or replicate existing studies. 

In this reproduction study, I hypothesize that the original analysis performed in QGIS can be reproduced within a Python environment utilizing the GeoPandas geoprocessing package. To check my hypothesis, I compare the original results table with the one created in the reproduction.

## Materials and procedure

### Computational environment

The reproduction study is run on a 2020 MacBook Pro with a 2.3 GHz Quad-Core Intel Core i7 processor and 16 GB 3733 MHz LPDDR4X. The computer employs the Sonoma 14.2 macOS operating system. The analysis is performed in JupyterLab 4.0.8 and utilizes Python 3.

The most important packages used are geopandas and pandas. The entire reproduction is built upon the two.

`# Import modules, define directories
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
}`

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
 | N/A | 1-787 | N/A | None |
| STATEFP10 | State Identification Code. | This code denotes that the tract is within Illinois. | object | N/A | N/A | N/A | N/A |
| COUNTYFP10 | County Identification Code. | This code denotes that the tract is within Cook County. | object | N/A | N/A | N/A | N/A |
| TRACTCE10 | Tract Identification Code. | This code is unique to the tract. | object | N/A | N/A | N/A | N/A |
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
| geometry | Geometry | The variable denotes the geometries of each census tract. | geometry | N/A | N/A | N/A | N/A |




#### Secondary data source1 name

**Standard Metadata**

- `Abstract`: Brief description of the data source
- `Spatial Coverage`: Specify the geographic extent of your study. This may be a place name and link to a feature in a gazetteer like GeoNames or OpenStreetMap, or a well known text (WKT) representation of a bounding box.
- `Spatial Resolution`: Specify the spatial resolution as a scale factor, description of the level of detail of each unit of observation (including administrative level of administrative areas), and/or or distance of a raster GRID size
- `Spatial Reference System`: Specify the geographic or projected coordinate system for the study
- `Temporal Coverage`: Specify the temporal extent of your study---i.e. the range of time represented by the data observations.
- `Temporal Resolution`: Specify the temporal resolution of your study---i.e. the duration of time for which each observation represents or the revisit period for repeated observations
- `Lineage`: Describe and/or cite data sources and/or methodological steps used to create this data source
- `Distribution`: Describe how the data is distributed, including any persistent identifier (e.g. DOI) or URL for data access
- `Constraints`: Legal constraints for *access* or *use* to protect *privacy* or *intellectual property rights*
- `Data Quality`: State result of quality assessment or state "Quality unknown"
- `Variables`: For each variable, enter the following information. If you have two or more variables per data source, you may want to present this information in table form (shown below)
  - `Label`: variable name as used in the data or code
  - `Alias`: intuitive natural language name
  - `Definition`: Short description or definition of the variable. Include measurement units in description.
  - `Type`: data type, e.g. character string, integer, real
  - `Accuracy`: e.g. uncertainty of measurements
  - `Domain`: Range (Maximum and Minimum) of numerical data, or codes or categories of nominal data, or reference to a standard codebook
  - `Missing Data Value(s)`: Values used to represent missing data and frequency of missing data observations
  - `Missing Data Frequency`: Frequency of missing data observations

| Label | Alias | Definition | Type | Accuracy | Domain | Missing Data Value(s) | Missing Data Frequency |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| variable1 | ... | ... | ... | ... | ... | ... | ... |
| variable2 | ... | ... | ... | ... | ... | ... | ... |

#### Secondary data source2 name

... same form as above...

### Prior observations  


At the time of this study pre-registration, the author had some prior knowledge of the geography of the study region with regards to the replication phenomena to be studied. The author had performed the original QGIS lab before this analysis. The reproduction follows the same workflow as the original lab. Mistakenly, the preregistration was written after the analysis was performed.

For each secondary source, declare the extent to which authors had already engaged with the data:

- [ ] data is not available yet
- [ ] data is available, but only metadata has been observed
- [ ] metadata and descriptive statistics have been observed
- [ ] metadata and a pilot test subset or sample of the full dataset have been observed
- [ ] the full dataset has been observed. Explain how authors have already manipulated / explored the data.

If pilot test data has been collected or acquired, describe how the researchers observed and analyzed the pilot test, and the extent to which the pilot test influenced the research design.

### Bias and threats to validity

Edge effects pose the greatest threats to validity of the original lab and reproduction study. Green spaces outside the city limits of Chicago are not considered. Chicago denizens living near the city limits could access green spaces outside of Chicago that are not included in parks.shp or forest.shp files. Including green spaces within a 0.25 mile distance from the city limits of Chicago could account for edge effects.

The initial lab design works to minimize modifiable areal unit problem (MAUP) occurrences. Access is calculated at the Census’s smallest unit size, blocks. Employing blocks to calculate access and population measures forms a more accurate model of access to green spaces within Chicago. 

The original lab and the reproduction do account for spatial heterogeneity. The analyzes assume Chicago is an isotropic plane ignoring the reality of transportation infrastructure, private property, and other barriers to mobility. Incorporating measures of these would greatly complicate the analyzes. The simplification of Chicago’s geography decreases the validity of the results while still providing informative results. 


### Data transformations

Describe all data transformations planned to prepare data sources for analysis.
This section should explain with the fullest detail possible how to transform data from the **raw** state at the time of acquisition or observation, to the pre-processed **derived** state ready for the main analysis.
Including steps to check and mitigate sources of **bias** and **threats to validity**.
The method may anticipate **contingencies**, e.g. tests for normality and alternative decisions to make based on the results of the test.
More specifically, all the **geographic** and **variable** transformations required to prepare input data as described in the data and variables section above to match the study's spatio-temporal characteristics as described in the study metadata and study design sections.
Visual workflow diagrams may help communicate the methodology in this section.

Examples of **geographic** transformations include coordinate system transformations, aggregation, disaggregation, spatial interpolation, distance calculations, zonal statistics, etc.

Examples of **variable** transformations include standardization, normalization, constructed variables, imputation, classification, etc.

Be sure to include any steps planned to **exclude** observations with *missing* or *outlier* data, to **group** observations by *attribute* or *geographic* criteria, or to **impute** missing data or apply spatial or temporal **interpolation**.

### Analysis

Describe the methods of analysis that will directly test the hypotheses or provide results to answer the research questions.
This section should explicitly define any spatial / statistical *models* and their *parameters*, including *grouping* criteria, *weighting* criteria, and *significance thresholds*.
Also explain any follow-up analyses or validations.

## Results

Describe how results are to be presented.

## Discussion

Describe how the results are to be interpreted *vis a vis* each hypothesis or research question.

## Integrity Statement

Include an integrity statement - The authors of this preregistration state that they completed this preregistration to the best of their knowledge and that no other preregistration exists pertaining to the same hypotheses and research.
If a prior registration *does* exist, explain the rationale for revising the registration here.

## Acknowledgements

This reproduction was completed for the Middlebury College Department of Geography course GEOG 361: Open GIScience in Fall 2023. The course was taught by Professor Joseph Holler, PhD.

This report is based upon the template for Reproducible and Replicable Research in Human-Environment and Geographical Sciences, DOI:[10.17605/OSF.IO/W29MQ](https://doi.org/10.17605/OSF.IO/W29MQ)


## References

Steven Manson, Jonathan Schroeder, David Van Riper, and Steven Ruggles. National Historical Geographic Information System: Version 13.0 [dataset]. Minneapolis, MN: IPUMS, 2018. https://doi.org/10.18128/D050.V13.0 

Tullis, Jason A., and Bandana Kar. “Where Is the Provenance? Ethical Replicability and Reproducibility in GIScience and Its Critical Applications.” Annals of the American Association of Geographers 111, no. 5 (July 29, 2021): 1318–28. https://doi.org/10.1080/24694452.2020.1806029.

Wilson, John P., Kevin Butler, Song Gao, Yingjie Hu, Wenwen Li, and Dawn J. Wright. “A Five-Star Guide for Achieving Replicability and Reproducibility When Working with GIS Software and Algorithms.” Annals of the American Association of Geographers 111, no. 5 (July 29, 2021): 1311–17. https://doi.org/10.1080/24694452.2020.1806026.


