<div align="center">

<img src="icons/logo.png" alt="AriesGeo Toolbox Logo" width="460"/>

# AriesGeo Toolbox v4.0.0

**A Scientific, Processing-First Geospatial Suite for QGIS 3.28+ & QGIS 4.x**

[![Version](https://img.shields.io/badge/version-4.0.0-00897B?style=for-the-badge)](https://github.com/Hendrcks/ariesgeo)
[![QGIS Compatibility](https://img.shields.io/badge/QGIS-3.28%2B%20%7C%204.x-589632?style=for-the-badge&logo=qgis&logoColor=white)](https://qgis.org)
[![Algorithms](https://img.shields.io/badge/Processing%20Algorithms-100-1E88E5?style=for-the-badge)](https://github.com/Hendrcks/ariesgeo)
[![Tests](https://img.shields.io/badge/Automated%20Tests-45%20Passing-2E7D32?style=for-the-badge)](https://github.com/Hendrcks/ariesgeo)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg?style=for-the-badge)](LICENSE)

> **Find faster. Remove clouds & scan-line gaps cleanly. Model terrain and spatial decisions with scientific rigor.**

</div>

---

## Overview

**AriesGeo Toolbox 4.0** (`ariesgeo`) is a comprehensive, scientific geospatial processing plugin for QGIS developed by **AriesPlus** (*Elishaetikosin*). Built on a **Processing-First Architecture**, it combines **100 production-ready scientific algorithms** across **7 specialized domains** with native QGIS-themed dockable panels and guided interactive wizards.

Every tool is registered under the `ariesgeo:` Processing provider (`ariesgeo:<algorithm_id>`) and runs seamlessly across:
- **Interactive QGIS Dock Widgets & Non-Modal Wizards** (100% adaptive to QGIS Light, Dark, Blend of Gray, and Night Mapping themes)
- **QGIS Processing Toolbox & Graphical Modeler**
- **QGIS Batch Processing Interface**
- **Headless `qgis_process` CLI & PyQGIS Scripts**
- **QGIS 3.28+ (Qt5 / PyQt5) and QGIS 4.x (Qt6 / PyQt6)**

---

## Core Product Capabilities

### 1. Unified Cloud, Cast Shadow & Landsat 7 SLC-Off Recovery Engine
Implements the published **USGS / ENVI Landsat Gapfill methodology** (*Scaramuzza, Micijevic, & Chander, 2004*) unified with multi-sensor optical cloud and shadow masking:
- **USGS Phase-2 Local Linear Histogram Matching (`LLHM`):** Vectorized $O(1)$ integral-image moving-window matching with automatic multi-scale window expansion ($17 \to 35 \to 71 \to 143 \to 287 \to \text{Global}$), $2.5\sigma$ MAD outlier screening over mutually clear pixels, and boundary seam feathering:
  $$G_W = \frac{\sigma_{T,W}}{\sigma_{D,W}}, \qquad B_W = \mu_{T,W} - G_W \mu_{D,W}, \qquad \hat{T}(x,y) = G_W D(x,y) + B_W$$
- **USGS Phase-1 Global Linear Histogram Matching (`GLHM`) & Single-File Delaunay Triangulation (`TIN`):** Whole-scene radiometric normalization or donor-free barycentric planar triangulation across internal scan-line wedges and cloud voids while strictly preserving exterior tilted scene footprints.
- **Automatic Multi-Donor Co-Registration & Cloud Screening:** Donor scenes with different dimensions, extents, resolutions, or CRSs are automatically warped to the target pixel grid in memory (`gdal.Warp`), screened for donor clouds/shadows, and composited sequentially without overwriting higher-priority recoveries.
- **Multi-Sensor 8-Bit / 16-Bit / Float Cloud & Shadow Detection:** Accurate detection across 8-bit RGB, 16-bit Sentinel-2 (`0–10,000`), 16-bit Landsat Collection 2 (`7,273–43,636+` even with `0` borders and `65,535` saturation pixels), bitwise **Landsat C2 `QA_PIXEL`**, **Sentinel-2 L2A `SCL`**, or custom binary masks.

### 2. Native Tabified Place Finder & Geocoding Suite
- Automatically docks alongside QGIS's native **Layers / Browser** tab bar on startup as a native `QgsDockWidget` (`Place Finder`).
- Supports **Nominatim (OSM)**, **Photon (Komoot)**, **Offline SQLite FTS5 + R-Tree Gazetteers**, and instant offline coordinate parsing (`DD`, `DMS`, `UTM`).
- Includes interactive map zoom/flash, one-click export to QGIS vector layers, search history, and saved favorites.

### 3. Raster Preprocessing, Harmonization & Feather Mosaicking
- Preflight stack alignment auditing, DN-to-Surface-Reflectance scaling, virtual (`.vrt`) and priority permanent GeoTIFF mosaicking, raised-cosine overlap seamline feathering, and Cloud Optimized GeoTIFF (`COG`) export.

### 4. Hydrologically Conditioned Terrain & Basin Modeling
- Priority-Flood depression filling & breaching (*Barnes et al., 2014*), Horn (*1981*) & Zevenbergen-Thorne (*1987*) terrain derivatives, deterministic **D8** (*O'Callaghan & Mark, 1984*) and **Multiple Flow Direction (`MFD`)** (*Freeman, 1991*) routing, Strahler/Shreve stream ordering, `TWI`, `SPI`, and Horton-Strahler basin morphometry.

### 5. Spatial Statistics & Multi-Criteria Decision Analysis (`MCDA`)
- Saaty (*1980*) **Analytic Hierarchy Process (`AHP`)** eigenvector solver with Consistency Ratio ($CR$) validation, Weighted Linear Combination (`WLC`), Zadeh (*1965*) fuzzy membership & overlay, sensitivity analysis, Kernel Density Estimation (`KDE`), Global Moran's $I$, Local Moran's $I_i$ (`LISA`), Getis-Ord $G_i^*$, and Clark-Evans Nearest Neighbor statistics.

### 6. Geospatial Data Hub & Reproducible Provenance
- **STAC API v1.0** catalog search (Landsat C2, Sentinel-2 L2A, Copernicus/SRTM/NASADEM), OpenStreetMap Overpass vector extraction, resumable SHA-256 verified downloads, JSON workflow recipes, and sidecar provenance reports (`.json`, `.md`, `.html`).

---

## Quick Installation

### Option 1: Install from ZIP in QGIS (Recommended)
1. Download **[`ariesgeo_toolbox.zip`](https://github.com/Hendrcks/ariesgeo/raw/main/ariesgeo_toolbox.zip)** from this repository.
2. Open **QGIS** and navigate to **Plugins → Manage and Install Plugins...**
3. Select the **Install from ZIP** tab.
4. Browse to `ariesgeo_toolbox.zip` and click **Install Plugin**.
5. Confirm **AriesGeo Toolbox** is checked in the **Installed** tab.

### Option 2: Manual Installation
Extract `ariesgeo_toolbox.zip` directly into your QGIS Python plugins directory:
- **Windows (QGIS 4):** `%APPDATA%\QGIS\QGIS4\profiles\default\python\plugins\ariesgeo_toolbox`
- **Windows (QGIS 3):** `%APPDATA%\QGIS\QGIS3\profiles\default\python\plugins\ariesgeo_toolbox`
- **Linux:** `~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/ariesgeo_toolbox`
- **macOS:** `~/Library/Application Support/QGIS/QGIS3/profiles/default/python/plugins/ariesgeo_toolbox`

---

## How to Use AriesGeo Toolbox

Once enabled, AriesGeo Toolbox is accessible from three places in QGIS:
1. **Left Dock Panel Tab:** Click the **Place Finder** tab next to your *Layers* / *Browser* panels.
2. **Menu & Toolbar:** Open **Plugins → AriesGeo Toolbox** (or use the **AriesGeo Toolbar** icons).
3. **Processing Toolbox:** Open **Processing → Toolbox** (`Ctrl+Alt+T`) and expand **AriesGeo Toolbox** to access all 100 algorithms.

---

### Guide 1: Removing Clouds, Cast Shadows & SLC-Off Gaps (`Cloud Remover`)

Open **Plugins → AriesGeo Toolbox → Cloud Remover** (or click the Cloud icon on the toolbar). The non-modal dialog offers three workflow tabs:

#### A. Multi-Temporal LLHM Recovery *(Recommended when you have ≥ 1 reference date)*
1. **Select Target Raster:** Choose your cloudy or SLC-off raster from the **loaded QGIS Raster Layers** dropdown (or click **Browse...**). An output filename (`*_cloudfree_llhm.tif`) is suggested automatically.
2. **Choose Detection Mode:**
   - *Auto Spectral Cloud + Shadow Detection* — automatic multi-band cloud + cast-shadow masking for 8-bit, 16-bit Landsat/Sentinel, or float reflectance imagery.
   - *Unified SLC-Off Stripes + Clouds + Shadows* — simultaneously repairs Landsat 7 ETM+ scan-line wedges, clouds, and shadows in one pass.
   - *Landsat Collection 2 `QA_PIXEL` Bitmask* / *Sentinel-2 L2A `SCL` Classification* / *External Binary Mask* — use official sensor quality bands or a custom mask.
3. **Tune Sensitivity (Optional):** Adjust **Threshold** (`0.60` default; lower catches thin haze, higher targets bright clouds), **Halo Buffer** (`2 px` default), and **Detect & Remove Cast Cloud Shadows**.
4. **Add Clear Donor Scene(s):** Pick one or more clear reference dates from the QGIS layer dropdown (`+ Add Selected QGIS Layer`) or disk (`+ Browse Donor Files...`). *Donors do **not** need matching dimensions or extents — AriesGeo automatically warps and cloud-screens each donor.*
5. **Select Harmonization Model:** Keep **USGS Local Linear Histogram Matching (`LLHM — Best`)** for seamless radiometric blending across seasonal/illumination differences, and click **Run Multi-Temporal Cloud & SLC-Off Recovery**.

#### B. Single-Scene Triangulation / Inpainting *(When no donor scene is available)*
1. Switch to the **Single-Scene Triangulation / Inpainting** tab and select your input raster.
2. Choose **Single-File Delaunay Triangulation (USGS / ENVI Gapfill)** (ideal for SLC-off stripes and compact clouds) or **Multi-Scale Edge IDW Inpainting**.
3. Set **Max Fill Width** (in pixels) and click **Run Single-Scene Cloud & Gap Restoration**. Valid `0` values and exterior scene borders remain untouched.

#### C. Preview / Export Classified Cloud Mask
1. Switch to **Preview / Export Cloud Mask** to test threshold and buffer settings before running full multi-band restoration.
2. Click **Generate & Load Cloud Mask into QGIS** to inspect a classified GeoTIFF (`0 = Clear`, `1 = Cloud`, `2 = Cloud Shadow / SLC-Off Gap`).

---

### Guide 2: Guided Landsat 7 SLC-Off Restoration (`AriesGapfill Wizard`)

Open **Plugins → AriesGeo Toolbox → AriesGapfill (Landsat 7 SLC-off)...** to launch the **6-Step Guided Wizard**:
1. **Step 1 — Method:** Select *Two-Image Local Moving Window (`LLHM`)*, *Two-Image Global Matching (`GLHM`)*, *Multi-Donor Smart Composite*, or *Single-Image Delaunay Triangulation*.
2. **Step 2 — Inputs & Mask Source:** Pick your target and donor scenes from loaded QGIS layers or disk, and select what to repair (*Unified SLC-Off + Clouds & Shadows*, *Standard NoData*, *Zero Pixels (`DN = 0`)*, *Auto QA*, or *Custom Mask*).
3. **Step 3 — Grid Alignment:** Inspect CRS/resolution compatibility; keep **Auto-align / warp donor rasters to target pixel grid** enabled.
4. **Step 4 — Parameters:** Configure the initial moving-window size, minimum valid overlap pairs, seam feather width, and residual triangulation fallback.
5. **Step 5 — Outputs & Provenance:** Choose paths for the repaired GeoTIFF plus optional **Per-Pixel Provenance Raster** (records exact donor ID per filled pixel), **Confidence Score Raster (`0–100`)**, and **HTML + JSON Scientific Audit Report**.
6. **Step 6 — Execute & Inspect:** Run in the background and review per-band fill rates, regression gain/bias coefficients, and donor contribution shares.

---

### Guide 3: Place Finder Dock, Mosaicking & Terrain Hydrology

- **Place Finder Dock:** Type any settlement, landmark, address, or coordinate pair (e.g., `Accra`, `Mount Kilimanjaro`, or `5.6037, -0.1870`) in the **Place Finder** tab and press `Enter`. Double-click any result to zoom and flash the location on the map canvas, or click **Add Layer** to save results as a QGIS point layer.
- **Mosaic Wizard (`Plugins → AriesGeo Toolbox → Build Raster Mosaic...`):** Combine adjacent satellite tiles or DEMs into instant zero-copy `.vrt` mosaics or feather-blended, Cloud-Optimized GeoTIFFs.
- **Terrain & Hydrology Analyzer (`Plugins → AriesGeo Toolbox → Terrain & Hydrology...`):** Condition raw DEMs with Priority-Flood depression filling, compute slope/aspect/hillshade/TWI, route D8/MFD flow accumulation, extract vector stream networks, and delineate upstream watersheds from gauge points.

---

## PyQGIS & `qgis_process` Automation Examples

Every algorithm in **AriesGeo Toolbox 4.0** can be scripted in Python or executed headlessly via `qgis_process`:

### 1. Multi-Temporal Cloud, Shadow & SLC-Off Removal (PyQGIS)
```python
import processing

# Restore a cloudy / SLC-off scene using USGS Phase-2 Local Linear Histogram Matching (LLHM)
result = processing.run("ariesgeo:remove_clouds", {
    "TARGET_SCENE": "C:/data/LC07_target_cloudy.tif",
    "DONOR_SCENES": [
        "C:/data/LC08_donor_date1.tif",
        "C:/data/LC08_donor_date2.tif",
    ],
    "THRESHOLD": 0.60,
    "DETECT_SHADOWS": True,
    "INCLUDE_SLC_GAPS": True,
    "HARMONIZATION_METHOD": 0,  # 0 = USGS LLHM, 1 = USGS GLHM, 2 = Direct
    "APPLY_RADIOMETRY": True,
    "OUTPUT_RASTER": "C:/output/LC07_restored_llhm.tif",
    "OUTPUT_MASK": "C:/output/LC07_cloud_shadow_mask.tif",
})
```

### 2. Unified AriesGapfill with Per-Pixel Provenance & Confidence Maps
```python
import processing

gapfill_res = processing.run("ariesgeo:landsat_gapfill", {
    "TARGET_SCENE": "C:/data/LE07_slcoff.tif",
    "METHOD": 0,       # 0 = LLHM, 1 = GLHM, 2 = Multi-Donor, 3 = Single-Scene Triangulation
    "MASK_SOURCE": 0,  # 0 = Unified SLC-Off + Clouds & Shadows, 1 = SLC-Off/NoData, 2 = Clouds Only
    "DONOR_SCENES": ["C:/data/LE07_donor1.tif", "C:/data/LE07_donor2.tif"],
    "OUTPUT_RASTER": "C:/output/LE07_filled.tif",
    "OUTPUT_PROVENANCE": "C:/output/LE07_provenance.tif",
    "OUTPUT_CONFIDENCE": "C:/output/LE07_confidence.tif",
})
```

### 3. MCDA Suitability Weights (AHP) & Topographic Wetness Index (`TWI`)
```python
import processing

# Compute Saaty (1980) AHP weights with Consistency Ratio validation
ahp_result = processing.run("ariesgeo:ahp_weights", {
    "MATRIX_JSON": "[[1, 3, 5], [0.3333, 1, 2], [0.2, 0.5, 1]]",
    "CRITERIA_NAMES": "Slope,Hydrology,Proximity",
    "OUTPUT_REPORT": "C:/output/ahp_weights.json",
})

# Compute steady-state Topographic Wetness Index: ln(a / tan(beta))
twi_result = processing.run("ariesgeo:hydro_twi", {
    "INPUT_SCA": "C:/data/specific_catchment_area.tif",
    "INPUT_SLOPE": "C:/data/slope_degrees.tif",
    "OUTPUT_TWI": "C:/output/twi.tif",
})
```

### 4. Headless CLI Execution (`qgis_process`)
```bash
qgis_process run ariesgeo:remove_clouds \
  --TARGET_SCENE="C:/data/sentinel2_cloudy.tif" \
  --DONOR_SCENES="C:/data/sentinel2_clear.tif" \
  --THRESHOLD=0.60 \
  --DETECT_SHADOWS=true \
  --HARMONIZATION_METHOD=0 \
  --OUTPUT_RASTER="C:/output/sentinel2_cloudfree.tif"
```

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
| 07 | `ariesgeo:place_proximity` | `01.07 Distance to places matrix` | Build $N \times K$ origin-destination geodesic distance matrices |
| 08 | `ariesgeo:search_within_aoi` | `01.08 Extract places inside polygon AOI` | Spatial-index filtered extraction of gazetteer places within study polygons |
| 09 | `ariesgeo:offline_gazetteer_build` | `01.09 Build offline SQLite gazetteer` | Compile GeoNames/OSM extracts into an indexed offline SQLite FTS5 + R-Tree database |
| 10 | `ariesgeo:gazetteer_quality_audit` | `01.10 Audit gazetteer completeness` | Evaluate spatial density, attribute completeness, and duplicate toponyms |

### `02 · Landsat 7 SLC-off Gapfill` (`02_gapfill` — 15 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 11 | `ariesgeo:slc_metadata_inspector` | `02.01 Inspect Landsat 7 scene` | Parse Landsat Collection 2 MTL files for WRS-2 path/row, solar geometry, and calibration constants |
| 12 | `ariesgeo:slc_gap_mask` | `02.02 Detect SLC-off gaps` | Extract per-band and union scan-line wedge masks |
| 13 | `ariesgeo:slc_gap_metrics` | `02.03 Characterize gap geometry` | Measure gap percentage, scan-line width profiles, and gap area |
| 14 | `ariesgeo:slc_donor_rank` | `02.04 Rank donor scenes` | Score candidate scenes by temporal proximity, cloud cover, and spatial overlap |
| 15 | `ariesgeo:slc_coregistration` | `02.05 Register target and donor` | Co-register donor rasters to target grids via precision affine warping |
| 16 | `ariesgeo:slc_stable_pixel_mask` | `02.06 Identify radiometrically stable overlaps` | Screen mutually clear pixels across co-registered target and donor scenes |
| 17 | `ariesgeo:slc_global_match` | `02.07 Two-image global radiometric matching` | Normalize donor radiometry via USGS Phase-1 Global Linear Histogram Matching (`GLHM`) |
| 18 | `ariesgeo:slc_local_match` | `02.08 Two-image local-window matching` | Vectorized USGS Phase-2 Local Linear Histogram Matching (`LLHM`, *Scaramuzza et al., 2004*) |
| 19 | `ariesgeo:slc_single_tin` | `02.09 Single-image TIN interpolation` | Barycentric Delaunay triangulation fill across scan-line gaps with footprint preservation |
| 20 | `ariesgeo:slc_single_idw` | `02.10 Single-image IDW interpolation` | Cross-track Inverse Distance Weighting interpolation across scan-line voids |
| 21 | `ariesgeo:slc_two_scene_fill` | `02.11 Two-scene gap recovery` | Gap restoration using a co-registered, radiometrically harmonized donor scene |
| 22 | `ariesgeo:slc_multidonor_fill` | `02.12 Multi-donor temporal recovery` | Sequential multi-scene `LLHM` restoration with residual fallback and source provenance |
| 23 | `ariesgeo:slc_donor_consistency` | `02.13 Screen donor suitability for gap recovery` | Compute MAE, RMSE, and radiometric bias across mutually valid target-donor overlaps |
| 24 | `ariesgeo:slc_recovery_validation` | `02.14 Validate recovery with holdout masks` | Blind cross-validation by imposing synthetic holdout masks on intact regions |
| 25 | `ariesgeo:slc_recovery_report` | `02.15 Generate gapfill QA report` | Generate structured HTML & JSON scientific recovery audit reports |

### `03 · Raster Preprocessing & Cloud Removal` (`03_raster_prep` — 20 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 26 | `ariesgeo:raster_inspector` | `03.01 Preflight raster stack inspector` | Audit CRS, pixel resolution, grid origin alignment, band count, datatype, and NoData |
| 27 | `ariesgeo:scene_metadata` | `03.02 Extract optical scene metadata` | Parse Landsat MTL and Sentinel-2 XML metadata into standardized JSON |
| 28 | `ariesgeo:reflectance_scale` | `03.03 Scale DN to surface reflectance` | Apply sensor gain/offset scaling with solar zenith correction and physical clamping |
| 29 | `ariesgeo:radiometric_qa` | `03.04 Detect saturation and radiometric anomalies` | Flag radiometric saturation, negative reflectance, and extreme statistical outliers |
| 30 | `ariesgeo:raster_grid_align` | `03.05 Co-register and align raster grids` | Warp rasters to an exact snap grid origin, resolution, extent, and CRS |
| 31 | `ariesgeo:raster_stack_builder` | `03.06 Build harmonized multi-band stack` | Combine single-band rasters into a unified multi-band dataset |
| 32 | `ariesgeo:landsat_qa_mask` | `03.07 Landsat C2 pixel mask` | Bitwise decoding of Landsat Collection 2 `QA_PIXEL` cloud, shadow, and fill flags |
| 33 | `ariesgeo:sentinel_scl_mask` | `03.08 Sentinel-2 SCL pixel mask` | Classify Sentinel-2 L2A Scene Classification (`SCL`) classes into validity masks |
| 34 | `ariesgeo:cloud_mask_refine` | `03.09 Refine cloud/shadow mask` | Morphological halo dilation to capture diffuse cloud edges and adjacent shadows |
| 35 | `ariesgeo:cloud_coverage_report` | `03.10 Compute cloud-valid fractions` | Quantify cloud vs. clear-sky pixel fractions and area in $\text{km}^2$ |
| 36 | `ariesgeo:temporal_cloud_composite` | `03.11 Replace cloud pixels using other dates` | Multi-date cloud replacement via USGS `LLHM`, clear-pixel median, max, or mean |
| 37 | `ariesgeo:nodata_spatial_fill` | `03.12 Spatial NoData interpolation` | Interpolate localized internal voids while preserving exterior footprints |
| 38 | `ariesgeo:mosaic_vrt` | `03.13 Create validated VRT mosaic` | Instant zero-duplication `.vrt` mosaicking across large tile collections |
| 39 | `ariesgeo:mosaic_priority` | `03.14 Quality-priority mosaic` | Deterministic scene-priority mosaicking into tiled, compressed GeoTIFFs |
| 40 | `ariesgeo:mosaic_seam_blend` | `03.15 Seamline/blended mosaic` | Distance-weighted feather blending across overlapping scene seamlines |
| 41 | `ariesgeo:radiometric_harmonize` | `03.16 Overlap radiometric harmonization` | Linear radiometric normalization across scene overlap zones prior to mosaicking |
| 42 | `ariesgeo:raster_clip_aoi` | `03.17 Exact polygon AOI clip and mask` | Crop rasters to polygon cutlines with target grid snapping |
| 43 | `ariesgeo:cog_export` | `03.18 Export Cloud Optimized GeoTIFF (COG)` | Generate Cloud Optimized GeoTIFFs with internal tiling and multiscale overview pyramids |
| 44 | `ariesgeo:raster_batch_pipeline` | `03.19 Batch preprocess raster directory` | Execute standardized preprocess & COG export pipelines across directories |
| 45 | `ariesgeo:raster_quality_summary` | `03.20 Generate preprocessing quality summary` | Summarize per-band valid coverage, statistics, and SHA-256 checksums |

### `04 · Terrain & Hydrology` (`04_terrain_hydro` — 24 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 46 | `ariesgeo:dem_diagnostics` | `04.01 DEM hydrologic & geometric diagnostics` | Audit vertical units, geographic vs. projected CRS, voids, flats, and pit density |
| 47 | `ariesgeo:dem_merge_prepare` | `04.02 Merge and project DEM tiles` | Mosaic and reproject raw elevation tiles to a metric projected CRS |
| 48 | `ariesgeo:dem_void_fill` | `04.03 Interpolate DEM voids` | Fill elevation voids while preserving ridge and valley continuity |
| 49 | `ariesgeo:dem_sink_treatment` | `04.04 Fill or breach DEM depressions` | Priority-Flood depression filling and epsilon gradient enforcement (*Barnes et al., 2014*) |
| 50 | `ariesgeo:dem_slope` | `04.05 Compute slope gradient` | Horn (*1981*) $3\times3$ finite-difference slope in degrees, percent rise, or radians |
| 51 | `ariesgeo:dem_aspect` | `04.06 Compute aspect and northness/eastness` | Azimuthal aspect ($0^\circ\text{–}360^\circ$) plus continuous $\cos(\psi)$ northness & $\sin(\psi)$ eastness |
| 52 | `ariesgeo:dem_hillshade` | `04.07 Analytical and multidirectional hillshade` | Standard analytical and 6-azimuth multidirectional hillshade (*Mark, 1992*) |
| 53 | `ariesgeo:dem_curvature` | `04.08 Profile, plan, and total curvature` | Second-order polynomial surface curvatures (*Zevenbergen & Thorne, 1987*) |
| 54 | `ariesgeo:dem_tri` | `04.09 Terrain Ruggedness Index (TRI)` | Riley et al. (*1999*) root-mean-square elevation difference index |
| 55 | `ariesgeo:dem_tpi` | `04.10 Multi-scale Topographic Position Index (TPI)` | Weiss (*2001*) annulus neighborhood elevation residual and landform classification |
| 56 | `ariesgeo:dem_roughness` | `04.11 Surface roughness & vector dispersion` | Local elevation range, standard deviation, and 3D surface normal dispersion |
| 57 | `ariesgeo:dem_contours` | `04.12 Generate index and intermediate contours` | Extract smoothed elevation contour lines with index/intermediate classification |
| 58 | `ariesgeo:dem_profile` | `04.13 Extract longitudinal terrain profile` | Sample elevation, slope, and cumulative distance along transect lines |
| 59 | `ariesgeo:flow_d8` | `04.14 D8 flow direction and accumulation` | O'Callaghan & Mark (*1984*) steepest-descent D8 pointers and upslope cell counts |
| 60 | `ariesgeo:flow_mfd` | `04.15 Multiple Flow Direction (MFD) accumulation` | Freeman (*1991*) slope-partitioned multi-direction flow dispersion |
| 61 | `ariesgeo:flow_specific_area` | `04.16 Specific Catchment Area (SCA)` | Upslope contributing area per unit contour width ($a = A / b$) |
| 62 | `ariesgeo:flow_stream_extract` | `04.17 Extract channel network by threshold` | Vectorize drainage networks from contributing area thresholds |
| 63 | `ariesgeo:flow_outlet_snap` | `04.18 Snap pour points to high-flow channels` | Snap gauge stations to maximum flow accumulation cells within a search radius |
| 64 | `ariesgeo:flow_watershed` | `04.19 Delineate upstream watershed basins` | Trace complete upslope catchment boundaries for snapped pour points |
| 65 | `ariesgeo:flow_subbasins` | `04.20 Partition reach subbasins` | Decompose a drainage network into individual reach-level subcatchments |
| 66 | `ariesgeo:stream_order` | `04.21 Strahler and Shreve stream ordering` | Topological classification of stream networks by Strahler (*1957*) and Shreve (*1966*) order |
| 67 | `ariesgeo:hydro_twi` | `04.22 Topographic Wetness Index (TWI)` | Beven & Kirkby (*1979*) steady-state wetness index $\ln(a / \tan\beta)$ |
| 68 | `ariesgeo:hydro_spi` | `04.23 Stream Power Index (SPI)` | Moore et al. (*1991*) erosive power index $a \cdot \tan\beta$ |
| 69 | `ariesgeo:watershed_morphometry` | `04.24 Compute basin morphometric indices` | Drainage density, elongation ratio, circularity, relief ratio, and hypsometric integral |

### `05 · Spatial Statistics & Suitability` (`05_spatial_stats` — 15 Algorithms)
| # | Algorithm ID | Display Name | Summary |
| :- | :--- | :--- | :--- |
| 70 | `ariesgeo:raster_standardize` | `05.01 Normalize and standardize criterion rasters` | Min-max $[0,1]$, Z-score, quantile, and benefit/cost direction normalization |
| 71 | `ariesgeo:ahp_weights` | `05.02 AHP pairwise matrix weight calculator` | Saaty (*1980*) principal eigenvector weights with Consistency Index ($CI$) and Ratio ($CR$) |
| 72 | `ariesgeo:weighted_overlay` | `05.03 Weighted Linear Combination (WLC) suitability` | Multi-criteria weighted overlay with hard boolean exclusion masks |
| 73 | `ariesgeo:fuzzy_membership` | `05.04 Continuous fuzzy membership functions` | Linear, sigmoidal, Gaussian, and J-shaped fuzzy transformation functions |
| 74 | `ariesgeo:fuzzy_overlay` | `05.05 Fuzzy logic combination operators` | Combine fuzzy layers via AND, OR, Algebraic Product, Algebraic Sum, and Gamma ($\gamma$) |
| 75 | `ariesgeo:suitability_sensitivity` | `05.06 Suitability weight sensitivity analysis` | One-At-A-Time (`OAT`) weight perturbation and class-flip uncertainty mapping |
| 76 | `ariesgeo:zonal_distribution` | `05.07 Zonal statistics and percentile distributions` | Compute mean, SD, median, IQR, percentiles ($P_{10}, P_{90}$), and area shares per zone |
| 77 | `ariesgeo:point_kde` | `05.08 Kernel Density Estimation (KDE) surface` | Quartic/Epanechnikov kernel density estimation with Silverman's rule-of-thumb bandwidth |
| 78 | `ariesgeo:point_idw` | `05.09 IDW interpolation with LOO cross-validation` | Inverse Distance Weighting with automatic Leave-One-Out cross-validation RMSE/MAE |
| 79 | `ariesgeo:moran_global` | `05.10 Global Moran's I spatial autocorrelation` | Global Moran's $I$, expected $E[I]$, variance, Z-score, and Monte Carlo permutation $p$-value |
| 80 | `ariesgeo:moran_local` | `05.11 Local Moran's I (LISA) cluster map` | Anselin (*1995*) HH, LL, HL, and LH spatial cluster and outlier classification |
| 81 | `ariesgeo:gi_star` | `05.12 Getis-Ord Gi* hot and cold spot analysis` | Getis & Ord (*1992*) $G_i^*$ Z-scores and 90%/95%/99% confidence hot/cold spot tiers |
| 82 | `ariesgeo:nearest_neighbor_stats` | `05.13 Clark-Evans Nearest Neighbor Index` | Observed vs. expected nearest-neighbor distance ratio $R$ and spatial randomness test |
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
| 99 | `ariesgeo:validation_statistics` | `07.07 Compare reference and numerical result` | Compute MAE, RMSE, Bias, and $R^2$ between independent reference and modeled values |
| 100 | `ariesgeo:provenance_export` | `07.08 Export processing manifest` | Export SHA-256 provenance manifests documenting inputs, parameters, and software environment |

---

## Repository Structure

```text
ariesgeo_toolbox/
├── __init__.py                  # QGIS classFactory entry point
├── plugin.py                    # Main plugin lifecycle, tabified Place Finder dock, non-modal dialogs
├── resources.py                 # High-DPI icon & banner logo loader
├── metadata.txt                 # QGIS plugin metadata (v4.0.0)
├── icons/                       # High-DPI emblem icons (32..256px) & horizontal banner logo
├── core/                        # Background QThread worker, SHA-256 provenance & GeoTIFF / COG I/O
├── place_finder/                # Nominatim, Photon, & offline SQLite FTS5 geocoding engine
├── gapfill/                     # USGS Landsat Gapfill core (LLHM, GLHM, TIN, multi-donor, QA decoders)
├── raster/                      # Cloud & shadow remover, stack inspector, feather mosaicking
├── terrain_hydrology/           # Priority-Flood, Horn derivatives, D8/MFD routing, morphometry
├── spatial_stats/               # AHP, WLC, Fuzzy MCDA, KDE, IDW, Moran's I, LISA, Gi*
├── data_hub/                    # STAC client, Landsat/Sentinel/DEM catalogs, OSM importer
├── quality_workflows/           # Layer/grid/geometry auditors, JSON recipe runner, validation
├── processing_provider/         # AriesGeoProcessingProvider & 100 algorithm definitions
├── ui/                          # Native QGIS-themed Place Finder dock, Cloud Remover & wizards
└── tests/                       # Automated scientific & UI regression test suite (45 test cases)
```

---

## Running Automated Tests

```bash
# Run with your QGIS Python interpreter (QGIS 3.28+ or QGIS 4.2+)
python-qgis.bat tests/run_tests.py
```

---

## Key Scientific References

- **Scaramuzza, P., Micijevic, E., & Chander, G. (2004).** *SLC Gap-Filled Products Phase One Methodology* & *Phase Two Methodology*. USGS / EROS Data Center.
- **Barnes, R., Lehman, C., & Mulla, D. (2014).** Priority-Flood: An optimal depression-filling and watershed-labeling algorithm for digital elevation models. *Computers & Geosciences*, 62, 117–127.
- **O'Callaghan, J. F., & Mark, D. M. (1984).** The extraction of drainage networks from digital elevation data. *Computer Vision, Graphics, and Image Processing*, 28(3), 323–344.
- **Freeman, T. G. (1991).** Calculating catchment area with divergent flow based on a regular grid. *Computers & Geosciences*, 17(3), 413–422.
- **Saaty, T. L. (1980).** *The Analytic Hierarchy Process*. McGraw-Hill.
- **Anselin, L. (1995).** Local indicators of spatial association—LISA. *Geographical Analysis*, 27(2), 93–115.

---

## Author & License

- **Author:** AriesPlus (*Elishaetikosin*)
- **Repository:** [https://github.com/Hendrcks/ariesgeo](https://github.com/Hendrcks/ariesgeo)
- **License:** Distributed under the **GNU General Public License v3.0 (`GPL-3.0`)**. See [`LICENSE`](LICENSE) for details.
