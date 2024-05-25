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

<img width="648" alt="ROC Curve" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/7e6dc0aa-5c78-4637-86d1-fc6a2f0f09fa">

<img width="441" alt="Evaluation Metrics" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/3f0b6166-7dc0-4c65-b4c3-b51bed0d0243">

* Conducted hyper-parameter tuning for eXtream Gradient Boosting Classifier, meticulously exploring various settings to ascertain the most effective combination for optimal performance:

<img width="279" alt="Best Parameters Combination" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/a69d3508-176c-46d5-b636-1d59cd2f3451">


* Tested the final model on the test set and got even better results:

<img width="137" alt="Evaluation Metrics (Test Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/b377805a-e4db-43d5-b9ac-194ccfb4d387">


* Retested the final model on the whole entry dataset and got excellent results:

<img width="123" alt="Evaluation Metrics Whole Set)" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/bf8ed98f-cb61-495a-a771-e358d22fb2fc">

## :chart_with_upwards_trend: Feature Importance
* Here is a chart showing the sorted contribution of each column to the target column "satisfaction":

<img width="640" alt="Feature Importance" src="https://github.com/NadirZamouche/Passenger-Satisfaction-Optimization-Initiative/assets/95188070/a94f7ce0-f0f7-4f94-ab42-4ce7010b7c28">

## 🎯 Recommendations
* I tweaked the top 5 contributing features' values:
  - AVG_Work_Time: capped at 8 Hours (turnover count: 711 -> 703).
  - Age: increased it by 10 years (turnover count: 711 -> 633).
  - TotalWorkingYears: increased it by 5 years (turnover count: 711 -> 686).
  - MonthlyIncome: increased it by 20.000 Indian Rupees that's $240 "March 2024" (turnover count: 711 -> 695).
  - YearsAtCompany: increased it by 10 years (turnover count: 711 -> 684).
  - ALL combined turnover count went from 711 to 119.

* Here some recommendations to reduce turnover rate:
  - Avoid crunch time at any cost.
  - Consider offering flexible working hours to further support employee well-being and retention.
  - Communicate transparently with employees about the reasons behind the adjustment in working hours.
  - Gather feedback from employees to understand how the adjusted working hours have impacted their satisfaction.
  - Prioritize retention efforts for younger employees to mitigate turnover risks.
  - Develop robust onboarding and career advancement programs for early-career professionals.
  - Cultivate a supportive work environment that addresses the needs and aspirations of younger talent.
  - Strengthen onboarding programs to effectively integrate new employees into the company culture and workflows, fostering a sense of belonging and commitment from the outset.
  - Develop comprehensive career pathing initiatives that provide clear trajectories for professional growth and advancement within the organization. This can incentivize employees to stay long-term by offering opportunities for skill development and career progression.
  - Implement mentorship programs to provide guidance and support to employees at various stages of their careers. Pairing less experienced employees with seasoned mentors can offer valuable insights, facilitate knowledge transfer, and enhance job satisfaction, thereby reducing turnover rates.
  - Review and adjust compensation structures to ensure they remain competitive within the industry and region, aiming to attract and retain top talent.
  - Offer additional benefits and perks aligned with employee preferences and needs, such as healthcare coverage, retirement plans, and wellness programs, to enhance overall job satisfaction and loyalty.
  - Conduct regular salary benchmarking exercises to stay informed about market trends and adjust compensation packages accordingly to retain valuable employees.
  - Strengthen onboarding processes to seamlessly integrate new employees into the company culture and workflow.
  - Implement initiatives to engage and support new hires during their initial months with the company.
  - Proactively address any challenges or concerns faced by new employees to enhance their experience and retention.

## 🔨 Conclusion
The analysis demonstrates the profound impact of adjusting key factors on turnover rates. By reducing average worked time, increasing age, total working years, and tenure, turnover rate decreased significantly from about 16% to nearly 3%. This underscores the importance of tailored retention strategies focusing on employee engagement and career development. Moving forward, continuous evaluation and adaptation of these strategies are crucial for sustaining employee retention and organizational success.

## 🔨 Conclusion
The analysis highlights the importance of ocean proximity, particularly being inland, followed by island properties, in predicting house prices. Additionally, median income is also a significant factor in determining housing prices, although slightly less influential compared to ocean proximity. This information can be valuable for understanding the drivers of housing market dynamics and making informed decisions in real estate investments or policy-making.
This model has shown very excellent results since the marginal error is very small, therfore it can be implemented for later use as you can see in this illustration:

<img width="258" alt="Results" src="https://github.com/NadirZamouche/HouseValue-Forecast/assets/95188070/4ca5fba8-4bcb-4370-9d8b-4b050bb8197b">
