## Data Flow Diagram

The following diagram illustrates the data flow for the Montería, Colombia Flood Assessment project:

```mermaid
graph TB
    A[Colombia gov geo-data platform] --> B[Fill DEM]
    B --> C[Flow Direction]
    B --> D[Flow Accumulation]
    C --> E[Flow Direction Calc]
    D --> F[Flow Accumulation Calc]
    F --> G[Stream Distance Calc]
    B --> H[Filled DEM]
    H --> I[Slope Calculation]
    I --> J[Slope]
    J --> K[TWI Calculation]
    
    A --> L[LULC - 2018 Land Cover]
    L --> M[Reclassify 1 to 5]

    A --> N[Soil - 2008 Map]
    N --> O[Reclassify 1 to 5]
    
    A --> P[Precipitation - 2013-2023]
    P --> Q[Calc Average Value]
    Q --> R[Station Points with Precipitation]
    R --> S[IDW Interpolation]

    A --> T[Population - 2018 Data]
    T --> U[Convert to Raster]
    U --> V[Reclassify 1 to 5]

    W[Google Earth Engine] --> X[NDVI - LANDSAT Data]
