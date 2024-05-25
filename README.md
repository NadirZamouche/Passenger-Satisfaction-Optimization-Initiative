# Passenger-Satisfaction-Optimization-Initiative

![787-type1-2-stills-shot01](https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/d28cdd1c-a144-42a0-a330-a55c0de11ce7)

## 📝 Description
Aerovia Airlines ✈️, an internationally renowned airline, is determined to offer its passengers an exceptional travel experience. To achieve this goal, the company has decided to launch an in-depth analysis of the data collected from its customers. 

Project goal:
- Objective: Identify and resolve issues affecting service quality, focusing on the main causes of passenger dissatisfaction.
- Task: Analyze the passenger experience data and determine the areas requiring improvement, and to propose concrete solutions to increase customer satisfaction.

## ⏳ Dataset
The satisfaction.csv file contains the following information:
- Gender: Gender of passengers ( Female, Male).
- Customer Type: (Loyal customer, disloyal customer).
- Age.
- Type of Travel: Purpose of passengers' trip (Personal Travel, Business Travel).
- Class: Passengers' class of travel on the aircraft (Business, Eco, Eco Plus).
- Flight distance.
- Inflight wifi service: Level of wifi service satisfaction (0:Not Applicable;1-5).
- Departure/ Arrival time convenient: Level of satisfaction with convenience of departure/ arrival times.
- Ease of Online booking: Level of satisfaction with online booking.
- Gate location: Level of satisfaction with gate location.
- Food and drink: Food and drink satisfaction level.
- Online boarding: Level of satisfaction with online boarding.
- Seat comfort: Level of satisfaction with seat comfort.
- Inflight entertainment: Level of satisfaction with in-flight entertainment.
- On-board service: Level of satisfaction with on-board service.
- Leg Room Service: Level of satisfaction with leg room.
- Baggage handling: Level of satisfaction with baggage handling.
- Check-in service: Level of satisfaction with check-in service.
- Inflight service: Level of satisfaction with in-flight service.
- Cleanliness: Level of satisfaction with cleanliness.
- Departure delay in Minutes: Minutes of delay on departure.
- Arrival Delay in Minutes: Minutes of delay on arrival.
- Satisfaction: Level of airline satisfaction (Satisfaction, neural or dissatisfaction).

## :mag: Data Cleansing
* Filled missing values using mean strategy.
* Changed certain satisfaction columns where their values were equal to 0 to 3 (mean) as clarified in the specifications (0: Not Applicable; 1-5).
* Dropped rows where their object column values were missing since they only represented a very small portion of the whole data around 2%.
* Deleted columns where their values were sequentially assigned numbers, such as IDs.
* Merged 'Departure Delay in Minutes' and 'Arrival Delay in Minutes' into one column called 'Total Delay' by adding their values.
* Applied label (binary) and ordinal encoders to the appropriate object columns.
* Created boxplots for each column to check for outliers. Here is a box plot for Flight Distance column:

<img width="547" alt="Box Plot for Flight Distance" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/940ac44e-76b3-479e-8201-8a6efb22c8a0">


* Ploted histograms for each column to see if the data is balanced or not:

<img width="750" alt="Histograms" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/58d7c6dd-d740-4d79-bc1c-0a5cb7551966">


* Ploted heat map for correlation matrix:

<img width="684" alt="Correlation Matrix" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/70088bc4-26f4-424b-a427-df928af540fb">

The correlation Matrix shows that there is:
- Moderate negative relationship between "Type of travel" and the target column "Satisfaction" (-0.45): meaning that when "Type of travel" is 0 (Business travel) the passenger is satisfied and when it's 1 (Personal travel) their satisfaction is often neutral or dissatisfied.
- Moderate positive relationship between "Class, Online boarding" and the target column "satisfaction" (0.49 & 0.55).
Weak positive relationship between "Inflight entertainement, Seat comfort, On-boarding service, Leg room service & Cleanliness" and the target column "satisfaction" (0.4, 0.35, 0.32, 0.31 & 0.31 respectively).

* Applied the standard scaler since there were outliers within the data (as show in box plot).
* Created the data pipeline encompassing all data preprocesing steps for later use in modeling.

## :desktop_computer:	Modeling
* Utilizing the previous data pipeline. I partitioned the data into two sets: 75% designated for training and 25% allocated for testing. Also, I used the StratifiedShuffleSplit to ensure representative stratification across the dataset.
* Employed 6 distinct classification models, systematically assessing for overfitting through cross-validation techniques. Subsequently, I computed various evaluation metrics for each model and discerned the optimal choice based on the precision score.

<img width="648" alt="ROC Curve" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/7e6dc0aa-5c78-4637-86d1-fc6a2f0f09fa">

<img width="441" alt="Evaluation Metrics" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/3f0b6166-7dc0-4c65-b4c3-b51bed0d0243">

* Conducted hyper-parameter tuning for eXtream Gradient Boosting Classifier, meticulously exploring various settings to ascertain the most effective combination for optimal performance.

<img width="279" alt="Best Parameters Combination" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/a69d3508-176c-46d5-b636-1d59cd2f3451">


* Tested the final model on the test set and got even better results :

<img width="137" alt="Evaluation Metrics (Test Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/b377805a-e4db-43d5-b9ac-194ccfb4d387">


* Retested the final model on the whole entry dataset and got excellent results:

<img width="123" alt="Evaluation Metrics Whole Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/bf8ed98f-cb61-495a-a771-e358d22fb2fc">

## :chart_with_upwards_trend: Feature Importance
* Here is a chart showing the sorted contribution of each column to the target column "satisfaction":

<img width="640" alt="Feature Importance" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/a94f7ce0-f0f7-4f94-ab42-4ce7010b7c28">
