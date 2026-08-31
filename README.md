# Columbian Sharp Tail Grouse and Greater Sage Grouse Lek Site Analysis
### Analysis of overlapping lekking range and habitat
### There are five script tools that will be used to preform the analysis

 The script tools will:
    clip lekking sites to smaller region
    clip landcover to smaller region
    preform Kernel density
    identify overlap
    create .csv and shapefile with final reports.

## Source Data:
   •	Data Source:
o	BLM UT GRSG Seasonal Habitats (Polygon). Department of the Interior: Bureau of Land Management,(2024), https://catalog.data.gov/dataset/blm-ut-grsg-seasonal-habitats-polygon

o	Elevation data: 10m DEM from USGS National Map, https://raster.utah.gov/

o	Land Cover Data. SWReGAP, Land Cover Data - SWReGAP

o	Sharp-Tailed grouse Leks data. https://dwr-data-utahdnr.hub.arcgis.com/datasets/utahDNR::ut-columbian-sharp-tailed-grouse-cstg-occupied-leks/about

o	UT DWR Greater Sage-Grouse Occupied Leks 2024. Arcgis.com, 2024, dwr-data-utahdnr.hub.arcgis.com/datasets/ut-dwr-greater-sage-grouse-occupied-leks-2024/explore
	Has updated data that I may use, UT DWR Greater Sage-Grouse Occupied Leks 2025 UT DWR Greater Sage-Grouse Occupied Leks 2025 | DWR Data
o	Utah Columbian Sharp-Tailed Grouse Habitat. Arcgis.com, 2025, dwr-data-utahdnr.hub.arcgis.com/datasets/utahDNR::utah-columbian-sharp-tailed-grouse-habitat/about

o	Utah Ruffed Grouse Habitat. Arcgis.com, 2025, dwr-data-utahdnr.hub.arcgis.com/datasets/utahDNR::utah-ruffed-grouse-habitat/about 


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
<img width="338" height="244" alt="LandcoverClip_Processing" src="https://github.com/user-attachments/assets/7ebd3db0-61df-4ebd-86fa-9845c026248a" />



### The DEM has already been set up for the Box Elder County Region
### The Landcover .tif is clipped to the Box Elder County Boundary to make the data more managable

![LandcoverClip script]
<img width="751" height="722" alt="LandcoverClip" src="https://github.com/user-attachments/assets/379dc23e-f2df-4e78-8f60-18c6e9d0e735" />

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

![GrouseClip script]
<img width="946" height="311" alt="GrouseClip" src="https://github.com/user-attachments/assets/4c780d64-5cd2-4ae9-832e-075303e913f9" />

![GrouseClip processing] 
<img width="334" height="247" alt="GrouseClip_Processing" src="https://github.com/user-attachments/assets/79db77ad-cff2-4362-9781-9ff403def54f" />

![GrouseClip results] 
<img width="511" height="270" alt="GrouseClip_results" src="https://github.com/user-attachments/assets/1a20cebb-0d36-4722-a176-e297ca180ada" />


# Create Buffer zones or Kernel Density using the clipped lekking site .shp files for both GRSG and CSTG.
#### We want two KDE polygons per species, Core and General
#### Run the 'KernelDensity' script tool two times. One for each species.

![KernelDensity script]
<img width="722" height="836" alt="KernelDensity" src="https://github.com/user-attachments/assets/6949c103-dfe9-4e1d-b125-9ee95b75f76e" />
![KernelDensity processing]
<img width="332" height="432" alt="KernelDensity_processing" src="https://github.com/user-attachments/assets/1b2624b5-2618-4167-afa6-81fb3dbb6bc4" />


    ####Here's and example of search radius at 6000. (6000-10000 is what I'd recommend)


# Analyze overlap KD Core regions of GRSG and CSTG lekking site buffer zones
## The 'Intersect Analysis' script tool will clip the core densities to only intersecting polygons

SpeciesA Core KD
SpeciesB Core KD

![IntersectAnalysis script]
<img width="747" height="310" alt="IntersectAnalysis" src="https://github.com/user-attachments/assets/b4760bed-b135-462b-95dd-183326a365ba" />

![IntersectAnalysis processing]
<img width="337" height="251" alt="IntersectAnalysis_Processing" src="https://github.com/user-attachments/assets/d25ca21f-e5d5-40bd-9119-64fdbcff0347" />


# Now that everything has been clipped down and overlap of core density has been identified
### It can be analyzed to identify any significant habitat and landcover competition between species during lekking

#### But, we can now also clip the landcover raster down to the intersect polygon.
#### Use the 'LandcoverClip' script tool again to get the clipped intersect landcover

![LandcoverClip_intersect processing]
<img width="334" height="268" alt="LandcoverClip_instersect_processing" src="https://github.com/user-attachments/assets/249e220c-6091-4637-804e-f210ee1782a0" />


##### Should now have groundcover raster in the intersect clip boundary

# This next block will read and process the feature attributes.
### export results as a shapefile and table for visualization and interpretation.
     output shapefile
     output .csv table reporting
     
![Process Reporting Step 1]
<img width="764" height="683" alt="ProcessReporting1" src="https://github.com/user-attachments/assets/5438c6cd-2e84-42f6-8f9c-a5abdb22ca98" />

![Process Reporting Step 2]
<img width="847" height="598" alt="ProcessReporting2" src="https://github.com/user-attachments/assets/83fb6d0a-64bf-49b0-b297-3f56992c619f" />


![Process Reporting Processing]
<img width="338" height="337" alt="ProcessReporting_Processing" src="https://github.com/user-attachments/assets/cb4397d6-5d72-45f5-92ec-5f4695107144" />

