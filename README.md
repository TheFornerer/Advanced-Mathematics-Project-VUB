# Advanced-Mathematics-Project-VUB
# This is Mateusz Czerniejs's Mathematics Project. 

## 1. Research question 
Which meteorological variables most strongly drive daily surface air temperature variations in Warsaw, Poland, and what dominant periodic frequencies govern local solar radiation over a 10-year period?

## 2. All the datasets were obtained from **NASA POWER (Prediction of Worldwide Energy Resources)** 
The data are for Warsaw, the capital city of Poland (latitude:  52.2298,   longitude: 21.0073), covering the 9 years from **December 31, 2015 to December 31, 2024**.

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

## Analysis

# Analysis 1: Multiple Linear Regression (Energy Balance Drivers)
To quantify how radiative forcing and atmospheric state variables jointly determine daily surface temperature, we fit an Ordinary Least Squares (OLS) multiple linear regression model:

$$T_{2\text{M}} = \beta_0 + \beta_1 S_{\downarrow} + \beta_2 \text{RH} + \beta_3 P_s + \beta_4 v_{\text{wind}} + \epsilon$$

* Variables were standardized ($z$-scores) to compare the relative physical effect size ($\beta_i$) of predictors measured in different units.
* Variance Inflation Factors (VIF) were computed to verify the absence of severe multicollinearity among meteorological predictors.

### Analysis 2: Fast Fourier Transform (Spectral Decomposition)
To analyse cyclical radiative forcing in the frequency domain, a Discrete Fourier Transform (DFT) was applied to the daily solar irradiance time series $S_{\downarrow}[n]$ ($N = 3653$ days) after removing the mean (DC component):

$$X[k] = \sum_{n=0}^{N-1} \left(S_{\downarrow}[n] - \bar{S}_{\downarrow}\right) e^{-i 2\pi k n / N}$$

* The Power Spectral Density (PSD) was computed to identify dominant oscillation periods ($T = 1/f$) and harmonic frequencies.

## Main Findings
* **Regression Results:** The multiple linear regression model explains **$R^2 = [0.XX]$** ($p < 0.001$) of the variance in daily surface temperature. Downward shortwave solar irradiance ($S_{\downarrow}$) is the strongest positive driver ($\beta_{\text{std}} = [X.XX]$), while relative humidity exhibits a strong negative correlation ($\beta_{\text{std}} = [-X.XX]$) due to cloud cover and evaporative cooling effects.
* **Spectral Results:** The FFT periodogram reveals a sharp, dominant spectral peak at **$f \approx 0.00274\text{ days}^{-1}$**, corresponding to a period of **$T \approx 365.3\text{ days}$** (Earth's orbital revolution around the Sun), along with a minor secondary harmonic at **$T \approx 182.6\text{ days}$** resulting from the asymmetric seasonal duration of summer vs. winter insolation at $50.85^\circ\text{N}$ latitude.*


  
## 5. Repository Structure
```text
├── README.md                              # Project documentation and findings
├── index.html                             # Source code for the presentation website
├── style.css                              # Styling for the presentation website
├── data/
│   └── brussels_weather_2016_2025.csv     # Raw daily meteorological data from NASA POWER
├── scripts/
│   └── analysis.py                        # Python script running regression, FFT, and plotting
└── figures/
    ├── regression_analysis.pdf            # Exported PDF: Standardized coefficients & residuals
    └── fft_solar_spectrum.pdf             # Exported PDF: Solar irradiance time series & PSD
