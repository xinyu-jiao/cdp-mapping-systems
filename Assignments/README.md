# Grocery Routes and Urban Exploration in Madison

This project aims to explore the **grocery shopping experience in Madison** by documenting and analyzing my personal travel routes to various food stores over a week. Through this process, I hope to reveal the differences in accessibility based on various modes of transportation (walking, bus, car) and to digitize my personal "mental map" of the city.

## Personal Narrative

I once lived near downtown Madison in this June, an area that, while vibrant, is not within walking distance of any large chain supermarkets. This makes acquiring fresh and affordable food an activity that requires advance planning. To meet my daily needs, I schedule several shopping trips each week, relying on walking, the city bus, and occasionally ride-sharing services or a borrowed car. This experience forms the personal lens through which I explore the city's retail geography.

My daily shopping experience is more than just a simple point-to-point movement; it also reflects the impact of urban planning and the public transportation system on residents' lives. By visualizing my personal data, I hope to gain a more intuitive understanding of these complex interrelationships.

## Dataset Created

I created a **GeoJSON** file named `GroceryMadison.geojson`, which records all my shopping trips for one week.

- **Data Type**: The dataset contains a series of **Point** data, where each point represents a store I visited.
- **Data Attributes**: Each point includes the following information:
  - `name`: The name of the store
  - `visit_date`: The date of the visit
  - `mode`: The mode of transport used for the trip (e.g., walk, bus, car)
- **Creation Tool**: I used [geojson.io](https://geojson.io/) to manually create and edit this dataset, accurately marking the geographic location and relevant attributes for each store.

## Proposed Related Dataset

To more comprehensively analyze my travel paths, I plan to relate my personal data with the following key dataset:

1. **Madison Metro Transit (GTFS)**
   - **Link**: [Madison Metro Transit GTFS Data](https://www.google.com/search?q=https://www.cityofmadison.com/metro/data)
   - **Description**: This is the open data for Madison's bus system, containing all bus routes, stops, and schedules. This dataset allows for a precise analysis of the network coverage for travel via public transportation. My script already includes the initial code to load and cache this data.

## Data Integration Workflow

My goal is to integrate my personal data with public transit data to visually reveal the relationship between my shopping routes and the city's public transportation system. The proposed workflow is as follows:

1. **Data Loading and Preparation**
   - Load the shopping destination data from `GroceryMadison.geojson` and my home coordinates from `home.txt`.
   - Utilize the **Google Maps Directions API** to generate precise route data (LineStrings) for each shopping trip, based on the recorded mode of transport (walk, bus, car), simulating the same routes I've travelled with.
   - Load Madison's **GTFS** data to generate a city-wide bus route network layer.
2. **Analysis and Visualization**
   - Create **walking-distance buffers** at different radii (e.g., 0.5 miles and 1 mile) centered on my home address to assess the accessibility of retail locations on foot.
   - Use the `folium` library to create an interactive map that integrates my home location, shopping destinations, travel routes, walking buffers, and the city-wide bus network layer.
   - Finally, generate an HTML file named `MadisonGroceryVisit.html` to comprehensively display the analysis results.

## Proposed Future Work

Building on the current project, future work could incorporate more complex socioeconomic data for a deeper analysis of urban accessibility.

A key direction is **Food Desert Analysis**. This would help to understand if my personal shopping experience is connected to broader issues of urban food inequality. Specific steps could include:

1. **Integrate Food Desert Data**: Introduce data from the **USDA Food Access Research Atlas**. This dataset provides information on low-income and low-access census tracts.
2. **Spatial Join Analysis**: Spatially join the food desert data with Madison's geographic data to identify and map officially designated "food deserts."
3. **Overlay Analysis**: Overlay my home location, shopping destinations, and travel routes with the food desert layer. This would visually reveal:
   - Whether my residence is located within or on the edge of a food desert.
   - Whether I need to travel through food desert areas to access fresh food.
   - The role the public transportation network plays in connecting residential areas to food stores in non-desert areas.

Through such an expanded analysis, this project could evolve from a personal narrative into a case study on urban food equity.