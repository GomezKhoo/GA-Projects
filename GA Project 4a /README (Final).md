# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 4: West Nile Virus

### Project Objectives:

Due to the recent epidemic of West Nile Virus in the Windy City, the Department of Public Health has set up a surveillance and control system in hope to learn something from the mosquito population. In order to curb the epidemic, pesticides will have to be deployed through the city. A more accurate method of predicting outbreaks of West Nile virus in mosquitos will help the City of Chicago and CPHD more efficiently and effectively allocate resources towards preventing transmission of this potentially deadly virus. 

The Department of Public Health has engaged us, an independent Data Science company, to derive an effective plan using data science methods to deploy these pesiticides. We would have to make recommendations on where pesticides should be sprayed and the cost vs benefit of deploying these pesticides.

---

### Background:

West Nile virus is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death.

In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

---

### Datasets Used:

For the purpose of the analysis, we are provided with the `train`, `test`, `spray` and `weather` datasets. 

The `train` dataset consists of data from 2007, 2009, 2011 and 2013. We will be using this dataset for model building purposes. The `test` dataset consists of data from 2008, 2010, 2012 and 2014. We will be predicting the mosquito population information using this dataset. 

The `spray` dataset consists of Geographic Information Mapping (GIS) data for the spray efforts in 2011 and 2013. Spraying can reduce the number of mosquitos in the area, and therefore might eliminate the appearance of West Nile virus. 

The `weather` dataset consists of weather conditions of 2007 to 2014, during the months of the tests. It is believed that hot and dry conditions are more favorable for West Nile virus than cold and wet. 

Please refer to data dictionaries below for the full infomation found in the datasets.

---

### Data Dictionary:

Three main datasets were used in this project. The data dictionaries of the datasets can be found below.

<br>**Dataset name: `train`**
<br>This dataset contains data from 2007, 2009, 2011, and 2013.

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|date|datetime|train| Date that the WNV test is performed.|
|address|string|train| Approximate address of the location of trap. This is used to send to the GeoCoder. |
|species|string|train| The species of mosquitos.|
|block|integer|train| Block number of address.|
|street|string|train| Street name.|
|trap|string|train| Id of the trap.|
|addressnumberandstreet|string|train| Approximate address returned from GeoCoder.|
|latitude|float|train| Latitude returned from GeoCoder.|
|longitude|float|train| Longitude returned from GeoCoder.|
|addressaccuracy|integer|train| Accuracy returned from GeoCoder.|
|nummosquitos|integer|train| Number of mosquitoes caught in this trap.|
|wnvpresent|integer|train| Whether West Nile Virus was present in these mosquitos. 1 means WNV is present, and 0 means not present.|

<br>**Dataset name: `test`**
<br>This dataset contains data from 2007, 2009, 2011, and 2013.

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|id|string|test| The id of the record.|
|date|datetime|test| Date that the WNV test is performed.|
|address|string|test| Approximate address of the location of trap. This is used to send to the GeoCoder. |
|species|string|test| The species of mosquitos.|
|block|integer|test| Block number of address.|
|street|string|test| Street name.|
|trap|string|test| Id of the trap.|
|addressnumberandstreet|*string*|test| Approximate address returned from GeoCoder.|
|latitude|float|test| Latitude returned from GeoCoder.|
|longitude|float|test| Longitude returned from GeoCoder.|
|addressaccuracy|integer|test| Accuracy returned from GeoCoder.|

<br>**Dataset name: `spray`**
<br>This dataset contains the GIS data of spraying efforts in 2011 and 2013.

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|date|datetime|spray|The date and time of the spray.|
|time|string|spray|The date and time of the spray.|
|Latitude|string|spray|The Latitude of the spray.|
|Longitude|string|spray|The Longitude of the spray.|


<br>**Dataset name: `weather`**
<br>This dataset contains the weather data from 2007 to 2014.

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|station|integer|weather|Station ID.|
|date|datetime|weather|Date of the weather data.|
|tmax|integer|weather|Maximum temperature in Degrees Fahrenheit.|
|tmin|integer|weather|Minimum temperature in Degrees Fahrenheit.|
|tavg|integer|weather|Average temperature in Degrees Fahrenheit.|
|depart|integer|weather|Departure from normal temperature in Degrees Fahrenheit.|
|dewpoint|integer|weather|Average dew point in Degrees Fahrenheit.|
|wetbulb|integer|weather|Average wet bulb in Degrees Fahrenheit.|
|heat|integer|weather|Absolute temperature difference of average temperature (Tavg) from base 65 deg Fahrenheit for Tavg >=65|
|cool|integer|weather|Absolute temperature difference of average temperature (Tavg) from base 65 deg Fahrenheit for Tavg <=65|
|sunrise|string|weather|Sunrise timing in 24H format. (Calculated, not observed)|
|sunset|string|weather|Sunset timing in 24H format. (Calculated, not observed)|
|codesum|string|weather|Significant weather types.|
|depth|integer|weather|Snowfall in inches.|
|water1|integer|weather|Amount of water equivalent from melted snow.|
|snowfall|float|weather|Snowfall in precipitation.|
|preciptotal|float|weather|Water equivalent(Inches & Hundredths(2400 Local Standard Time). Rainfall & melted snow.|
|stnpressure|float|weather|Average station pressure. Inches of HG.|
|sealevel|float|weather|Average sea level pressure. Inches of HG.|
|resultspeed|float|weather|Resultant wind speed. Speed in miles per hour.|
|resultdir|float|weather|Resultant wind direction. To tens of degrees. Whole degrees.|
|avgspeed|float|weather|Average wind speed. Speed in miles per hour.|

---

### Key takeaways from the project:
1. 3 out of the 7 mosquito species constituted all observed presences of the WNV.

2. The features: longitude, species, and r_humid are the top 3 variables used by our model to predict the presence of WNV.

3. Although the 2013 spraying data shows some effectiveness in controlling the virus, we are unable to directly compare cause and effect but we can take suitable measures. These measures are covered in our recommendations below.

---

### Recommendations:
1. Spray locations:
- Since costs are proportional to area, we would recommend to target community areas in Chicago that are predicted to have a high probability of the virus and more heavily densed.
2. Educational Campaigns:
- Run campaigns to educate the public on best practices for prevention and that the most effective approach to combat such viruses is a joint effort between the community and government.
3. Alert system:
- Inform residents in areas when up-to-date data suggests a higher likelihood of the virus to take necessary measures to protect themselves.