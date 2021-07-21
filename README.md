
## Sea Level Raise Analysis

*The purpose of this analysis was to look at the rate of sea level raise in florida. 
I wanted to see if it is worth it to buy a home in florida, or if flooding will destroy the property in my life time and if so when. 

*This analysis was done using weather station data from different stations spread across Florida evenly using the RNOAA API in R. 
To copy this analysis you will have to get your own personal API key for NOAA at API Key http://www.ncdc.noaa.gov/cdo-web/token. 

*To get the florida station codes go to my github at My github https://github.com/btindol178/Sea-Level-Raise-Analysis- .

########################################################################################
########################################################################################
<h3> First Rmarkdown Chunk </h3>

* Step 1: API Key @  http://www.ncdc.noaa.gov/cdo-web/token <br>
options(noaakey = "Your API Key Here") <br> 

* Step 2: Small list of stations evenly spaced around states boarder on all sides. We want the station id for RNOAA API calls  <br>
florida_stations <- read.csv("florida_stations.csv");colnames(florida_stations)[1] <- "ID" <br>

* Step 3: Bring in leaflet points for plot <br>
mappoints <- read.csv("mappoints.csv") <br>

* Step 4: Pick one station for API Testing in florida <br>
station1 <- florida_stations$ID[1] <br>

* Step 5: Read in water level data for all of the different stations <br>
temp <- read.csv("florida_water_levels_in_feet_final.csv");temp <- temp[-c(1)] <br>

kable(florida_stations) <br> 
########################################################################################
########################################################################################
<h3> Visualizing what the station ID's look like  </h3>

![Caption for the picture2.](https://raw.githubusercontent.com/btindol178/Sea-Level-Raise-Analysis-/main/station_ids.JPG)

########################################################################################
########################################################################################
<h3> Locations of the weather stations that feed the NOAA API.we are going to pickevenly spaced stations around state </h3>

* Step 6: Visualize where the stations are located <br>

leaflet(data = mappoints) %>%
  addTiles() %>%
  addCircles(lng = mappoints$lonz,
             lat = mappoints$latz,
             popup = mappoints$stationname) %>%
  clearBounds()

