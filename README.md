# Montería, Colombia Flood Assessment

This project focuses on assessing flood risks in Montería, Colombia, with a specific interest in investigating infection transmission during floods. Given the challenges with historical flood data quality, a Multi-Criteria Decision Making (MCDM) approach was employed.

## Data Sources
- **[GOV.CO](https://www.colombiaenmapas.gov.co/):** 
  GOV.CO includes comprehensive geo data in Colombia and is managed by the Colombian government.

- **[IDEAM](http://dhime.ideam.gov.co/atencionciudadano/):** 
  IDEAM stands for the Institute of Hydrology, Meteorology, and Environmental Studies (Instituto de Hidrología, Meteorología y Estudios Ambientales). It provides hydrology, meteorology, and environmental data.


## Data Flow Diagram

The following diagram illustrates the parameters preparation:

```mermaid
graph TB
    A[Colombia government geo-data platform] -->|SRTM 30 Meters DEM| B[Fill DEM]
    B --> C[Flow Direction]
    B --> D[Flow Accumulation]
    C --> E[Use arcpy.sa.FlowDirection() to output Flow Direction]
    D --> F[Use arcpy.sa.FlowAccumulation() to output Flow Accumulation]
    F --> G[Distance from Stream]
    G --> H[Use arcpy.sa.EucDistance() to calculate distance]
    B --> I[Filled DEM (Elevation)]
    I --> J[Use arcpy.sa.Slope() to output Slope (degrees)]
    J --> K[Slope]
    K --> L[TWI]
    L --> M[Calculate TWI]
    
    A -->|2018 Land cover map (1:100,000)| N[LULC]
    N --> O[Reclassify rank 1 to 5]

    A -->|2008 Soil Characteristics Map, Córdoba (1:100,000)| P[Soil]
    P --> Q[Reclassify rank 1 to 5]
    
    A -->|2013-2023 Annual Precipitation| R[Precipitation]
    R --> S[Calculate average value]
    S --> T[Station points with annual precipitation value]
    T --> U[IDW]

    A -->|2018 distribution of population| V[Population]
    V --> W[polygon to raster]
    W --> X[Reclassify rank 1 to 5]

    Z[Google Earth Engine] -->|LANDSAT L08 C01 T1 8DAY NDVI| AA[NDVI]
```
The following diagram illustrates the  MCDA process:

```mermaid
graph TB
    A[Colombia government geo-data platform] -->|SRTM 30 Meters DEM| B[Fill DEM]
    B --> C[Flow Direction]
    B --> D[Flow Accumulation]
    C --> E[Use arcpy.sa.FlowDirection() to output Flow Direction]
    D --> F[Use arcpy.sa.FlowAccumulation() to output Flow Accumulation]
    F --> G[Distance from Stream]
    G --> H[Use arcpy.sa.EucDistance() to calculate distance]
    B --> I[Filled DEM (Elevation)]
    I --> J[Use arcpy.sa.Slope() to output Slope (degrees)]
    J --> K[Slope]
    K --> L[TWI]
    L --> M[Calculate TWI]
    
    A -->|2018 Land cover map (1:100,000)| N[LULC]
    N --> O[Reclassify rank 1 to 5]

    A -->|2008 Soil Characteristics Map, Córdoba (1:100,000)| P[Soil]
    P --> Q[Reclassify rank 1 to 5]
    
    A -->|2013-2023 Annual Precipitation| R[Precipitation]
    R --> S[Calculate average value]
    S --> T[Station points with annual precipitation value]
    T --> U[IDW]

    A -->|2018 distribution of population| V[Population]
    V --> W[polygon to raster]
    W --> X[Reclassify rank 1 to 5]

    Z[Google Earth Engine] -->|LANDSAT L08 C01 T1 8DAY NDVI| AA[NDVI]
```
## Methodology
A combination of various MCDM methods was used to ensure a comprehensive evaluation of high-risk areas:

1. **AHP (Analytic Hierarchy Process):**
   - Used to determine the relative importance (weights) of each criterion.
   
2. **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution):**
   - Evaluates alternatives based on their distance to an ideal solution, considering both best and worst-case scenarios.

3. **VIKOR (VlseKriterijumska Optimizacija I Kompromisno Resenje):**
   - Ranks alternatives with conflicting criteria by finding the closest solution to the ideal, ensuring a balanced compromise.

4. **EDAS (Evaluation Based on Distance from Average Solution):**
   - Assesses alternatives by calculating their positive and negative distances from an average solution.

### Process Overview:
- AHP was first used to determine the criterion weights.
- These weights were applied in the TOPSIS, VIKOR, and EDAS methods to generate flood risk maps.
- The results from these methods were standardized to produce a final flood risk assessment map.

## Tools & Environment
- **Software:** All analyses were conducted using ArcGIS Pro 3.1.0.

## References
- Mitra, Rajib & Das, Jayanta. (2022). A comparative assessment of flood susceptibility modelling of GIS-based TOPSIS, VIKOR and EDAS techniques in the Sub-Himalayan foothills region of Eastern India. 10.21203/rs.3.rs-1710264/v1.
