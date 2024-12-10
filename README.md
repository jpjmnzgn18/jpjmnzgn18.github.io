# **Juan Pablo Jimenez Gonzalez**
# Adv GIS course final project site
### [adv GIS repository](https://github.com/jpjmnzgn18/GIS_Python.git)
## Surface analysis tool
### - Why would you want to use this tool?
Once you're planning doing field work or you want to familiarize with an specific location, understanding the landscape is fundamental to determine next steps in your project. If you work with projects in different sites it can get really annoying and tedious to generate DEMs, slope, curvature and aspect rasters each time. It is nice to be able to do it all with just one command, instead of using each time different tools in differents GUIs.

### - Script objective
Generate rasters of aspect, slope, hillshade and curvature depending on the input, which could be a DEM or contour lines. In case of contour lines are given as an input, a DEM will also be generated.

### - How it works?
Giving as an input contour lines or a DEM, the script will generate aspect, slope, hillshade and curvature rasters. The user should specify the units for slope raster (degrees or percent rise) and which method is used to calculate aspect and slope, wether geodesic or planar (geodesic is better for long very long extensions). The rasters will be saved in an output folder specified by the user.

### - Outputs
