# Columbian Sharp Tail Grouse and Greater Sage Grouse Lek Site Analysis
### We are analyzing overlapping lekking range and habitat
### There are five script tools that will be used to preform the analysis

 The script tools will:
    clip lekking sites to smaller region
    clip landcover to smaller region
    preform Kernel density
    identify overlap
    create .csv and shapefile with final reports.

# Start by opening a new project in ArcPro, Map template.
    Add folder connection to folder containing the scripts and data folder
    Drag the following data to map:
        (0)be_10_dem
        (1)BLM_UT_GRSG_Seasonal_Habitats_Polygon).shp
        (2)Box_Elder_Addition_QL1_AOI.shp
        (3)CSTG_Occupied_Leks.shp
        (4)swgap_landcover_Clip.tif (clip to DEM)
        (5)UT_DWR_Greater_Sage-Grouse_Occupied_Leks.shp
        (6)Utah_Columbian_Sharptailed_Grouse_Habitat.shp


# Clip features to Area Of Interest by running 'LandcoverClip' script tool
### This will concentrate the analysis to a smaller area
![LandcoverClip processing](images/LandcoverClip_Processing.png)


### The DEM has already been set up for the Box Elder County Region
### The Landcover .tif is clipped to the Box Elder County Boundary to make the data more managable

![LandcoverClip script](images/LandcoverClip.png)
#### If it fails, try again (I'm not sure why it works sometimes and not others.)

# Next we want to clip the habitat polygons and lekking sites for each species to the region boundary
##For this we will use the 'GrouseClip' script tool

Run 'GrouseClip' tool 4 times
(1) first tool parameter (Utah_Columbian_Shaprtailed_Grouse_Habitat.shp)
     second tool parameter (Box_Elder_Addition_QL1_AOI.shp)
     third tool parameter (BE_UCSG_Hab.shp)
(2) first tool parameter (BLM_UT_GRSG_Seasonal_Habitats_(polygon).shp)
     second tool parameter (Box_Elder_Addition_QL1_AOI.shp)
     third tool parameter (BE_GRSG_Hab.shp)
(3) first tool parameter (CSTG_Occupied_Leks.shp)
     second tool parameter (Box_Elder_Addition_QL1_AOI.shp)
     third tool parameter (BE_UCSG_Lek.shp)
(4)  first tool parameter (UT_DWR_Greater_Sage-Grouse_Occupied_Leks_2025.shp)
     second tool parameter (Box_Elder_Addition_QL1_AOI.shp)
     third tool parameter (BE_UGRSG_Lek.shp)

![GrouseClip script](images/GrouseClip.png)
![GrouseClip processing] (images/GrouseClip_Processing.png)
![GrouseClip results] (images/GrouseClip_results.png)

# Create Buffer zones or Kernel Density using the clipped lekking site .shp files for both GRSG and CSTG.
#### We want two KDE polygons per species, Core and General
#### Run the 'KernelDensity' script tool two times. One for each species.

![KernelDensity script](images/KernelDensity.png)
![KernelDensity processing](images/KernelDensity_processing.png)
    ####Here's and example of search radius at 6000. (6000-10000 is what I'd recommend)


# Analyze overlap KD Core regions of GRSG and CSTG lekking site buffer zones
## The 'Intersect Analysis' script tool will clip the core densities to only intersecting polygons

SpeciesA Core KD
SpeciesB Core KD

![IntersectAnalysis script](images/IntersectAnalysis.png)
![IntersectAnalysis processing](images/IntersectAnalysis_Processing.png)


# Now that everything has been clipped down and overlap of core density has been identified
### It can be analyzed to identify any significant habitat and landcover competition between species during lekking

#### But, we can now also clip the landcover raster down to the intersect polygon.
#### Use the 'LandcoverClip' script tool again to get the clipped intersect landcover

![LandcoverClip_intersect processing](images/LandcoverClip_intersect_processing.png)

##### Should now have groundcover raster in the intersect clip boundary

# This next block will read and process the feature attributes.
### export results as a shapefile and table for visualization and interpretation.
     output shapefile
     output .csv table reporting
     
![Process Reporting Step 1](images/ProcessReporting1.png)
![Process Reporting Step 2](images/ProcessReporting2.png)

![Process Reporting Processing](images/ProcessReporting_Processing.png)
