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
* Employed 6 distinct classification models, systematically assessing for overfitting through cross-validation techniques. Subsequently, I computed various evaluation metrics for each model and discerned the optimal choice based on the precision score:

<img width="482" alt="ROC Curve" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/ab9ef452-f96a-4a41-bdfa-a25870db30f6">

<img width="453" alt="Evaluation Metrics" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/05c08250-d426-4774-b35e-176866f58c35">


* Conducted hyper-parameter tuning for Random Forest Classifier, meticulously exploring various settings to ascertain the most effective combination for optimal performance:

<img width="212" alt="Best Parameters Combination" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/399cdad4-1abf-4cca-91d0-f033cef99afd">


* Tested the final model on the test set and got even better results:

<img width="148" alt="Evaluation Metrics (Test Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/f7fc6a0e-a765-4022-928e-2156672640f9">

* Retested the final model on the whole entry dataset and got excellent results:

<img width="114" alt="Evaluation Metrics (Whole Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/d241a528-09e5-41e2-aae6-7eefad4f9f9d">


## :chart_with_upwards_trend: Feature Importance
* Here is a chart showing the sorted contribution of each column to the target column "satisfaction":

<img width="458" alt="Feature Importance" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/86278cb7-adcd-45ad-83b5-7fc209b3b6a5">


## 🎯 Recommendations
* I tweaked the top 5 contributing features' values:
  - Online boarding satisfaction: capped to at least 4.
  - Inflight wifi service satisfaction: increased to at least 4.
  - Type of Travel: changed to Business Travel.
  - Class: changed to Business.
  - Inflight entertainment satisfaction: increased to at least 4.

* Here some recommendations to reduce dissatisfaction rate:
  - Conduct a detailed analysis to identify and address specific pain points.
  - Improve the overall boarding journey, including pre-boarding and boarding.
  - Maintain the premium in-flight services.
  - Enhance services and amenities for non-buisness travelers.
  - Enhance service quality, comfort, and additional amenities for non-business class passengers.
  - Invest in faster and more reliable internet access.
  - Offer different tiers of service to cater to varying customer needs.
  
## 🔨 Conclusion
To effectively enhance overall customer satisfaction, the airline should prioritize simplifying the online check-in process, enhancing services for non-business travelers, investing in reliable inflight WiFi services and entertainment programs. These targeted strategies address key areas that directly impact customer experience and satisfaction, leading to a more satisfied and loyal customer base.
