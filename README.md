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
* use a tool for collecting "ground truth" image annotations
    * A tool in google earth engine app is being developed
    * see also the list [satellite-image-deep-learning/annotation](https://github.com/satellite-image-deep-learning/annotation)
* standardize annotation data into DwC-archive-like file format
* add the asset to the [list of DwC-archive-like-files](https://docs.google.com/spreadsheets/d/1RRC3L9dmvycJRG5f947DWAHBlZywpijYOwlJvBZ-yec/edit#gid=0)

### 2. select input parameters
Input pameters are spatiotemporal layers containing input data for the model.

A curated spreadsheet of the "most-awesome"<sup>TM</sup> input parameters in GEE can be found in [this g-sheet](https://docs.google.com/spreadsheets/d/1VyBMu1hN-FpSVV7Gi6VSTS1e3gaiudj6ZqYzsuvv3zw/edit?usp=sharing).

Common inputs include:

* elevation+bathymetry
* temperature
* precipitation
* reflectance (satellite images)

Additional imagery inputs can be pulled in from ERDDAP or other sources.
Other dataset lists:
* [corentin-dfg/Satellite-Image-Time-Series-Datasets](https://github.com/corentin-dfg/Satellite-Image-Time-Series-Datasets)

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

