# Jakobshavn Glacier NDSI Change Detection Using Landsat
This project uses Landsat 7, 8, and 9 surface reflectance imagery in Google Earth Engine to track changes in snow/ice conditions over Jakobshavn Glacier, Greenland. The analysis compares the summer conditions between 2000 and 2024 using the Normalised Difference Snow Index (NDSI) to capture the period of strongest surface melt. Landsat was chosen for its consistent data continuity and 30 m resolution, which is adequate for broad spatial patterns and glacier margins.


## Aim
To identify broad spatial changes in summer snow/ice cover over Jakobshavn Glacier between 2000 and 2024.


## Data Sources
All satellite data were imported from the Google Earth Engine Data Catalog:
- Landsat 7 Collection 2 Level 2: LANDSAT/LE07/C02/T1_L2
- Landsat 8 Collection 2 Level 2: LANDSAT/LC08/C02/T1_L2
- Landsat 9 Collection 2 Level 2: LANDSAT/LC09/C02/T1_L2


## Project Workflow
1. Filtered the Landsat ImageCollections (IC) to only include images within the glacier boundary. As summer in Greenland spans from June-August, Landsat 7 IC was filtered to only include images from 01/06/2000-31/08/2000, while Landsat 8 and 9 ICs were merged and filtered for images between 01/06/2024-31/08/2024.
2. Preprocessed the filtered ICs by selecting the green and SWIR bands for NDSI calculation and applying scale factors.
3. Created median summer composites for the year 2000 and 2024 from the preprocessed ICs.
4. Calculated the NDSI for these two composites, then filtered to keep only snow/ice pixels with NDSI >= 0.3.
5. Calculated the NDSI change as 2024 NDSI minus 2000 NDSI.
6. Plotted and visualised the changes.

Note that median composite + NDSI were used to address transient clouds as traditional GEE cloud mask confuses snow with clouds, resulting in images with very few pixels left.


## Results and Limitations
- The final dNDSI map shows negative NDSI change concentrated along parts of the glacier margins and downstream ablation zone, suggesting reduced surface snow/ice between summer 2000 and summer 2024.
- However, Landsat optical imagery can only track surface snow/ice changes and cannot represent subsurface loss or total glacier mass change. This is highly relevant as Jakobshavn Glacier is a marine-terminating glacier, with warm current flowing deep through the Ilulissat Icefjord trough, directly undermining the glacier from below. Thus, additional investigation into the change in elevation of the glacier or the ocean temperature is required.


## Tools
- Google Earth Engine (Python API): Users must have a Google Earth Engine account
- geemap: interactive map and conversion of Earth Engine images into NumPy arrays for plotting.
- numpy: array handling for image data converted from Earth Engine.
- matplotlib: plotting the final NDSI change map.
- matplotlib.colors / matplotlib.colorbar: creating the custom ΔNDSI colour scale and colour bar.
- pathlib: creating output folders and managing saved file paths.

Exact package requirements are provided in `requirements.txt`.
