# Amazon Delivery Geolocation Analysis

## Overview
This project analyzes Amazon delivery data to visualize the locations of Amazon stores and drop-off points in India using geospatial analysis. It utilizes Geospatial techniques to explore patterns in delivery routes and calculate distances between stores and drop-off locations, and carbon footprint emissions.

I strongly advise checking the code via nbviewer since the folium package is not supported on GitHub. [Link](https://nbviewer.org/github/lucasjmorgado/DA-GEO-Amazon-Logistics/blob/main/Amazon_Geo.ipynb)

### Key Features:
- Transformation of data from Pandas DataFrames to GeoPandas for geospatial analysis.
- Mapping of Amazon store locations and drop-off points.
- Heatmap visualization of drop-off areas to identify delivery concentration.
- Calculation of distances using both geodesic and Google Cloud Platform (GCP) Directions API for accuracy in distance estimation.
- Raw estimation of carbon footprint emissions.

## Project Structure

### Data Sources
- **Amazon Delivery Dataset**: Dataset containing Amazon Stores And Drop Offs -> amazon_delivery.csv -> [Kaggle Dataset](https://www.kaggle.com/datasets/sujalsuthar/amazon-delivery-dataset) 
- **Country Boundaries**: Downloaded from natural earth dataset -> 110m_cultural.zip -> [Natural Earth Data](https://www.naturalearthdata.com/downloads/110m-cultural-vectors/)
- **Indian States Shape File**: Used for visualizing state boundaries in India -> Indian_states.shp -> [Kaggle India GIS Data](https://www.kaggle.com/datasets/nehaprabhavalkar/india-gis-data/data)
- **GCP Directions API**: Used for gathering real world routes for distance estimation -> [GCP Directions API](https://developers.google.com/maps/documentation/directions/overview?hl=pt-br)


### Data Processing
1. **Loading Data**: The Amazon delivery data is read into a Pandas DataFrame and backed up for safety.
2. **Data Cleaning**: 
   - Removed entries with invalid geographical coordinates (latitude and longitude less than 5).
   - Filtered unique locations for Amazon stores and drop-off points.
3. **Geospatial Transformation**: 
   - Converted the cleaned DataFrames to GeoDataFrames and assigned the appropriate Coordinate Reference System (CRS) EPSG:4326 for accurate mapping.
4. **Distance Calculation**: 
   - Used the `geopy` library to calculate geodesic distances between stores and drop-offs.
   - Sampled data to query the GCP Directions API for more accurate route distances and durations.

### Geospatial Visualization
- **Map Visualization**: 
  - Plotted the locations of Amazon stores and drop-off points over a map of India.
  - Displayed states and country boundaries for contextual understanding.
- **Heatmap Visualization**: 
  - Generated heatmaps using Folium to visualize delivery concentration across drop-off locations.

### Key Transformations
- **CRS Transformations**: All GeoDataFrames were assigned the CRS EPSG:4326 to ensure compatibility in mapping.
- **Mapping**: The combination of store and drop-off locations allowed for effective mapping and visual interpretation of delivery patterns.
  
### Distance Analysis
- **Geodesic Distances**: Utilized `geopy` to calculate the minimum distance between stores and drop-offs, providing insights into potential delivery efficiencies.
- **GCP Directions API**: Estimated distances and durations using the GCP API, allowing for a comparison with geodesic distances to understand the accuracy of route predictions.

## Examples
### Map of Amazon Stores and Drop-Off Points
![Amazon Delivery Map](https://raw.githubusercontent.com/lucasjmorgado/DA-GEO-Amazon-Logistics/refs/heads/main/dash0.png) 
- Stores in Yellow and Drop-Off in Red

#### It's also visible in this map the regions of India without Amazon Stores, this could be a good insight for the creation of new stores

### Heatmap of Drop-Off Areas
![Drop-Off Heatmap](https://raw.githubusercontent.com/lucasjmorgado/DA-GEO-Amazon-Logistics/refs/heads/main/dash1.png) 

Check here with an interective Map. [Link](https://nbviewer.org/github/lucasjmorgado/DA-GEO-Amazon-Logistics/blob/main/amazon_dropoff_heatmap.html)

Following the following article, its visible to see the areas with most emission having similarities in our drop off dash:

![CO2 Emissions in India](https://www.researchgate.net/publication/347625606/figure/fig2/AS:975026589278208@1609475862443/Carbon-footprints-per-capita-in-623-districts-in-India-Choropleth-map-showing-the.png) 

### Calculated Distances Overview
- Estimated distances between store and drop-off locations using both methods (geodesic and GCP) along with their median error values.
- I used an average emissions per km for delivery trucks beeing 0.12 kg CO2 per km

#### Results
- Minimum Estimated carbon emissions with Geopy: 46619.30 kg CO2
- Estimated carbon emissions geopy plus median from Api Consumption: 64244.97 kg CO2
  
## Conclusion
This project showcases the power of geospatial analysis in understanding delivery logistics and optimizing routes for Amazon in India. The transformations and visualizations provide insights that can inform operational strategies to improve efficiency and reduce carbon emissions during delivery. 
