
## Sea Level Raise Analysis

*The purpose of this analysis was to look at the rate of sea level raise in florida. 
I wanted to see if it is worth it to buy a home in florida, or if flooding will destroy the property in my life time and if so when. 

*This analysis was done using weather station data from different stations spread across Florida evenly using the RNOAA API in R. 
To copy this analysis you will have to get your own personal API key for NOAA at API Key http://www.ncdc.noaa.gov/cdo-web/token. 

*To get the florida station codes go to my github at My github https://github.com/btindol178/Sea-Level-Raise-Analysis- .

###################################################################
###################################################################
* API Key @  http://www.ncdc.noaa.gov/cdo-web/token <br>
options(noaakey = "Your API Key Here") <br> 

* small list of stations evenly spaced around states boarder on all sides <br>
* we want the station id for RNOAA API calls  <br>
florida_stations <- read.csv("florida_stations.csv");colnames(florida_stations)[1] <- "ID" <br>

* Bring in leaflet points for plot <br>
mappoints <- read.csv("mappoints.csv") <br>

* pick one station for API Testing in florida <br>
station1 <- florida_stations$ID[1] <br>

* read in water level data for all of the different stations <br>
temp <- read.csv("florida_water_levels_in_feet_final.csv");temp <- temp[-c(1)] <br>

kable(florida_stations) <br> 
###################################################################
###################################################################




![Caption for the picture.](https://raw.githubusercontent.com/btindol178/Sea-Level-Raise-Analysis-/main/st_peters_1_foot.JPG)


