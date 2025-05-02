# Land Suitability Study for Solar Power Plant in Kano State Using GIS and Multicriteria Decision Analysis

## Project Overview

This project performs a comprehensive suitability analysis for identifying optimal solar farm locations using ArcGIS Pro. The analysis incorporates multiple environmental, infrastructural, and geographical factors to determine areas that are most suitable for solar farm development while avoiding protected areas in Kano State, Nigeria.

## Prerequisites

- ArcGIS Pro (with Spatial Analyst and 3D Analyst extensions)
- Python 3.x
- Required input data (see Data Sources section)

## Installation

1. Clone or download this repository
2. Ensure that ArcGIS Pro is installed with the required extensions
3. Place all input data in the appropriate directories as referenced in the script

## Input Data

The dataset used for this analysis was fundamental spatial datasets that were used to perform a comprehensive evaluation. These dataset include a `Digital Elevation Model (DEM)` of resolution of 30m resolution from [Open Topography](https://opentopography.org/!) to know the topographic variations within the study area; `solar radiation` data from [Global Solar Atlas](https://globalsolaratlas.info/map); `land cover classification` data from [ESA Worlcover](https://esa-worldcover.org/en) which represents the land use of the study area for the year 2023; `road network` data from [GeoFabrik](https://www.geofabrik.de/) which is in vector format and contains classification of road types; `electrical grid` network data from [HDX](https://data.humdata.org/) which shows transmission and distribution points within the study area; `protected areas` boundaries from [World Database on Protected Areas (WDPA)](https://www.protectedplanet.net/en/thematic-areas/wdpa?tab=WDPA) which encompasses conservation zones, wildlife reserves, and culturally significant sites; and the `study area` boundary that defines the geographical scope of analysis.

## Methodology

The suitability analysis follows these main steps:

1. **Data Preparation**

   - Clipping all input data to the study area
   - Projecting rasters to Projected coordinate system. Here, WGS 1984 UTM Zone 31N coordinate system
   - Creating a filled DEM for topographic analysis

2. **Criteria Analysis**

   - **Solar Potential**: Reclassifies photovoltaic power output
   - **Terrain Analysis**:
     - Aspect: Evaluates optimal sun-facing slopes
     - Slope: Identifies flat areas suitable for installation
     - Elevation: Considers elevation effects on solar potential
   - **Infrastructure Proximity**:
     - Distance to electrical grid
     - Distance to road networks
   - **Land Cover**: Evaluates land cover suitability
   - **Constraints**: Excludes protected areas

3. **Weighted Overlay Analysis**

   - Combines all criteria with the following weights:
     - Solar Potential: 36%
     - Aspect: 14%
     - Slope: 8%
     - Land Cover: 5%
     - Elevation: 5%
     - Grid Proximity: 16%
     - Road Proximity: 16%

4. **Final Processing**
   - Reclassifies overlay results into three suitability classes
   - Extracts suitable areas outside protected regions
   - Converts raster results to vector polygons
   - Dissolves polygons based on suitability classification

## Output

The analysis produces several intermediate outputs and the final result:

- `Digital Elevation Model`: Map showing the DIgital Elevation of the Kano State
  ![alt text](maps/DEM.jpg)
- `Land Use`: Land Use map of Kano State
  ![alt text](maps/landuse.jpg)
- `Proximity to Grid`:
  ![alt text](maps/Proximity_to_grid.jpg)
- `Proximity to Road`
  ![alt text](maps/Proximity_to_road.jpg)

- `SuitableLocationsFarm`: Dissolved polygons grouped by suitability class

## Suitability Classes

The final output classifies areas into three suitability categories:

1. **Low Suitability** (1): Marginally suitable areas
2. **Moderate Suitability** (2): Areas with good potential
3. **High Suitability** (3): Optimal locations for solar farm development

## Usage

To run the analysis:

1. Ensure all input data is properly prepared and accessible
2. Open ArcGIS Pro and navigate to the project directory
3. Run the Python script from the ArcGIS Pro Python window or command line:
   ```python
   python solar_farm_suitability.py
   ```

## Customization

The analysis can be customized by modifying:

- Reclassification ranges for individual criteria
- Weighting scheme in the Weighted Overlay step
- Input data sources for updated or alternative datasets

## Project Structure

```
Solar Farm Suitability Analysis/
├── Solar Farm Suitability Analysis.gdb/  # Geodatabase containing all outputs
├── solar_farm_suitability.py             # Main Python script
└── Data/                                 # Input datasets
```

## Notes

- The script uses a UTM Zone 31N projection, which is appropriate for the study area
- The analysis considers the proximity to infrastructure balanced with environmental factors
- Protected areas are completely excluded from consideration

## Future Improvements

- Incorporate additional criteria such as land ownership and cost
- Add climate data to account for seasonal variations
- Include socio-economic factors for comprehensive analysis
- Implement sensitivity analysis for different weighting schemes

## License

[Specify your license information here]

## Contact

[Your contact information]
