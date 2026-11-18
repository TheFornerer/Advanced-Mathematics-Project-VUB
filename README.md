# Advanced-Mathematics-Project-VUB
# This is Mateusz Czerniejs's Mathematics Project. 

## 1. Research question 
Which meteorological variables most strongly drive daily surface air temperature variations in Warsaw, Poland, and what dominant periodic frequencies govern local solar radiation over a 10-year period?

## 2. All the datasets were obtained from **NASA POWER (Prediction of Worldwide Energy Resources)** 
The data are for Warsaw, the capital city of Poland (latitude:  52.2298,   longitude: 21.0073), covering the 10 years from **December 31, 2015 to December 31, 2025**.

## 3. The cvs file of the dataset can be located in this repository under the name of " " 
# I used these variables to model how strongly they derive by using: 
  * T2M: Daily Mean Temperature at 2 Meters 
  * ALLSKY_SFC_SW_DWN: All-Sky Surface Shortwave Downward Irradiance 
  * RH2M: Relative Humidity at 2 Meters 
  * PS: Surface Pressure 
  * WS2M: Wind Speed at 2 Meters

To reproduce the dataset manually, head to the NASA Data Power viewer at this address :( https://power.larc.nasa.gov/data-access-viewer/ ), select the single-point with standard resolution. Then make sure you are on the Agroclimatology community. Then set the daily temporal resolution for (latitude:  52.2298,   longitude: 21.0073). Make sure to be within the 10-year time frame, export the parameters listed above, and then export them as CSVs.

## 4. Methodology & Mathematical Analyses
All data processing and statistical modelling were performed in Python with these extra imports: pandas, numpy, scipy, statsmodels, and matplotlib.
