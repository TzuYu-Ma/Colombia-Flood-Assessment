# Montería, Colombia Flood Assessment

This project focuses on assessing flood risks in Montería, Colombia, with a specific interest in investigating infection transmission during floods. Given the challenges with historical flood data quality, a Multi-Criteria Decision Making (MCDM) approach was employed.

## Data Sources
- **[GOV.CO](https://www.colombiaenmapas.gov.co/):** 
  GOV.CO includes comprehensive geo data in Colombia and is managed by the Colombian government.

- **[IDEAM](http://dhime.ideam.gov.co/atencionciudadano/):** 
  IDEAM stands for the Institute of Hydrology, Meteorology, and Environmental Studies (Instituto de Hidrología, Meteorología y Estudios Ambientales). It provides hydrology, meteorology, and environmental data.

## Data Flow Diagram

The following diagram illustrates the data flow for the Montería, Colombia Flood Assessment project:

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
