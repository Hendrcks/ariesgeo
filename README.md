<div align="center">

# AriesGeo Toolbox v4.0.0

**A Scientific, Processing-First Geospatial Suite for QGIS 3.28+ & QGIS 4.x**

[![Version](https://img.shields.io/badge/version-4.0.0-00897B?style=for-the-badge)](https://github.com/Hendrcks/ariesgeo)
[![QGIS Compatibility](https://img.shields.io/badge/QGIS-3.28%2B%20%7C%204.x-589632?style=for-the-badge&logo=qgis&logoColor=white)](https://qgis.org)
[![Algorithms](https://img.shields.io/badge/Processing%20Algorithms-100-1E88E5?style=for-the-badge)](https://github.com/Hendrcks/ariesgeo)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg?style=for-the-badge)](LICENSE)

> **Find faster. Mosaic better. Model terrain and spatial decisions with scientific rigor.**

</div>

---

## Overview

**AriesGeo Toolbox 4.0** (`ariesgeo`) is a professional, scientific geospatial processing plugin for QGIS developed by **AriesPlus** (Elishaetikosin). Built on a **Processing-First Architecture**, it exposes **100 production-ready scientific algorithms** across **7 specialized domains**, alongside interactive dockable widgets and guided multi-step wizards.

Every algorithm is registered under the `ariesgeo:` Processing provider (`ariesgeo:<algorithm_id>`) and works natively across:
- **QGIS Processing Toolbox**
- **QGIS Graphical Modeler**
- **Batch Processing Interface**
- **Headless `qgis_process` CLI & PyQGIS Automation**
- **QGIS 3.28+ (Qt5 / PyQt5) and QGIS 4.x (Qt6 / PyQt6)**

---

## Quick Installation

### Option 1: Install from ZIP in QGIS (Recommended)
1. Download **[`ariesgeo_toolbox.zip`](https://github.com/Hendrcks/ariesgeo/raw/main/ariesgeo_toolbox.zip)** from this repository.
2. Open **QGIS** and navigate to **Plugins → Manage and Install Plugins...**
3. Select the **Install from ZIP** tab.
4. Browse to `ariesgeo_toolbox.zip` and click **Install Plugin**.
5. Enable **AriesGeo Toolbox** in the **Installed** tab.

### Option 2: Manual Installation
Extract `ariesgeo_toolbox.zip` directly into your QGIS Python plugins directory:
- **Windows (QGIS 4):** `%APPDATA%\QGIS\QGIS4\profiles\default\python\plugins\ariesgeo_toolbox`
- **Windows (QGIS 3):** `%APPDATA%\QGIS\QGIS3\profiles\default\python\plugins\ariesgeo_toolbox`
- **Linux:** `~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/ariesgeo_toolbox`
- **macOS:** `~/Library/Application Support/QGIS/QGIS3/profiles/default/python/plugins/ariesgeo_toolbox`

---

## Key Highlights in v4.0.0

- **100 Scientific Processing Algorithms:** Organized into 7 domain-specific groups with rigorous mathematical foundations and peer-reviewed citations.
- **Landsat 7 ETM+ SLC-off Restoration Suite:** Single-scene Delaunay triangulation (TIN), directional IDW, Global Linear Histogram Matching (GLHM), Local Linear Histogram Matching (LLHM, Scaramuzza et al. 2004), multi-donor priority compositing, cross-donor discrepancy auditing, and artificial scan-line cross-validation (RMSE, MAE, Bias, R²).
- **Raster Preprocessing & Cloud Removal:** Preflight alignment auditing, DN-to-Surface-Reflectance scaling, Landsat `QA_PIXEL` & Sentinel-2 `SCL` bitmask decoding, morphological cloud buffer refinement, multi-temporal cloud-free compositing, raised-cosine feather seam blending, and Cloud Optimized GeoTIFF (COG) export.
- **Terrain & Hydrological Modeling:** Priority-Flood depression treatment (Barnes et al. 2014), Horn (1981) & Zevenbergen-Thorne (1987) derivatives, deterministic D8 (O'Callaghan & Mark 1984) and Freeman (1991) MFD flow routing, Strahler (1957) & Shreve (1966) stream ordering, TWI, SPI, and Horton-Strahler basin morphometry.
- **Spatial Statistics & Multi-Criteria Decision Analysis (MCDA):** Saaty (1980) Analytic Hierarchy Process (AHP) eigenvector solver with Consistency Ratio (CR) validation, Weighted Linear Combination (WLC), Zadeh (1965) fuzzy membership & overlay, Global Moran's I, Anselin (1995) Local Moran's I (LISA), Getis-Ord Gi*, and Clark-Evans (1954) Nearest Neighbor analysis.
- **Geospatial Data Hub & Acquisition:** STAC API v1.0 catalog querying, Landsat Collection 2, Sentinel-2 L2A, and global DEM coverage discovery, OpenStreetMap Overpass extraction, SHA-256 verified asset downloading, and offline SQLite spatial indexing.
- **Reproducible Quality Control & Provenance:** SHA-256 dataset hashing, JSON workflow recipe execution, continuous validation statistics, and standardized machine-readable provenance manifests.

---

## Complete 100-Algorithm Catalog (`ariesgeo:`)

### `01 · Place Finder & Geocoding` (`01_place_finder` — 10 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 01 | `ariesgeo:place_search` | `01.01 Search places and settlements` | Forward geocode place names via Nominatim, Photon, or offline SQLite FTS5 gazetteers |
| 02 | `ariesgeo:reverse_geocode` | `01.02 Reverse geocode coordinates` | Resolve point features or coordinates into structured address hierarchies |
| 03 | `ariesgeo:batch_geocode` | `01.03 Batch geocode table` | Geocode CSV/attribute tables with rate-limit protection and fallback queries |
| 04 | `ariesgeo:coordinate_parser` | `01.04 Parse and normalize coordinates` | Parse DD, DMS, DDM, UTM, MGRS, and WKT strings into standardized geometries |
| 05 | `ariesgeo:transform_coordinates` | `01.05 Transform coordinate table CRS` | Reproject coordinate tables across CRSs with datum transformation auditing |
| 06 | `ariesgeo:nearest_place` | `01.06 Find nearest named settlement` | Compute geodesic distances and compass bearings to nearest populated places |
| 07 | `ariesgeo:place_proximity` | `01.07 Distance to places matrix` | Build N × K origin-destination geodesic distance matrices |
| 08 | `ariesgeo:search_within_aoi` | `01.08 Extract places inside polygon AOI` | Spatial-index filtered extraction of gazetteer places within study polygons |
| 09 | `ariesgeo:offline_gazetteer_build` | `01.09 Build offline SQLite gazetteer` | Compile GeoNames/OSM extracts into an indexed offline SQLite FTS5 + R-Tree database |
| 10 | `ariesgeo:gazetteer_quality_audit` | `01.10 Audit gazetteer completeness` | Evaluate spatial density, attribute completeness, and duplicate toponyms |

### `02 · Landsat 7 SLC-off Gapfill` (`02_gapfill` — 15 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 11 | `ariesgeo:slc_metadata_inspector` | `02.01 Parse Landsat MTL metadata` | Parse Landsat Collection 2 MTL files for WRS-2 path/row, solar geometry, and calibration constants |
| 12 | `ariesgeo:slc_gap_mask` | `02.02 Extract SLC-off gap mask` | Extract per-band and union scan-line wedge masks |
| 13 | `ariesgeo:slc_gap_metrics` | `02.03 Quantify gap geometry and severity` | Measure gap percentage, scan-line width profiles, and nadir usable core width |
| 14 | `ariesgeo:slc_donor_rank` | `02.04 Rank candidate donor scenes` | Score candidate scenes by temporal proximity, seasonal day-of-year, cloud cover, and overlap |
| 15 | `ariesgeo:slc_coregistration` | `02.05 Sub-pixel donor co-registration` | Align donor scenes to target grid via FFT phase correlation and affine shifting |
| 16 | `ariesgeo:slc_stable_pixel_mask` | `02.06 Mask clouds and transient change` | Exclude clouds, shadows, snow, and land-cover change from regression training |
| 17 | `ariesgeo:slc_global_match` | `02.07 Global linear histogram match` | Normalize donor radiometry via scene-wide robust gain/bias estimation |
| 18 | `ariesgeo:slc_local_match` | `02.08 Local moving-window regression (LLHM)` | USGS Phase-2 Local Linear Histogram Matching (Scaramuzza et al. 2004) |
| 19 | `ariesgeo:slc_single_tin` | `02.09 Single-scene Delaunay triangulation fill` | Barycentric planar interpolation across scan-line gaps with footprint preservation |
| 20 | `ariesgeo:slc_single_idw` | `02.10 Single-scene directional IDW fill` | Anisotropic cross-track Inverse Distance Weighting interpolation |
| 21 | `ariesgeo:slc_two_scene_fill` | `02.11 Two-scene primary donor transfer` | Gap restoration using a single radiometrically harmonized donor scene |
| 22 | `ariesgeo:slc_multidonor_fill` | `02.12 Multi-donor priority composite fill` | Sequential multi-scene restoration with spatial fallback and source provenance |
| 23 | `ariesgeo:slc_donor_consistency` | `02.13 Cross-donor discrepancy map` | Pixel-wise radiometric standard deviation and Z-score anomaly mapping across donors |
| 24 | `ariesgeo:slc_recovery_validation` | `02.14 Artificial scan-line cross-validation` | Blind cross-validation by imposing synthetic SLC-off masks on intact regions |
| 25 | `ariesgeo:slc_recovery_report` | `02.15 Export gap-fill provenance report` | Generate structured JSON & Markdown scientific recovery audit reports |

### `03 · Raster Preprocessing & Cloud Removal` (`03_raster_prep` — 20 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 26 | `ariesgeo:raster_inspector` | `03.01 Preflight raster stack inspector` | Audit CRS, pixel resolution, grid origin alignment, band count, datatype, and NoData |
| 27 | `ariesgeo:scene_metadata` | `03.02 Extract optical scene metadata` | Parse Landsat MTL and Sentinel-2 XML metadata into standardized JSON |
| 28 | `ariesgeo:reflectance_scale` | `03.03 Scale DN to surface reflectance` | Apply sensor gain/offset scaling with solar zenith correction and physical clamping |
| 29 | `ariesgeo:radiometric_qa` | `03.04 Detect saturation and radiometric anomalies` | Flag radiometric saturation, negative reflectance, and extreme statistical outliers |
| 30 | `ariesgeo:raster_grid_align` | `03.05 Co-register and align raster grids` | Warp rasters to an exact snap grid origin, resolution, extent, and CRS |
| 31 | `ariesgeo:raster_stack_builder` | `03.06 Build harmonized multi-band stack` | Combine single-band rasters into a unified multi-band dataset with wavelength metadata |
| 32 | `ariesgeo:landsat_qa_mask` | `03.07 Decode Landsat QA_PIXEL mask` | Bitwise decoding of Landsat Collection 2 `QA_PIXEL` cloud, shadow, dilated cloud, and snow flags |
| 33 | `ariesgeo:sentinel_scl_mask` | `03.08 Decode Sentinel-2 SCL mask` | Classify Sentinel-2 L2A Scene Classification (`SCL`) classes into binary clear/contaminated masks |
| 34 | `ariesgeo:cloud_mask_refine` | `03.09 Morphological cloud mask refinement` | Morphological opening, closing, sieve filtering, and Euclidean safety buffering |
| 35 | `ariesgeo:cloud_coverage_report` | `03.10 Calculate cloud coverage per AOI` | Quantify usable clear-sky percentages per scene and study polygon |
| 36 | `ariesgeo:temporal_cloud_composite` | `03.11 Multi-temporal cloud-free composite` | Construct cloud-free composites via medoid, median, or clearest-observation synthesis |
| 37 | `ariesgeo:nodata_spatial_fill` | `03.12 Spatial NoData hole interpolation` | Interpolate small internal voids with max-area guards that preserve outer footprints |
| 38 | `ariesgeo:mosaic_vrt` | `03.13 Build GDAL Virtual Mosaic (VRT)` | Instant zero-duplication `.vrt` mosaicking across large tile collections |
| 39 | `ariesgeo:mosaic_priority` | `03.14 Priority-ordered permanent mosaic` | Deterministic scene-priority mosaicking into tiled, compressed GeoTIFFs |
| 40 | `ariesgeo:mosaic_seam_blend` | `03.15 Feather-blended seamline mosaic` | Distance-weighted raised-cosine feather blending across overlap zones |
| 41 | `ariesgeo:radiometric_harmonize` | `03.16 Overlap radiometric harmonization` | OLS/Theil-Sen linear normalization across scene overlap zones prior to mosaicking |
| 42 | `ariesgeo:raster_clip_aoi` | `03.17 Exact polygon AOI clip and mask` | Crop rasters to polygon cutlines with target grid snapping |
| 43 | `ariesgeo:cog_export` | `03.18 Export Cloud Optimized GeoTIFF (COG)` | Generate Cloud Optimized GeoTIFFs with internal tiling and multiscale overview pyramids |
| 44 | `ariesgeo:raster_batch_pipeline` | `03.19 Batch preprocess raster directory` | Execute standardized scale → mask → align → clip → COG pipelines across folders |
| 45 | `ariesgeo:raster_quality_summary` | `03.20 Generate preprocessing quality summary` | Summarize per-band valid coverage, histograms, and SHA-256 checksums |

### `04 · Terrain & Hydrology` (`04_terrain_hydro` — 24 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 46 | `ariesgeo:dem_diagnostics` | `04.01 DEM hydrologic & geometric diagnostics` | Audit vertical units, geographic vs. projected CRS, voids, flats, and pit density |
| 47 | `ariesgeo:dem_merge_prepare` | `04.02 Merge and project DEM tiles` | Mosaic and reproject raw elevation tiles to a metric projected CRS using cubic/bilinear kernels |
| 48 | `ariesgeo:dem_void_fill` | `04.03 Interpolate DEM voids` | Fill elevation voids while preserving ridge and valley continuity |
| 49 | `ariesgeo:dem_sink_treatment` | `04.04 Fill or breach DEM depressions` | Priority-Flood depression filling and epsilon gradient enforcement (Barnes et al. 2014) |
| 50 | `ariesgeo:dem_slope` | `04.05 Compute slope gradient` | Horn (1981) 3×3 finite-difference slope in degrees, percent rise, or radians |
| 51 | `ariesgeo:dem_aspect` | `04.06 Compute aspect and northness/eastness` | Azimuthal aspect (0°–360°) plus continuous cos(ψ) northness & sin(ψ) eastness |
| 52 | `ariesgeo:dem_hillshade` | `04.07 Analytical and multidirectional hillshade` | Standard analytical and 6-azimuth multidirectional hillshade (Mark 1992) |
| 53 | `ariesgeo:dem_curvature` | `04.08 Profile, plan, and total curvature` | Second-order polynomial surface curvatures (Zevenbergen & Thorne 1987) |
| 54 | `ariesgeo:dem_tri` | `04.09 Terrain Ruggedness Index (TRI)` | Riley et al. (1999) root-mean-square elevation difference index |
| 55 | `ariesgeo:dem_tpi` | `04.10 Multi-scale Topographic Position Index (TPI)` | Weiss (2001) annulus neighborhood elevation residual and landform classification |
| 56 | `ariesgeo:dem_roughness` | `04.11 Surface roughness & vector dispersion` | Local elevation range, standard deviation, and 3D surface normal dispersion |
| 57 | `ariesgeo:dem_contours` | `04.12 Generate index and intermediate contours` | Extract smoothed elevation contour lines with index/intermediate classification |
| 58 | `ariesgeo:dem_profile` | `04.13 Extract longitudinal terrain profile` | Sample elevation, slope, and cumulative distance along transect lines |
| 59 | `ariesgeo:flow_d8` | `04.14 D8 flow direction and accumulation` | O'Callaghan & Mark (1984) steepest-descent D8 pointers and upslope cell counts |
| 60 | `ariesgeo:flow_mfd` | `04.15 Multiple Flow Direction (MFD) accumulation` | Freeman (1991) slope-partitioned multi-direction flow dispersion |
| 61 | `ariesgeo:flow_specific_area` | `04.16 Specific Catchment Area (SCA)` | Upslope contributing area per unit contour width (a = A / b) |
| 62 | `ariesgeo:flow_stream_extract` | `04.17 Extract channel network by threshold` | Vectorize drainage networks from contributing area thresholds |
| 63 | `ariesgeo:flow_outlet_snap` | `04.18 Snap pour points to high-flow channels` | Snap gauge stations to maximum flow accumulation cells within a search radius |
| 64 | `ariesgeo:flow_watershed` | `04.19 Delineate upstream watershed basins` | Trace complete upslope catchment boundaries for snapped pour points |
| 65 | `ariesgeo:flow_subbasins` | `04.20 Partition reach subbasins` | Decompose a drainage network into individual reach-level subcatchments |
| 66 | `ariesgeo:stream_order` | `04.21 Strahler and Shreve stream ordering` | Topological classification of stream networks by Strahler (1957) and Shreve (1966) order |
| 67 | `ariesgeo:hydro_twi` | `04.22 Topographic Wetness Index (TWI)` | Beven & Kirkby (1979) steady-state wetness index ln(a / tan β) |
| 68 | `ariesgeo:hydro_spi` | `04.23 Stream Power Index (SPI)` | Moore et al. (1991) erosive power index a · tan β |
| 69 | `ariesgeo:watershed_morphometry` | `04.24 Compute basin morphometric indices` | Drainage density, elongation ratio, circularity, relief ratio, and hypsometric integral |

### `05 · Spatial Statistics & Suitability` (`05_spatial_stats` — 15 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 70 | `ariesgeo:raster_standardize` | `05.01 Normalize and standardize criterion rasters` | Min-max [0,1], Z-score, quantile, and benefit/cost direction normalization |
| 71 | `ariesgeo:ahp_weights` | `05.02 AHP pairwise matrix weight calculator` | Saaty (1980) principal eigenvector weights with Consistency Index (CI) and Ratio (CR) |
| 72 | `ariesgeo:weighted_overlay` | `05.03 Weighted Linear Combination (WLC) suitability` | Multi-criteria weighted overlay with hard boolean exclusion masks |
| 73 | `ariesgeo:fuzzy_membership` | `05.04 Continuous fuzzy membership functions` | Linear, sigmoidal, Gaussian, and J-shaped fuzzy transformation functions |
| 74 | `ariesgeo:fuzzy_overlay` | `05.05 Fuzzy logic combination operators` | Combine fuzzy layers via AND, OR, Algebraic Product, Algebraic Sum, and Gamma (γ) |
| 75 | `ariesgeo:suitability_sensitivity` | `05.06 Suitability weight sensitivity analysis` | One-At-A-Time (OAT) weight perturbation and class-flip uncertainty mapping |
| 76 | `ariesgeo:zonal_distribution` | `05.07 Zonal statistics and percentile distributions` | Compute mean, SD, median, IQR, percentiles (P10, P90), and area shares per zone |
| 77 | `ariesgeo:point_kde` | `05.08 Kernel Density Estimation (KDE) surface` | Quartic/Epanechnikov kernel density estimation with Silverman's rule-of-thumb bandwidth |
| 78 | `ariesgeo:point_idw` | `05.09 IDW interpolation with LOO cross-validation` | Inverse Distance Weighting with automatic Leave-One-Out cross-validation RMSE/MAE |
| 79 | `ariesgeo:moran_global` | `05.10 Global Moran's I spatial autocorrelation` | Global Moran's I, expected E[I], variance, Z-score, and Monte Carlo permutation p-value |
| 80 | `ariesgeo:moran_local` | `05.11 Local Moran's I (LISA) cluster map` | Anselin (1995) HH, LL, HL, and LH spatial cluster and outlier classification |
| 81 | `ariesgeo:gi_star` | `05.12 Getis-Ord Gi* hot and cold spot analysis` | Getis & Ord (1992) Gi* Z-scores and 90%/95%/99% confidence hot/cold spot tiers |
| 82 | `ariesgeo:nearest_neighbor_stats` | `05.13 Clark-Evans Nearest Neighbor Index` | Observed vs. expected nearest-neighbor distance ratio R and spatial randomness test |
| 83 | `ariesgeo:buffer_exposure_summary` | `05.14 Multi-ring buffer exposure summary` | Summarize raster and vector indicators across concentric distance rings |
| 84 | `ariesgeo:spatial_model_report` | `05.15 Export MCDA & spatial statistics report` | Compile AHP matrices, weights, area breakdowns, and autocorrelation metrics into a report |

### `06 · Data Hub & Acquisition` (`06_data_hub` — 8 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 85 | `ariesgeo:catalog_stac_search` | `06.01 Query STAC API catalog by AOI and date` | Query STAC v1.0 endpoints (Earth Search, Planetary Computer, USGS) into vector footprints |
| 86 | `ariesgeo:catalog_asset_inspect` | `06.02 Inspect STAC item bands and COG URLs` | Extract asset band keys, spatial resolutions, EPSG codes, and `/vsicurl/` streaming paths |
| 87 | `ariesgeo:catalog_landsat_search` | `06.03 Search Landsat 7/8/9 Collection 2 scenes` | Search Landsat Collection 2 scenes with WRS-2 Path/Row and SLC-off donor scoring |
| 88 | `ariesgeo:catalog_sentinel_search` | `06.04 Search Sentinel-2 L2A scenes` | Search Sentinel-2 L2A scenes by MGRS tile, cloud cover, and seasonal window |
| 89 | `ariesgeo:catalog_dem_search` | `06.05 Identify available global DEM tiles` | Discover Copernicus GLO-30, SRTM, NASADEM, and AW3D30 tiles intersecting an AOI |
| 90 | `ariesgeo:catalog_osm_import` | `06.06 Download OpenStreetMap vectors by AOI` | Query Overpass API to import roads, waterways, buildings, and settlements into GeoPackage layers |
| 91 | `ariesgeo:download_assets` | `06.07 Batch download and verify remote assets` | Resumable download manager with retries and SHA-256 checksum verification |
| 92 | `ariesgeo:local_catalog_index` | `06.08 Index local geospatial folder into catalog` | Scan local folders to build a searchable SQLite spatial catalog of rasters and vectors |

### `07 · Quality Control & Workflows` (`07_quality_workflows` — 8 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 93 | `ariesgeo:layer_integrity_audit` | `07.01 Audit dataset CRS, bounds, and integrity` | Verify readability, valid CRS definitions, non-empty bounds, and spatial index presence |
| 94 | `ariesgeo:raster_alignment_audit` | `07.02 Strict pixel-grid alignment verifier` | Verify exact CRS, pixel size, and origin alignment across multi-raster stacks |
| 95 | `ariesgeo:vector_geometry_audit` | `07.03 Audit vector topology and geometry validity` | GEOS validity check for self-intersections, unclosed rings, duplicate vertices, and slivers |
| 96 | `ariesgeo:algorithm_preflight` | `07.04 Pre-execution scientific readiness check` | Check geographic vs. projected CRS rules and sample-size requirements before running models |
| 97 | `ariesgeo:workflow_run` | `07.05 Execute JSON analysis recipe` | Execute multi-step `.aries_recipe.json` pipelines with intermediate handoff and logging |
| 98 | `ariesgeo:workflow_batch` | `07.06 Run analysis recipe across batch AOIs` | Iterate a JSON analysis recipe across multiple study areas or temporal windows |
| 99 | `ariesgeo:validation_statistics` | `07.07 Compare reference and numerical result` | Compute MAE, RMSE, Bias, and R² between independent reference and modeled values |
| 100 | `ariesgeo:provenance_export` | `07.08 Export processing manifest` | Export SHA-256 provenance manifests documenting inputs, parameters, and software environment |

---

## PyQGIS & CLI Usage Example

Every tool in **AriesGeo Toolbox 4.0** can be called programmatically in Python or via `qgis_process`:

```python
import processing

# 1. Calculate AHP Criteria Weights with Consistency Ratio check
ahp_result = processing.run("ariesgeo:ahp_weights", {
    "MATRIX_JSON": "[[1, 3, 5], [0.3333, 1, 2], [0.2, 0.5, 1]]",
    "CRITERIA_NAMES": "Slope,Hydrology,Proximity",
    "OUTPUT_REPORT": "C:/temp/ahp_weights.json"
})

# 2. Compute Topographic Wetness Index (TWI)
twi_result = processing.run("ariesgeo:hydro_twi", {
    "INPUT_SCA": "C:/data/specific_catchment_area.tif",
    "INPUT_SLOPE": "C:/data/slope_degrees.tif",
    "OUTPUT_TWI": "C:/temp/twi.tif"
})
```

---

## Author & License

- **Author:** AriesPlus (Elishaetikosin)
- **Repository:** [https://github.com/Hendrcks/ariesgeo](https://github.com/Hendrcks/ariesgeo)
- **License:** Distributed under the **GNU General Public License v3.0 (GPL-3.0)**.
