# Automated Terrain-Based Flood Hazard Modeling (HAND)

## 1. The Problem
Manual hydrodynamic modeling (e.g., HEC-RAS) takes weeks of GUI-based data preparation, digitization, and processing. It creates human bottlenecks and scales poorly across massive regions.

## 2. The Engineering Solution
A 100% automated Python pipeline that generates accurate, hydrostatic inundation maps and vulnerability overlays in minutes. 
* Programmatic ingestion of Copernicus 30m DEM arrays.
* Fully automated hydrological conditioning (pit/depression filling) and D8 flow routing.
* Dynamic calculation of the Height Above Nearest Drainage (HAND) matrix.

## 3. Pipeline Resilience (The Edge Cases)
* **API Failbacks:** When the Overpass API timed out on massive regional queries, the pipeline was engineered to autonomously fall back to bulk Geofabrik FTP downloads, unzipping and clipping the national database to the local bounding box.
* **Geometric Precision:** Utilized `geopandas.clip()` instead of standard spatial joins (`sjoin`) to physically slice road geometries at the flood boundary, turning a 639-million-cubic-meter calculation error into a physically accurate 49.2-million-cubic-meter engineering proposal.

## 4. The Tech Stack
* `numpy` (Matrix manipulation)
* `pysheds` (Hydrological routing)
* `rasterio` (Spatial array processing)
* `geopandas` / `shapely` (Vector geometry intersection)
* **3 Jupyter Notebooks** containing the core execution logic.

---

## Visual Proof

### Hydrostatic Flood Stages (2m, 5m, 8m)
![Flood Stages](assets/gilgit_hydrostatic_flood_stages.png)

### Earthwork Volume Calculation & Geometric Clipping
![Earthwork Calculation](assets/levee_earthwork_calculation.png)
