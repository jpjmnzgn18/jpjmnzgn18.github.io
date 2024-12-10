# **Juan Pablo Jimenez Gonzalez**
### jpjmnzgn18.github.io
# **Adv GIS course final project site**
![hillshade](https://raw.githubusercontent.com/jpjmnzgn18/docs/main/assets/hillshade.jpg)
### Access the scripts: [adv GIS repository](https://github.com/jpjmnzgn18/GIS_Python.git)
## **Surface analysis tool**
### **Why would you want to use this tool?**
Once you're planning doing field work or you want to familiarize with an specific location, understanding the landscape is fundamental to determine next steps in your project. If you work with projects in different sites it can get really annoying and tedious to generate DEMs, slope, curvature and aspect rasters each time. It is nice to be able to do it all with just one command, instead of using each time different tools in differents GUIs.

### **Script description**
This script allows users to generate terrain analysis rasters (aspect, slope, hillshade, and curvature) from either a DEM or contour lines provided as input. If contour lines are used, the script first generates a DEM based on user-defined parameters, including the cell size and the elevation field from the shapefile's attribute table.

**Users can specify**:
The slope raster units (degrees or percent rise).
The calculation method for slope and aspect (planar or geodesic), where geodesic is recommended for large-scale datasets.
The output rasters are saved in a user-specified folder. The script validates all input paths and provides clear feedback in case of errors.

### **How it works?**

First the necessary libraries/modules are installed and then the functions to generate the DEM and terrain rasters are specified.

After that, the workflow is:

1. User Input: DEM or Contour Lines
2. Path for DEM (if DEM is selected)
3. Path for Contour Lines (if contour lines are selected)
4. Validate Inputs
5. Generate DEM from contours (if contour lines are selected)
6. Generate Terrain Rasters
7. Save Output Rasters

### What should I consider?
- Consider generating a new environment first, then installing the appropriate modules and check for compatibility between them. This script was created installing them with conda install -c conda-forge.

### - Outputs example

