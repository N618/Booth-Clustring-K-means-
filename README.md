# 📌 Booth Clustering and Validation for Assembly Constituency Analysis

This notebook provides a complete geospatial pipeline for **booth-level clustering**, **spatial containment validation**, **interactive visualization**, and **representative booth pair selection** for field analysis across Indian Assembly Constituencies (ACs).

---

## 📁 Input Data

* **Booth Shapefile**: Geospatial point data (e.g., `andhrapradesh.booth.shp`)
* **AC Boundary Shapefile**: Used for spatial validation
* *(Optional)* Excel/CSV output paths for storing results

---

## ⚙️ Libraries Used

* `pandas`, `numpy`: Data operations
* `geopandas`, `shapely`: Geospatial handling
* `folium`: Interactive mapping
* `json`: GeoJSON formatting
* `sklearn`: KMeans clustering
* `geopy`: Geodesic distance calculations

---

## 🚦 Workflow Overview

### 1. **Load and Preprocess Booth Data**

* Load booth shapefiles using `GeoPandas`
* Filter specific ACs
* Remove duplicate geometries
* Extract `lat` and `lng` from booth point geometries

---

### 2. **Geospatial Validation: Booth Inside AC**

* Create temporary `Point` objects for each booth
* Check if each booth lies **within its AC boundary**
* Add a `'status'` column to label each booth as `'inside'` or `'outside'`

✅ Helps catch spatial data errors or misalignments.

---

### 3. **Booth Clustering Using KMeans**

* For each AC:

  * Apply KMeans clustering (e.g., 12 clusters)
  * Use latitude and longitude as features
  * Assign cluster labels to each booth

✅ Enables **grouping nearby booths** for sampling or coverage planning.

---

### 4. **Interactive Mapping with Folium**

* For each AC:

  * Render AC boundary and clustered booths on a **Folium map**
  * Save each as a standalone HTML file

✅ Interactive maps for **visual validation**, review, or sharing.

---

### 5. **Select Representative Booth Pairs by Cluster**

* For each cluster within each AC:

  * If only 1 booth: include as-is with `NaN` for second point
  * If multiple booths:

    * Calculate **pairwise great-circle distances**
    * Select a pair with **distance between 500m and 5000m**, if available
    * If not, fall back to first two booths
* Result is a table of **selected booth pairs per cluster** with distance in meters

✅ Ensures representative **booth-pair selection** for audits, polling experiments, or targeted interventions.

---

## ✅ Setup Instructions

Install the required libraries:

```bash
pip install pandas geopandas shapely folium scikit-learn geopy
```

Ensure that all shapefile components (`.shp`, `.shx`, `.dbf`, etc.) are in the appropriate directory.

---

## 📦 Output Files

* `Telengana_ac##_sample_maps.html`: Interactive maps with AC boundaries and booths
* `selected_pairs_df`: Final DataFrame of selected booth pairs with distances
* Updated booth dataset with:

  * `lat`, `lng`: Coordinates
  * `status`: `'inside'` or `'outside'`
  * `cluster`: Cluster number from KMeans
