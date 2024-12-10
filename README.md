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

### **What should I consider?**
- Consider generating a new environment first, then installing the appropriate modules and check for compatibility between them. This script was created installing them with conda install -c conda-forge.

### **Python code sections**

```python

# Conditions depending on the input

if input_type == 'dem':
    # User input for DEM processing
    input_dem = input("Enter the full path to the input DEM file (e.g., 'C:/data/dem.tif'): ").strip()
    output_folder = input("Enter the full path to the output folder (e.g., 'C:/data/output/'): ").strip()
    slope_units = input("Enter the slope units ('degrees' or 'percent'): ").strip().lower()

    # Validate slope units
    if slope_units not in ['degrees', 'percent']:
        print("Invalid slope_units input. Defaulting to 'degrees'.")
        slope_units = 'degrees'

    # Validate DEM file existence
    if not os.path.exists(input_dem):
        raise FileNotFoundError(f"The specified DEM file does not exist: {input_dem}")

    # Run raster generation
    generate_rasters(input_dem, output_folder, slope_units)

elif input_type == 'contour lines':
    # Contour lines handling
    contour_file = input("Enter the full path to the contour lines file (e.g., C:/data/contours.shp): ").strip()
    output_dem = input("Enter the full path to the output DEM file (e.g., C:/data/output_dem.tif): ").strip()
    cell_size = float(input("Enter the desired cell size for the DEM (e.g., 10.0): ").strip())
    
    # Load shapefile and display attributes
    try:
        gdf = gpd.read_file(contour_file)
        print("Shapefile opened successfully.")
        print(f"Layer name: {os.path.basename(contour_file)}")
        print(f"EPSG code: {gdf.crs}")
        print(f"Number of rows: {len(gdf)}")
        print(f"Geometry type: {gdf.geom_type.unique()}")
        print(f"Columns (fields) in the attribute table: {list(gdf.columns)}")

        # User selects the elevation field
        elev_field = input("Please type the name of the elevation field: ").strip()
        if elev_field not in gdf.columns:
            raise ValueError(f"Field '{elev_field}' not found in the attribute table.")

    except Exception as e:
        print(f"Error processing shapefile: {e}")
        raise

    # Generate DEM
    generated_dem = generate_dem_from_contours(contour_file, output_dem, cell_size, elev_field)

    # Proceed with terrain analysis
    output_folder = input("Enter the full path to the output folder (e.g., C:/data/output/): ").strip()
    slope_units = input("Enter the slope units ('degrees' or 'percent'): ").strip().lower()
    
    if slope_units not in ['degrees', 'percent']:
        print("Invalid slope_units input. Defaulting to 'degrees'.")
        slope_units = 'degrees'

    generate_rasters(generated_dem, output_folder, slope_units)

else:
    print("Invalid input. Please enter 'DEM' or 'contour lines'.")
```
### **Expected outputs**
![output](https://raw.githubusercontent.com/jpjmnzgn18/docs/main/assets/output_example.png)

