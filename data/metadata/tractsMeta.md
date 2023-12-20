# Census Tracts 2010

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
