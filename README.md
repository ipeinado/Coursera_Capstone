# Capstone Project - The Battle of Neighborhoods

This repo contains a notebook and some related data for comparing different neighborhoods in the city of **Madrid**.

## [1. Problem and Background](#problem)

During the Coursera Applied Data Science Capstone Course, we have used Python and the Foursquare API to explore New York City and Toronto, segmenting and clustering their neighborhoods based on geographical information taken from the Foursquare API. In this project, we will make something similar with data from the city of **Madrid**, in Spain.

Madrid is the capital of Spain. The city of Madrid has a population of around **3.3 million** inhabitants, and a metropolitan area population of around **6.5 million**, many of which work within the city limits. Madrid is the economic capital of Spain, and although it is not the main touristic destination of Spain (Mallorca or Barcelona welcome more tourists per year), it is the main economic, administrative and business hub of the country.

As any other big city, Madrid is a very hetereogeneous city. This project aims to explore the different neighborhoods based on data obtained from the FourSquare API, and to figure out the best place in the city to open a restaurant. In order to get to a conclusion, we will investigate:

* The number of restaurants per neighborhood (including restaurants per inhabitant)
* The most common type of restaurants in each neighborhood
* The price range of restaurantes in each neighborhood (given the 4 categories of restaurants in Foursquare)
* Finally, we will explore other relevant data.

## [2. Data](#data)
The city of Madrid comprises 21 districts and 131 neighborhoods. 

### Districts and Neighborhoods

 In order to get information about the venues in each neighborhood from the Foursquare API, we need to get info about (1) the name of all neighborhoods in Madrid, and (2) the geographical coordinates of each neighborhood. The municipality of Madrid shares open data about the city, in order to support interested citizens in the development of new applications, studies, analysis or research. Data can be found in [this website](https://datos.madrid.es/portal/site/egob). Madrid's Open Data Portal does not provide a dataset with this information; therefore, we will need to use a geolocation service to get the coordinates for each neighborhood. From the Open Data Portal, we will use the following datasets:
 * [Madrid neighborhoods](https://datos.madrid.es/egob/catalogo/200078-1-distritos-barrios.csv) (area and perimeter)
 * [Madrid districts](https://datos.madrid.es/egob/catalogo/200078-4-distritos-barrios.csv)
 * [Madrid districts](https://datos.madrid.es/egob/catalogo/200078-9-distritos-barrios.zip) (in geographical format, .shp)
 * [Madrid neighborhoods](https://datos.madrid.es/egob/catalogo/200078-10-distritos-barrios.zip) (in geopraphical format .shp)

 ### Geographical Information
 
 We will use then use the Nominatim library to get the geographical coordinates (latitude and longitude) for each neighborhood. These coordinates will be used in the requests to the Foursquare API. 
 
 ### Using the Foursquare API
 
 We will expore the recommended venues near the central location of each neighborhood, using the ```explore``` API (https://api.foursquare.com/v2/venues/explore):
 1. First, we will make a generic request in order to get information about all venues. With this information, we can get an idea of the total number of places in a neighborhood, as well as their types.
 2. Then, we will make a second batch of requests looking for recommended venues based on price for each neighborhood. Currently the valid range of price points are [1, 2, 3, 4], 1 being the least expensive, 4 being the most expensive. Therefore, we will make 4 requests per neighborhood. This will help us get an idea of the number of venues per price range per neighborhood.

### Other information to explore
* [Census of venues, their activities and terraces (December 2020)](https://datos.madrid.es/egob/catalogo/209548-252-censo-locales-historico.csv), a comprehensive listing of all venues and their activities in Madrid, can be used to get extra information that cannot be gathered via the Foursquare API.
* [*Padron* municipal (register of inhabitants per neighborhood, December 2020)](https://datos.madrid.es/egob/catalogo/209163-172-padron-municipal-historico.csv), in case we want to get extra information regarding the number of inhabitants per neighborhood.

### Visual representation
 We will use the geographical format to present some information about the neighborhoods. In order to create the Choropleth maps with [Folium](https://python-visualization.github.io/folium/), we need a .geojson file. CartoDB offers geojson files both for neighborhoods and districts:
 * [Madrid Neighborhoods (geojson)](https://davideme.carto.com/tables/barrios/public/map)
 * [Madrid districts (geojson)](https://team.carto.com/u/jsanz/tables/distritos/public)