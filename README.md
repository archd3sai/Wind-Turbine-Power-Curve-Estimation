# Wind Turbine Power Curve Estimation

The power curve of a wind turbine is a graph that indicates how large the electrical power output will be for the turbine at different 
wind speeds. The figure below shows a sketch about how the power output from a wind turbine varies with steady wind speed.

![power](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/power.png)

The wind turbine power curve shows the relationship between the wind turbine power and hub height wind speed. It essentially captures the wind turbine performance. Hence it plays an important role in condition monitoring and control of wind turbines. Power curves made available by the manufacturers help in estimating the wind energy potential in a candidate site. Accurate models of power curve serve as an important tool in wind power forecasting and aid in wind farm expansion.

### Data
This data is an actual operational dataset of an inland wind turbine which is freely available on [TAMU Library](https://tamucs-my.sharepoint.com/personal/yu-ding_tamu_edu/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fyu%2Dding%5Ftamu%5Fedu%2FDocuments%2FWind%5FSpatio%5FTemporal%5FDataset1%2Ezip&parent=%2Fpersonal%2Fyu%2Dding%5Ftamu%5Fedu%2FDocuments&cid=34459bcf-3ce4-41fb-ac24-c1ccc5fbb0ac). The data were collected from July 30, 2010 through July 31, 2011. The data also has environemntal variables collected from met masts.

The attributes in the file are:

- V: wind speed (m/s),
- D: wind direction (degree),
- rho: air density (kg/m^3),
- I: turbulence intensity,
- Sb: below-hub wind shear,
- y: normalized power output relative to the rated power (%).

### Objective
Objective of this project is to perform independent analysis of the wind-turbine data and predict the power curve of a wind turbine.

### EDA

**Wind Speed Distribution**

![WindDist](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/monthlyWindDist.png)

**Annual Wind Direction**

![AirDir](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/AnnulWindDirection.png)

**Air Density Distribution**

![AirDist](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/AirDist.png)

**Annual Power Curve**

![PowerCurve](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/AnnualPowerCurve.png)

**Correlation Plot**

![corr](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/Corr.png)

### Models

**Polynomial Models**

![poly](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/Poly.png)

**Random Forest Regression Power Curve**

![rf](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/rf.png)

**Gradient Boosting Regression Power Curve**

![gb](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/gb.png)

**XGBoost Regression Power Curve**

![xgb](https://github.com/archd3sai/Wind-Turbine-Power-Curve-Estimation/blob/master/Images/xgb.png)

### Conclusion

Here, for predicting the relative power we have two issues.
- Relative power cannot go outside the range of [0, 100].
- We know that true power curve is non-linear.

To tackle first problem while using regression problem, we can use sigmoid function but it will change the distribution of the response variable. So, to solve both of the problems I used tree based methods which gave me very good results compared to linear regression and lasso regression as they fit a straight line. Results for non linear models can be seen below.

| Model | R-squared Value | Test RMSE |
| --- | --- | --- |
| Polynomial (Degree 4) Regression | 0.92814 | 9.072 |
| Randomforest Regression | 0.99398 | 6.721 |
| Gradient Boost Regression | 0.97786 | 6.631 |
| XGBoost Regression | 0.97755 | 6.404 |


As we can see, in boosting methods bias reduces which improves the test results.


Also, feature importance plots suggests that Wind Speed (Velocity), Wind Direction and Wind Sheer are most important features for predicting the relative power.

