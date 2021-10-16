# Methodology
This project aims to produce average day ahead electricity demand forecast for July 2018, given two years of hourly temperature and actual electricity demand data from 2017 to 2018. Since the electricity demand is driven by different factors in summer and winter, for July forecast, only data from May to September (summer season) is taken for training so that data noises coming from the winter season can be avoided. Also, July 2018 data was separated from the training set and used to test the accuracy of the models. Two different day-ahead forecast methods are applied to produce the daily forecast in July 2018 as follows. 
## Method 1:
Forecast the hourly electricity demand on the next day based on calendar and 24-hour temperature features; then sum up to get the daily electricity demand.
## Method 2: 
Choose the current day’s daily electricity demand as the base value; summarize hourly temperature features into daily temperate features; use the current day and the next day’s daily temperate features plus the base value to directly forecast the next day’s daily electricity demand.
# Feature Selection and Feature Engineering
## Method 1:
Hour of the Day, Day of the Week, Day of the Year and Temperature are selected for training. They are engineered as below:

![Alt text](https://github.com/jsun66/Day-Ahead-Electricity-Demand-Forecast/blob/main/Tables%20and%20Figures/Table%201_Feature%20Engineering%20for%20Method%201.PNG)
## Method 2:
Training is performed on the daily scale. For a day, its 24-hour temperature data is summarized into Maximum Temperature, Minimum Temperature, Average Temperature, Temperature Standard Deviation and Degree Days. In addition, the known average demand of the current day is chosen as the base value. A binary feature (0/1) is introduced to represent the different demand patterns during weekdays or weekends.

![Alt text](https://github.com/jsun66/Day-Ahead-Electricity-Demand-Forecast/blob/main/Tables%20and%20Figures/Table%202_Feature%20Engineering%20for%20Method%202.PNG)
# Forecasting Models
Two forecasting models are used and compared: a feedforward neural network (FNN) and an XGBoost (decision-tree-based ensemble learning model). The FNN model has one hidden layer with 4 neurons for method 1 and 9 neurons for method 2. Relu activation function is used. Mean Absolute Error is chosen as the loss function; the XGBoost model uses 150 estimators.
# Results and Discussions
## Trustworthiness of the Results:
X’s temperature instead of Y’s average temperature is given and used to predict Y’s electricity demand. This is based on the assumption that X’s temperature can represent Y’s temperature, which is not the case.
Besides, the day-ahead temperatures are actual temperatures instead of forecasted temperatures. In reality, the day-ahead temperatures are forecasted. There might be an error on the day-ahead temperature forecast itself. 
## Accuracy of the Models:
Mean absolute percentage error (MAPE) is chosen as the accuracy metric of the models. The MAPEs of the two models with the two methods are showing below:

![Alt text](https://github.com/jsun66/Day-Ahead-Electricity-Demand-Forecast/blob/main/Tables%20and%20Figures/Table%203_MAPEs%20for%20Daily%20Electricity%20Demand%20in%20July.PNG)

As can be seen from above, Method 2 produces more accurate forecast than Method 1. FNN performs better for Weekdays and XGBoost performs better for Weekends. 

## Combined Scatterplot and Line Chart

![Alt text](https://github.com/jsun66/Day-Ahead-Electricity-Demand-Forecast/blob/main/Tables%20and%20Figures/Weekday%20Forecast%20Vs.%20Actual%20Demand.png)

