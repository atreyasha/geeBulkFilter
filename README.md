# geeBulkFilter

This project summarizes code in the Google Earth Engine API in order to bulk filter and export remote sensing data. These methods have been used in the following paper/thesis (https://github.com/AtreyaSh/remoteSensingThesis):

1. `geeBulkFilter.js` essentially imports a Landsat ImageCollection object and then conducts spatial and temporal filters. Next, it also clears clouds, cloud-shadows, water, snow and low illumination areas due to terrain-related shadows. Reprojection is also involved due to differing coordinate reference systems of datasets. Finally, an export function saves the filtered images onto Google Drive.

2. `projection_stringComparison.js` is experimental and is used to test the equivalence of techniques to retrieve projection data. 

<img src="https://user-images.githubusercontent.com/35427332/41541174-2428fc60-7312-11e8-98bb-9b05ffc24a9b.png" width="800">

# Guide for Ubuntu 16.04

## 1. Implement `geeBulkFilter.js` script in GEE

For simplicity, first navigate to a desired directory and clone this git repository onto your workspace:

`$ git clone https://github.com/AtreyaSh/geeBulkFilter.git`

1. To start this process, a Google account is necessary. Next, one needs to sign up for GEE. If this is not done as yet, navigate to the following site to sign up:

   https://earthengine.google.com/

2. After signing up for GEE, log into your account within GEE and navigate to the central code editor. Create a new repository and name it accordingly. 

3. Next, we need to upload certain assets required for our analysis. Within the GEE code editor, navigate to the `Assets` tab and select `NEW` and `Table upload`. Select all the files corresponding to the generic file path `/gee_input/DL_PL_KN_Dissolve_WGS84` with the endings `.cpg, .dbf, .prj, .sbn, .sbx, .shp, .shp.xml, .shx `. Let this asset be named `DL_PL_KN_Dissolve_WGS84`. Import this asset into the code editor with the variable name `table`.

4. Select all the files corresponding to the generic file path `/gee_input/DL_PL_KN_Dissolve_UTM43N` with the endings `.cpg, .dbf, .prj, .sbn, .sbx, .shp, .shp.xml, .shx `. Let this asset be named `DL_PL_KN_Dissolve_UTM43N`. Import this asset into the code editor with the variable name `table2`.

5. We now have the important variables imported. Now, copy and paste the code from the [geeBulkFilter.js](/geeBulkFilter.js) file into the GEE code editor. With this, we are good to go. 

6. Run the script and the corresponding data will be sent to your Google Drive for downloading!

**What does the `geeBulkFilter.js` script do?**

1. Queries Landsat 8 Surface Reflectance Imagery for the WRS Row/Path 147/38 in the time period from 2011-01-01 to 2017-05-01.

2. Chooses images with a mean cloud score of less than or equal to 10.

3. Clips the images to a desired shapefile.

4. Removes clouds, cloud-shadows, water and snow from the images to provide clear images for analysis.

5. Removes pixels which experience significant terrain-related shadows. This is done by calculating hillshade and setting a threshold for significant shadows.

6. Exports resulting images into your Google Drive.

This script results in 31 Landsat 8 SR images from 2013-2017 being downloaded into Google Drive. These images were then manually downloaded and can be found in the `/gee_output` directory.

## 2. Refine resulting remote sensing data

Now that we have downloaded the resulting remote sensing data from GEE, we would need to review and refine this data. Further information on this process can be found here: [geeDataClean.md](/geeDataClean.md)
