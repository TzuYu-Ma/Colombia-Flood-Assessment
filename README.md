```mermaid
graph TB
    A[Colombia government geo-data platform] --> B[Fill DEM]
    B --> C[Flow Direction]
    B --> D[Flow Accumulation]
    C --> E[Flow Direction Calculation]
    D --> F[Flow Accumulation Calculation]
    F --> G[Distance from Stream Calculation]
    B --> H[Filled DEM (Elevation)]
    H --> I[Slope Calculation]
    I --> J[Slope]
    J --> K[TWI Calculation]
    
    A --> L[LULC - 2018 Land Cover Map]
    L --> M[Reclassify rank 1 to 5]

    A --> N[Soil - 2008 Soil Characteristics Map]
    N --> O[Reclassify rank 1 to 5]
    
    A --> P[Precipitation - 2013-2023 Annual Data]
    P --> Q[Calculate Average Value]
    Q --> R[Station Points with Annual Precipitation]
    R --> S[IDW Interpolation]

    A --> T[Population - 2018 Distribution]
    T --> U[Convert to Raster]
    U --> V[Reclassify rank 1 to 5]

    W[Google Earth Engine] --> X[NDVI - LANDSAT L08 C01 T1 8DAY]