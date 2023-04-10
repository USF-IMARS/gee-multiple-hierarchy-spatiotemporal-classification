# multiple-hierarchy-spatiotemporal-classifications
Documentation for the "multiple nominal hierarchy spatiotemporal classification modeling" methods using satellite imagery in google earth engine to create habiat classmaps.


## workflow for implementing a new habitat classification
1. Identify ground truth data
2. Select spatiotemporal input parameters
3. train + tweak the model
4. validate results

### 1. Identify ground truth data
Example ground truth data: 
* species-defined habitat data can be downloaded in the form of DwC-standardized taxonomic occurrence data from OBIS+GBIF 
    * open an issue here to for code to import DwC occurrences into GEE
* a tool for inputting "ground truth" data using a google earth engine app has been developed
    * open an issue here to set up a meeting 

### 2. select input parameters
Input pameters are spatiotemporal layers containing input data for the model.

A curated spreadsheet of the "most-awesome"<sup>TM</sup> input parameters in GEE can be found in [this g-sheet](https://docs.google.com/spreadsheets/d/1iShMShmQDnrlLkf3y3MMskKloH9bq3rxSg0z-KJucaY/edit?usp=sharing).

Common inputs include:

* elevation+bathymetry
* temperature
* precipitation
* reflectance (satellite images)

### 3. train+tweak
This modeling paradigm develops a model for each class representing the liklihood of the class for each spatiotemporal pixel.
To get greater accuracy each class can specify relationships relative to other classes.

#### Example of cloud-masking superceding water class:
* A model to identify the "cloud" class is created.
* The cloud class is set to supercede the "water" class.
    * a threshold is set tranform the probabilty of "cloud" into a binary (cloud|not cloud)  
* A model of the water class is created
    * ground truth points in spatiotemporal pixels determined "cloud" are excluded
    * input parameters are masked using the binary "cloud" layer

### 4. validate results
A random subseet of ground truth points should be witheld from training to be used for validation.
Methods for partitioning ground truth include:
* 80/20 split
* 10-fold cross validation

## Acknowldegements
These ideas have been developed through the following projects
* NSF 3D wetlands
* NERRS mangrove impact analyses

