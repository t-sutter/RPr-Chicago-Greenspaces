# Census Blocks 2010

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
