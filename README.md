
## Sea Level Raise Analysis

*The purpose of this analysis was to look at the rate of sea level raise in florida. 
I wanted to see if it is worth it to buy a home in florida, or if flooding will destroy the property in my life time and if so when. 

*This analysis was done using weather station data from different stations spread across Florida evenly using the RNOAA API in R. 
To copy this analysis you will have to get your own personal API key for NOAA at API Key http://www.ncdc.noaa.gov/cdo-web/token. 

*To get the florida station codes go to my github at My github https://github.com/btindol178/Sea-Level-Raise-Analysis- .

Lines signitured with * Step #: means this is the descripton <br> 
Lines signitured with -- after * is the code to be executed in an r- markdown chunk
########################################################################################
########################################################################################
<h3> First Rmarkdown Chunk </h3>

* Step 1: API Key @  http://www.ncdc.noaa.gov/cdo-web/token <br>
-- options(noaakey = "Your API Key Here") <br> 

* Step 2: Small list of stations evenly spaced around states boarder on all sides. We want the station id for RNOAA API calls  <br>
-- florida_stations <- read.csv("florida_stations.csv");colnames(florida_stations)[1] <- "ID" <br>

* Step 3: Bring in leaflet points for plot <br>
-- mappoints <- read.csv("mappoints.csv") <br>

* Step 4: Pick one station for API Testing in florida <br>
-- station1 <- florida_stations$ID[1] <br>

* Step 5: Read in water level data for all of the different stations <br>
-- temp <- read.csv("florida_water_levels_in_feet_final.csv");temp <- temp[-c(1)] <br>

kable(florida_stations) <br> 


![Caption for the picture2.](https://raw.githubusercontent.com/btindol178/Sea-Level-Raise-Analysis-/main/station_ids.JPG)

########################################################################################
########################################################################################
<h3> Locations of the weather stations that feed the NOAA API.we are going to pickevenly spaced stations around state </h3>

* Step 6: Visualize where the stations are located <br>

-- leaflet(data = mappoints) %>%
  addTiles() %>%
  addCircles(lng = mappoints$lonz,
             lat = mappoints$latz,
             popup = mappoints$stationname) %>%
  clearBounds()
  
![Caption for the picture3.](https://raw.githubusercontent.com/btindol178/Sea-Level-Raise-Analysis-/main/leaflet_station_location.JPG)

########################################################################################
########################################################################################
<h3> Example API call from the API </h3>

The api call works by inputting the station name (station id) and a beginning date and ending in yyyymmdd format in numeric form.<br>
The api call releases the data in 5 minute increments and for only 30 day time windows.<br>


* Step 7: Get water level with api call <br>
 -- station1_pull <-coops_search(station_name = station1, begin_date = 20140927,
             end_date = 20140928, product = "water_level", datum = "stnd")
             
* Step 8: Make dataframe and change column names <br> 
station1_pull <- data.frame(station1_pull);colnames(station1_pull)<- c("ID","Station Name", "lat","lon","date time","water level (ft)","standard dev","other data","other data2")

kable(head(station1_pull[c(1:7)]))

![Caption for the picture4.](https://raw.githubusercontent.com/btindol178/Sea-Level-Raise-Analysis-/main/api_dataframe_call.JPG)
########################################################################################
########################################################################################
<h3> Now we need to get two vectors to programatically enter the date range for API calls</h3>

* Step 9: Get a time range for the next 130 months from 2010/01/01
-- datevar <- seq(as.Date("2010/01/01"), by = "month", length.out = 130)

* Step 10: Get a time range for the next 130 months from 2010/02/01
-- datevar2 <- seq(as.Date("2010/02/01"), by = "month", length.out = 130)

* Step 11: St clean up columns for API Call format
-- datedf <- data.frame(start=datevar,end=datevar2);datedf$start <- gsub("-","",datedf$start);datedf$end <- gsub("-","",datedf$end);datedf$start <- as.numeric(datedf$start);datedf$end <- as.numeric(datedf$end)

kable(head(datedf))
########################################################################################
########################################################################################
