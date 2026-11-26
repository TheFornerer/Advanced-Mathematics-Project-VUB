<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>~*~ WARSAW WEATHER & SOLAR PHYSICS ~*~</title>
    <style>
        body {
            background-color: #000080;
            background-image: radial-gradient(#FFFFFF 1px, transparent 1px), radial-gradient(#FFFF00 1.5px, #000080 1.5px);
            background-size: 60px 60px;
            background-position: 0 0, 30px 30px;
            color: #FFFFFF;
            font-family: "Comic Sans MS", "Chalkboard SE", cursive, sans-serif;
            margin: 0;
            padding: 20px;
        }
        table.main-layout {
            width: 820px;
            margin: 0 auto;
            background-color: #000044;
            border: 5px ridge #00FFFF;
            padding: 15px;
        }
        h1 {
            color: #FFFF00;
            text-align: center;
            text-shadow: 3px 3px #FF00FF;
            font-size: 32px;
            margin-bottom: 5px;
        }
        h2 {
            color: #00FF00;
            background-color: #220066;
            border: 2px dashed #FF00FF;
            padding: 5px 10px;
            font-size: 20px;
        }
        .marquee-box {
            background-color: #000000;
            border: 2px inset #C0C0C0;
            color: #00FF00;
            padding: 5px;
            font-weight: bold;
            margin-bottom: 15px;
        }
        .blink {
            animation: blinker 1s linear infinite;
            color: #FF00FF;
            font-weight: bold;
        }
        @keyframes blinker {
            50% { opacity: 0; }
        }
        .nav-bar {
            text-align: center;
            background-color: #C0C0C0;
            color: #000000;
            border: 3px outset #FFFFFF;
            padding: 8px;
            margin-bottom: 20px;
            font-weight: bold;
        }
        .nav-bar a {
            color: #0000FF;
            margin: 0 12px;
            text-decoration: underline;
        }
        .nav-bar a:hover {
            background-color: #FFFF00;
            color: #FF0000;
        }
        .graph-box {
            background-color: #FFFFFF;
            color: #000000;
            border: 4px outset #C0C0C0;
            padding: 12px;
            text-align: center;
            margin: 15px 0;
        }
        .graph-box img {
            max-width: 100%;
            height: auto;
            border: 2px solid #000000;
        }
        .graph-caption {
            font-size: 14px;
            font-weight: bold;
            margin-top: 8px;
            color: #000080;
        }
        table.stats-table {
            width: 100%;
            border-collapse: collapse;
            background-color: #000066;
            margin: 10px 0;
        }
        table.stats-table th, table.stats-table td {
            border: 2px solid #00FFFF;
            padding: 8px;
            text-align: center;
        }
        table.stats-table th {
            background-color: #FF00FF;
            color: #FFFF00;
        }
        .footer {
            text-align: center;
            margin-top: 20px;
            font-size: 13px;
            color: #C0C0C0;
        }
        .counter {
            background-color: #000000;
            color: #FF0000;
            font-family: "Courier New", monospace;
            font-size: 20px;
            font-weight: bold;
            padding: 4px 10px;
            border: 2px inset #808080;
            letter-spacing: 3px;
        }
    </style>
</head>
<body>

<table class="main-layout">
    <tr>
        <td>
            <div class="marquee-box">
                <marquee behavior="scroll" direction="left">
                    *** WELCOME TO MY ADVANCED MATH &amp; PHYSICS PROJECT WEBSITE *** ANALYZING 3,289 DAYS OF NASA POWER DATA FOR WARSAW, POLAND (2015-2024) ***
                </marquee>
            </div>

            <h1>&#9733; WARSAW ENERGY BALANCE &amp; SOLAR PHYSICS &#9733;</h1>
            <p style="text-align: center; color: #00FFFF; margin-top: 0;">
                <i>By: Mateusz Czerniej | VUB Advanced Math Project 2026</i>
            </p>

            <div class="nav-bar">
                [ <a href="#question">Research Question</a> ]
                [ <a href="#data">NASA Dataset</a> ]
                [ <a href="#analysis1">Analysis 1: Regression</a> ]
                [ <a href="#analysis2">Analysis 2: FFT Spectrum</a> ]
                [ <a href="#conclusion">Findings</a> ]
            </div>

            <hr color="#00FFFF" size="3">

            <!-- SECTION 1: RESEARCH QUESTION -->
            <h2 id="question">&#128269; 1. Research Question</h2>
            <p>
                <span class="blink">NEW!</span> Which meteorological variables most strongly drive daily surface air temperature variations in <b>Warsaw, Poland</b> (Pa&#322;ac Kultury i Nauki, 52.23&deg;N, 21.01&deg;E), and what dominant periodic frequencies govern local solar radiation over a 9-year period?
            </p>

            <!-- SECTION 2: DATA -->
            <h2 id="data">&#128225; 2. The NASA POWER Dataset</h2>
            <p>
                Data was downloaded from the <b>NASA POWER Project</b> covering <b>3,289 days</b> (Dec 31, 2015 – Dec 31, 2024). Here are the physical variables analyzed in Python:
            </p>
            <ul>
                <li><b style="color:#FFFF00;">T2M:</b> Daily Mean Air Temperature at 2 Meters (&deg;C)</li>
                <li><b style="color:#FFFF00;">ALLSKY_SFC_SW_DWN:</b> All-Sky Surface Shortwave Downward Irradiance (MJ/m&sup2;/day)</li>
                <li><b style="color:#FFFF00;">RH2M:</b> Relative Humidity at 2 Meters (%)</li>
                <li><b style="color:#FFFF00;">PS:</b> Surface Atmospheric Pressure (kPa)</li>
                <li><b style="color:#FFFF00;">WS2M:</b> Wind Speed at 2 Meters (m/s)</li>
            </ul>

            <!-- SECTION 3: ANALYSIS 1 -->
            <h2 id="analysis1">&#128200; 3. Analysis 1: Multiple Linear Regression (OLS)</h2>
            <p>
                To see how radiative forcing and atmospheric state variables jointly control daily temperature, I ran an Ordinary Least Squares (OLS) multiple linear regression in Python (<b>R&sup2; = 0.622</b>, p &lt; 0.001):
            </p>

            <table class="stats-table">
                <tr>
                    <th>Physical Variable</th>
                    <th>Raw Slope (&beta;)</th>
                    <th>Standardized Effect (&beta;<sub>std</sub>)</th>
                    <th>VIF (Collinearity)</th>
                    <th>Physical Interpretation</th>
                </tr>
                <tr>
                    <td><b>Solar Irradiance</b></td>
                    <td>+0.505 &deg;C / (MJ/m&sup2;)</td>
                    <td style="color:#00FF00;"><b>+0.452</b></td>
                    <td>3.95</td>
                    <td>Strongest positive driver (direct solar heating)</td>
                </tr>
                <tr>
                    <td><b>Relative Humidity</b></td>
                    <td>-0.229 &deg;C / %</td>
                    <td style="color:#FF6666;"><b>-0.330</b></td>
                    <td>3.83</td>
                    <td>Cloud cover &amp; evaporative cooling</td>
                </tr>
                <tr>
                    <td><b>Surface Pressure</b></td>
                    <td>-2.269 &deg;C / kPa</td>
                    <td style="color:#FF6666;"><b>-0.213</b></td>
                    <td>1.11</td>
                    <td>Cold continental winter high-pressure systems</td>
                </tr>
                <tr>
                    <td><b>Wind Speed</b></td>
                    <td>-0.802 &deg;C / (m/s)</td>
                    <td style="color:#FF6666;"><b>-0.114</b></td>
                    <td>1.20</td>
                    <td>Convective heat loss &amp; cold air advection</td>
                </tr>
            </table>

            <!-- IMAGE PLACEHOLDER 1 -->
            <div class="graph-box">
                <!-- REPLACE "regression_analysis.png" WITH YOUR EXACT IMAGE FILE NAME -->
                <img src="regression_analysis.png" alt="Multiple Linear Regression Results Graph">
                <div class="graph-caption">
                    Figure 1: Standardized effect sizes (left) and observed vs. predicted daily temperatures in Warsaw (right).
                </div>
            </div>

            <!-- SECTION 4: ANALYSIS 2 -->
            <h2 id="analysis2">&#9889; 4. Analysis 2: Fast Fourier Transform (FFT)</h2>
            <p>
                Next, I applied a <b>Discrete Fast Fourier Transform (FFT)</b> to the daily solar irradiance time series to transform it from the time domain into the frequency domain and uncover hidden orbital cycles:
            </p>
            <ul>
                <li><b>Dominant Frequency:</b> <span style="color:#00FFFF;">f = 0.002736 cycles/day</span></li>
                <li><b>Extracted Period:</b> <span style="color:#FFFF00;">T = 365.44 days</span> (matches Earth's 365.25-day revolution around the Sun!)</li>
            </ul>

            <!-- IMAGE PLACEHOLDER 2 -->
            <div class="graph-box">
                <!-- REPLACE "fft_solar_spectrum.png" WITH YOUR EXACT IMAGE FILE NAME -->
                <img src="fft_solar_spectrum.png" alt="FFT Solar Irradiance Spectrum Graph">
                <div class="graph-caption">
                    Figure 2: Daily solar irradiance time series (top) and FFT Power Spectral Density showing the 365.4-day orbital peak (bottom).
                </div>
            </div>

            <!-- SECTION 5: CONCLUSION -->
            <h2 id="conclusion">&#127775; 5. Physical Interpretation &amp; Main Findings</h2>
            <p>
                <b>1. Thermodynamics of Warsaw's Surface:</b> Together, solar radiation, humidity, pressure, and wind explain <b>62.2%</b> of all daily temperature variance across 9 years. Incoming shortwave solar radiation is the #1 warming factor, while high humidity and winter high-pressure cells strongly cool the surface.
            </p>
            <p>
                <b>2. Orbital Mechanics in Weather Data:</b> Even though daily weather looks noisy due to clouds, the FFT cleanly isolates Earth's <b>1-year orbital period (365.4 days)</b> as a massive spike in the frequency spectrum.
            </p>

            <hr color="#FF00FF" size="3">

            <div class="footer">
                <p>You are visitor number:</p>
                <span class="counter">001337</span>
                <p style="margin-top: 12px;">
                    Best viewed in Netscape Navigator 4.0 or Internet Explorer 5.0 at 800x600 resolution!<br>
                    <a href="https://github.com/YOUR-USERNAME/YOUR-REPO-NAME" style="color:#00FFFF;">[ Back to My GitHub Repository ]</a>
                </p>
            </div>
        </td>
    </tr>
</table>

</body>
</html>
