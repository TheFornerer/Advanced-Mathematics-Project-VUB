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

## 4. Main Findings

### Dataset Overview (Warsaw: Dec 31, 2015 – Dec 31, 2024)
Across **N = 3,289** daily observations near Pałac Kultury i Nauki (`52.2298° N, 21.0073° E`), daily mean temperature (`T2M`) averaged **9.46 °C** (SD = **9.04 °C**, range **-17.10 °C to 28.56 °C**), and downward shortwave solar irradiance (`ALLSKY_SFC_SW_DWN`) averaged **10.91 MJ/m²/day** (SD = **8.10 MJ/m²/day**, range **0.44 to 30.91 MJ/m²/day**).

### Analysis 1: Multiple Linear Regression (OLS)
The multiple linear regression model predicting daily mean temperature from solar irradiance, relative humidity, surface pressure, and wind speed is statistically significant ($F(4, 3284) = 1352$, $p < 0.001$) and explains **$R^2 = 0.622$ (62.2%)** of the daily temperature variance:

$$T_{2\text{M}} = 251.538 + 0.505\,S_{\downarrow} - 0.229\,\text{RH} - 2.269\,P_s - 0.802\,v_{\text{wind}}$$

* **Solar Irradiance (`ALLSKY_SFC_SW_DWN`):** Raw slope $\beta = +0.505\ ^\circ\text{C}/(\text{MJ/m}^2/\text{day})$, standardized effect **$\beta_{\text{std}} = +0.452$** ($p = 8.96 \times 10^{-94}$). This is the strongest positive driver of surface warming via direct radiative energy input.
* **Relative Humidity (`RH2M`):** Raw slope $\beta = -0.229\ ^\circ\text{C}/\%$, standardized effect **$\beta_{\text{std}} = -0.330$** ($p = 9.79 \times 10^{-54}$). Higher humidity is associated with increased cloud cover (blocking sunlight) and evaporative cooling.
* **Surface Pressure (`PS`):** Raw slope $\beta = -2.269\ ^\circ\text{C}/\text{kPa}$, standardized effect **$\beta_{\text{std}} = -0.213$** ($p = 1.40 \times 10^{-75}$). In Central Europe, strong high-pressure anticyclones frequently bring cold, clear continental air masses in winter.
* **Wind Speed (`WS2M`):** Raw slope $\beta = -0.802\ ^\circ\text{C}/(\text{m/s})$, standardized effect **$\beta_{\text{std}} = -0.114$** ($p = 8.87 \times 10^{-22}$). Stronger winds enhance convective heat transfer away from the surface.
* **Multicollinearity Check (VIF):** All Variance Inflation Factors lie between **1.11 and 3.95** (`SW_DWN`: 3.95, `RH2M`: 3.83, `PS`: 1.11, `WS2M`: 1.20), well below the critical threshold of 5–10, confirming that the predictors do not suffer from problematic multicollinearity.

### Analysis 2: Fast Fourier Transform (FFT Spectral Analysis)
Applying a one-sided Real Discrete Fourier Transform (`rfft`) to the mean-centered solar irradiance series ($N = 3289$ days) reveals a single dominant spectral spike in the Power Spectral Density ($\text{PSD}_{\max} = 82,708.83$):
* **Dominant Frequency:** **$f = 0.002736\text{ cycles/day}$**
* **Corresponding Period:** **$T = \frac{1}{f} = 365.44\text{ days}$**

This matches Earth's **365.25-day orbital revolution** around the Sun (within the discrete frequency bin resolution $\Delta f = 1/3289 \approx 0.000304\text{ cycles/day}$ of a 9-year window), proving that astronomical orbital mechanics govern Warsaw's long-term radiative energy budget despite daily cloud noise.


  
## 5. Repository Structure
```text
├── README.md                                              # Project documentation and findings
├── ‎Index/MathProject.txt                                  # Source code for the website
├── data/
│   └── WarsawNassa_Power_data.csv                         # Raw daily meteorological data from NASA POWER
├── Code
│   └── Math project.ipynb                                 # Colab code
│   └── Advanced-Math-Project_Mateusz_Czerniej_VSCode.txt  # Python script running regression, FFT, and plotting
└── figures/
    ├── regression_analysis.pdf                            # Exported PDF: Standardized coefficients & residuals
    └── fft_solar_spectrum.pdf                             # Exported PDF: Solar irradiance time series & PSD
