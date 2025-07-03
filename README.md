# Booth Clustering for Assembly Selection

This Jupyter Notebook is designed for performing **booth-level clustering** using geospatial data across different assembly constituencies. It is specifically tailored to process shapefiles representing polling booths and apply clustering techniques to select representative booths from a region (e.g., Telangana, Andhra Pradesh).

## 📁 Input Data

The notebook uses the following input:

* **Shapefile** containing booth locations:

  ```
  andhrapradesh.booth.shp
  ```

  This file contains geospatial point data representing booth locations, along with attributes like assembly constituency (`ac`) and other metadata.

## ⚙️ Key Libraries Used

* `pandas` & `numpy`: Data manipulation.
* `geopandas`: Handling geospatial vector data.
* `shapely`: For geometry operations.
* `folium`: For map visualization.

## 🚦 Workflow Overview

1. **Load Booth Shapefile**
   Load and visualize booth location data from a `.shp` file.

2. **Filter by Constituency**
   Select booths from a list of assembly constituencies (e.g., 1 to 119).

3. **Geometry Cleanup**
   Remove duplicate booth geometries.

4. **Extract Coordinates**
   Compute latitude and longitude from the booth's `Point` geometry.

5. *(Optional Next Steps)*
   * Apply a clustering algorithm (e.g., KMeans, DBSCAN) based on spatial proximity.
   * Visualize clustered booths using `folium` maps.
   * Select a representative booth from each cluster.

## 📌 Output

The expected output is:

* A filtered and cleaned GeoDataFrame of booth locations.
* Optionally, clustered booth groups with geographic centroids or sample booths for further analysis or on-ground deployment.

## ✅ Prerequisites

Before running the notebook, make sure you have the following installed:

```bash
pip install pandas geopandas shapely folium
```

Also, ensure that the shapefile and its associated files (.shx, .dbf, etc.) are correctly located at the path specified in the notebook.
