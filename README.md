# Airline Passenger Satisfaction Survey Predictive Modeling

<img width="332" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/af749eea-c575-4e9d-aa9d-fa1abea10b51">


## Project Overview

This report aims to establish predictive algorithms using SAS Enterprise Miner. The dataset used in this report is an Airline Passenger Satisfaction Survey, which is available on Kaggle. It contains the survey parameter with a target variable of satisfaction (Satisfied / Neutral or Dissatisfied) with passenger demographic information and airline service dimensions, such as delay times. 

The outcome of this study provides data-driven guidelines for the airline company to identify which service dimensions contribute to the dissatisfaction, hence, to improve their service quality.

## Objectives 
1. to gain insights into airline service dimensions and consumer demographics that influence customer satisfaction through conducting exploratory data analysis.
   
2. to establish a machine learning model using SAS Enterprise Miner that able to:
- Categorize satisfaction of airline service dimension ratings and client demographics.
- Deploy, apply, and compare predictive modeling strategies to determine the optimal performance model.
- Critically interpret the data.
3. to make strategic recommendations to boost customer satisfaction and improve business growth.

  ### Data Source
The dataset is obained from Kaggle [Available Here](https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction)

### Software
- SAS Enterprise Miner [Available Here](https://www.sas.com/en_my/software/enterprise-miner.html)

### Methodology
This report uses The Cross-Industry Standard Process for Data Mining (CRISP-DM) for executing predictive modeling. CRISP-DM's prevalence as the most widely-used analytics model lends credibility for its effectiveness for its flexible and industry-agnostic approach. It has been the popular methodology in numerous polls conducted among data mining experts (Hotz, 2018).


<img width="199" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/8d6924ce-c470-49c5-a1b9-d13eabd0f656">

## Data Modeling Techniques
### Exploratory Data Analysis (EDA)

The dataset contains 103,904 observations across 25 variables. The Figure 2 shows a descriptive outlook of the dataset from Import Files nodes. The changes were made to the A, ID and Satisfaction column, where the variable A was rejected as its not useful in predicting target variable, ID role changed to ID. Satisfaction was chosen as target variable with binary level; Satisfied and Neutral / Dissatisfied and will be used for predictive modeling.

<img width="544" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/3c98b3b2-a2e4-45cd-acef-22e36d2133d6">

### Data Understanding
Initial stage of creating predictive modeling is to understand the underlying structure of the dataset. The StatExplore module is used to provide numerical summaries that focus on the statistical properties of the data. On the other hand, Graph Explore emphasizes visual exploration to understand data distribution and relationships.

### Target Variable from Graph Explore

<img width="546" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/27da46b5-e489-491f-a7f2-877d73d9dab3">

The binary target variable percent is shown in figure 3. It illustrates that the target variable class is balanced even though neutral or dissatisfied slightly higher than satisfied by 13.6% or 1,136. The difference is so small that it does not indicate bias in distribution classification.

### Summary Statistic from StatExplore

<img width="538" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/d0bc9bf2-2372-440d-ac92-2dc1cdf49104">

Figure 4 shows the detailed statistical summary of each variable. It reveals an unusual outcome that could indicate issues with the data. The existence of missing values and error values. The initial observation is that there are 300 missing values in the Arrival_Delay_in_Minutes variable. 

In addition, the summary statistics reveal that there are minimal values of 0 in 15 service dimensions, such as Baggage_handling, seat_comfort, and inflight_entertainment. These values suggest the presence of invalid values, which could potentially imply an entry error. The rating scale ranges from 1 to 5. 

The variables Arrival_Delay_in_Minutes and Departure_Delay_in_Minutes display notable abnormalities characterized by exceptionally high skewness and kurtosis. These variables may require specific measures, such as transformation or outlier handling, to enhance the performance of the model. This report will address two primary issues: missing values and inaccurate values of zero.

### Dataset Preparation

Once the data has been thoroughly examined, the following step is to make the necessary preparations for predictive modeling. After identifying missing and incorrect values during the data understanding phase, the next step is to address these issues by utilizing a replacement node and an imputation node to substitute those values.

<img width="554" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/f45d87dd-b9df-4653-bf58-be275e1db44b">

The replacement is depicted in Figure 5. This was done using the Replacement Node as shown in methodology figure 10. Any value that below 1 in service dimension, substituted with missing value through the utilization of a user-specified limit method. As a replacement, we then designate the value "Missing" in the score property. Age, arrival_delay_in_minutes, baggage handling, departure_delay_in_minutes and flight distance did not undergo any changes as there is no error identified.

<img width="547" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/6829933b-b1a0-403c-b8e6-4f5b57a9c445">


The result depicted in figure 6. A total of 15,932 values have been transformed into new values. The variable has been renamed with the addition of the "REP" prefix, and its minimum value has been updated to 1. The preceding 0 values have been transformed into missing values.

### Manage Missing Values using Imputation

<img width="134" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/11ed7ce6-d8dd-4606-bb9a-3d44b37ebdbf">

<img width="542" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/cb78e74b-cc69-41c3-8795-a5c8288576da">

In the presence of missing values, imputation is implemented as a means of handling the situation. The property adjustment in figure 7. SAS Enterprise Miner selects the input method to be counted automatically when the target variable is a class. Indicator variable type set to unique; variable source set to imputed; and variable role set to input. The evidence of imputation as shown in the ‘Number of missing for Train’. The variable has been renamed with the addition of the "M_REP" prefix.

### Data Partition

<img width="221" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/354a5b40-3105-4826-860a-1b47ade12fab">

The fundamental principle of data partitioning is that the amount of training data should exceed the amount of validation data. In this report, the data partition was divided into an 80:20 ratio, with 80% allocated for training and 20% for validation.

### Inspecting Variable Correlation

After variable imputation and data partition, checking variable correlation helps to identify multicollinearity, a condition where predictors variables are highly correlated with each other that can affect the precision coefficient of statistical power of the model.

<img width="536" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/da566846-3598-48e2-b0fa-d4497e24cc97">

The variable correlation matrix in figure 9 indicates that there are no significant strong positive correlations among predictors, except for Arrival Delay in Minutes and Departure Delay in Minutes. This is expected as delays in departure are likely to result in delays in arrival.

## Predictive Algorithm

As per figure 10, the model chosen for analysis is Decision Tree, HP Tree and Logistic Regression to identify the problems that arise from airline passenger satisfaction surveys. We compare Decision Tree model and HP Tree model to provide a predictive model so that the airline can understand more about customer related data and its trends. The highest score will be chosen for the predictive model.

Second, the logistic regression model will be employed for the purpose of categorization and predictive analytics. Each independent variable will be assessed and assigned a score to determine which variable has a greater impact on satisfaction. Since the outcome is a probability, the variable that is affected by other factors is constrained to a range of values between 0 and 1. This approach facilitates the identification of the most significant features for predicting customer satisfaction.

<img width="521" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/2bc0c01b-3f9f-47a2-8c00-33ccb9d40997">

### Experiment 1: Logistic Regression

Logistic regression allows analysis of each predictor in the airline satisfaction survey to predict the dependent variable, satisfaction. The initial phase involves comparing the logistic regression model with different hyperparameter tuning like selection models. The selection models are default, forward, backward, and stepwise. We establish the validation classification as the standardized selection criterion for all models.

<img width="518" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/404b0530-94da-44c1-9842-3a29476a81c9">


### Model Evaluation

<img width="542" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/258f867f-fea5-4a5f-8114-9d0cf926b7a7">

Figure 12 illustrates that both Log Regression Backward and Log Regression None (default) have the same validation misclassification rate. However, SAS Enterprise Miner automatically selects the model with accurate predictors for customer satisfaction by assigning label Y to the selected model. In order to demonstrate the effectiveness of the model, a thorough analysis of the metrics for each model is conducted in figure 13, and their performance is evaluated using a scoring system.

<img width="509" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/e7780770-61f8-4978-8fed-aee4b6e7c445">
<img width="511" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/0e98f139-08c3-4a73-9724-e2dab46c959d">

The Logistic Regression Backward Is the best model for its performance indicators given low misclassification rate and high specificity that reflect correct assignment of positive class on which customer is labeled satisfied. The focus was set to the logistic regression backward and it has the best performance against other models.

<img width="542" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/b3d37437-fb98-4691-b741-4b62a89b5c3d">

### Interpretation and outcome

Figure 14 provides information about the relationship between the predictor variables and target variables in Logistic Regression Backward. The coefficients, significance, and odds ratios are accessed to have insight between predictor and satisfaction. The model suggests that Business class, loyal customer type, cleanliness, check-in service, ease of online booking, inflight entertainment, inflight service, inflight wi-fi service, leg room service, on board service, online boarding, and seat comfort indicate factors that increase the odds of customer satisfaction. Negative coefficients, such as for Economy class and departure/arrival time issues, indicate these factors decrease the odds of satisfaction. Non-significant predictors (p ≥ 0.05), such as gender, have no substantial impact on satisfaction.

### Experiment 2: Decision Tree / HP Tree

Decision trees are a powerful model for visualizing and understanding hierarchical patterns and relationships within a dataset. It can provide insights into the repercussions of these patterns, such as the probability of different event outcomes. The model demonstrates the use of conditional control statements, such as "If-then" scenarios, to aid in the decision-making process and establish an organization's strategic goals and key performance indicators. The purpose for utilizing the Decision Tree in SAS Enterprise Miner is to predict the “Satisfaction” target variable using various input variables. The result contributes to the development of a data-driven method for decision-making within the airline industry, offering valuable information to enhance customer satisfaction.

<img width="464" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/103b1832-1ad4-44e9-8196-c62274449a6f">

### Model Evaluation

<img width="529" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/5d7faa86-f62b-445d-87d8-d3944a958041">

According to fit statistics in figure 16, SAS Enterprise Miner labeled HP Tree C4.5 as Y, indicating the best performance model. HP Tree C4.5 scored the highest with lowest misclassification rate at 0.054 against other models. 

Figure 17 shows performance comparison of each model.

<img width="516" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/578a72c6-b4b0-4c7c-ba7b-986d4c71d5d6">
<img width="410" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/9a772bc0-b050-4693-ad34-636def4a4481">
<img width="412" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/c878e5c1-da39-4576-a52f-8787fb893f61">

The HP Tree C4.5 is the optimal model due to its strong performance indicators, characterized by a low misclassification rate and a high specificity. These indications accurately assign the positive class, indicating customer satisfaction. HP Tree Cost-Complexity is not lacking in performance when compared to C4.5, which could serve as an alternative model. The HP Tree Assessment and Optimal Decision Tree Assessment both demonstrated good performance. However, they scored lower in performance measures compared to C4.5 and HP Tree CC, which is the cause for their rejection. The subsequent research will concentrate on the HP Tree C4.5.

<img width="546" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/193cfad8-8392-49ad-9354-5db455afe954">

The plot in figure 18 illustrates the determination of the most suitable level of complexity for the decision tree model. The ideal number of leaves is determined by the point at which the validation misclassification rate is minimized, as represented by the blue vertical line, which occurs at 116. After a certain point, increasing the complexity (leaves) of the model results in overfitting. This means that the model's performance on the validation set does not increase or may even suffer, despite fitting the training data more accurately.

<img width="541" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/79730554-0ba8-4308-842d-fe3e7880241f">

Now, let examine the node rules that affect customer satisfaction. In order to find the important nodes, we will take into account the nodes with notable predicted values and substantial sample sizes. These nodes are crucial because they demonstrate a distinct pattern in prediction results (either overwhelmingly satisfied or unsatisfied).

<img width="541" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/9c79e38b-56b8-4d7d-a0d1-c4a8c5bec528">
<img width="533" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/db1136fd-6a49-49cf-a7c3-006df90d547a">

### Interpretation and outcome

The best performing model based on high accuracy value is HP Tree C4.5. This model can be used for decision making as it highlights the pattern of customer satisfaction. The individual node provides information about the nodes and provides crucial information about how different factors (features) contribute to predicting customer satisfaction. Below is a list of summarized node rules together with their associated details that support business decisions as per business objectives presented in the next section.

1. Dissatisfied Personal Travel. It is predicted that this type of customers who give rating Inflight Wi-Fi service below 4 and online boarding greater than or equal to 3 will likely be dissatisfied. Based on the output, total observation is 4,638 in this category has a similar pattern, with 0% predicted to be satisfied and 100% predicted to be neutral or dissatisfied.

<img width="514" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/2f17f6fb-10ae-4a16-8086-78f96a79b195">

2. Dissatisfied Personal Travel in Eco or Eco Plus. Similar to previous node, the main contribution of customer frustration are Inflight Wi-Fi service and online boarding that has scoring below 3. Total observation was significant with 14,757. Eco and Eco plus are the most vulnerable to having the highest customer churn, with 0% predicted to be satisfied and 100% predicted to be neutral or dissatisfied.

<img width="513" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/02cfd83c-9260-4580-9fef-6ca03bc47466">

3. Dissatisfied Business Class. The major frustration from Business class customers is from Inflight entertainment (rating below 3), Inflight Wi-Fi service and online boarding which has ratings of below 3. The airline company needs to pay attention to business class as this segment pays extra for service they are getting. Based on the output, a total of 2,498 observations falls into this category, with 0.5% predicted to be satisfied and 99% predicted to be neutral or dissatisfied.

<img width="515" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/b44a4086-17aa-447b-a52a-9bc486e1c3cd">

4. Dissatisfied Loyal Business Class Customer. Under similar condition but for loyal customers, it shows a similar pattern. On which inflight service and check-in service rating less than 4, inflight entertainment rating between 1 and less than 3, inflight wi-fi service, online boarding rating less than 3. Additionally, these customers have given a gate location rating of less than 3. Based on the output, a total of 2,499 observations falls into this category, with 11% predicted to be satisfied and 88% predicted to be neutral or dissatisfied.

<img width="515" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/0352764f-4f0b-49dd-8ad2-0b66d28fbcf3">

5. Dissatisfied Loyal Customer for Business Travel in ECO or eco PLUS. Displeasure of this segment of customers is relatively similar to Personal Travel in node rule 29. The main frustrations are from inflight service and check-in service (both ratings less than 4) baggage handling (rating less than 4.), inflight Wi-Fi service, and online boarding (both ratings less than 3). Based on the output, a total of 4,234 observations falls into this category, with 5% predicted to be satisfied and 95% predicted to be neutral or dissatisfied.

<img width="513" alt="image" src="https://github.com/AfifRifaie95/Airline-Passenger-Satisfaction-Survey-Predictive-Modeling-in-SAS-EM-visual-in-Power-BI/assets/159521904/0d589a7f-4033-4d7e-983c-1306aaaa8ee6">

## Recommendation
Deducing from the above analysis on customer satisfaction, the airlines are recommended to take the following five strategic actions,

A) Improve critical service. According to the output and finding from the individual node rules, the most contributor of customer dissatisfactions are Inflight Wi-Fi, Online Onboarding, Baggage Handling and Check-in Service. These crucial services must be rechecked by the airline company to make sure it meets the standard of international bodies. Allowing external experts to transparently audit this area could meet the business objectives.

B) Digital transformation. Getting feedback from customers is important for airline companies to identify which services are in need for improvement. Through digital transformation, airlines can encourage passengers to give honest feedback with ease. Airlines such as Southwest Airlines in the United States have pivoted to social media channels like Twitter and Facebook, recognizing that digital-first channels are easy to access and preferred by many customers (Goldstein, 2023). Any improvement undertaken must be communicated actively to show the airline’s commitment in improving the service. By embracing digital opportunities, airlines can also enhance passenger satisfaction through personalized services, increased efficiency, and innovative solutions. The integration of AI, predictive maintenance, cloud technology, and collaborative data sharing are also key strategies that can lead to a significant improvement in the air travel experience. 

C) Expectation Management. It involves understanding, shaping, and fulfilling passenger expectations. It is a multifaceted concept that encompasses pre-flight, in-flight, and post-flight experiences. The literature suggests that passengers form expectations based on their previous travel experiences, word of mouth, and the promises made by the airline. (Lestari & Murjito, 2020). These expectations serve as a benchmark against which the actual service is evaluated. 

D) Marketing campaign. Understanding the needs and preferences of different traveler demographics, such as business travelers, and by using data-driven strategies, airlines can create targeted campaigns that resonate with passengers. The satisfaction rate among business travelers is notably higher than that of personal travelers. This could be attributed to the fact that business travelers place a premium on service quality, which is often addressed in targeted marketing 25
campaigns. By focusing marketing efforts on the specific needs and preferences of business travelers, airlines can improve satisfaction rates within this demographic.

## Conclusion
The data modeling was done using predictive analysis with Logistic Regression, Decision Tree and HP Tree model. The logistic regression provides information about the relationship between the predictor variables and target variables while HP Tree helps visualizing and understanding hierarchical patterns within a dataset. The combination of both models provides essential resolution to the airline satisfaction problem by systematically analyzing curated data. This insightful information can be confidently communicated to the highest management for their decision.

As seen on figure 20, it shows that a large number of customers are likely to be dissatisfied. People who fly in economy classes are much more likely to refrain from being loyal customers. While some Online boarding gets are between 3 and 5, dissatisfaction is noted when ratings fall below or equal to 3. Checking bags and customer service get low ratings (less than 4). The personal travel category is significantly impacted by dissatisfied passengers, as a majority of them tend to express unfavorable sentiments in their reviews of the services.

The models provide a baseline for optimal strategy that can reduce customer dissatisfaction. This report met the objectives by conducting exploratory data analysis to get insights into airline service dimensions and customer demographics that influence satisfaction. Established a machine learning model using SAS Enterprise Miner to categorize satisfaction of airline service dimension ratings and customer demographics. Based on the findings, made strategic recommendations to the airline company to boost customer satisfaction and improve business growth.

## Reference
1. Goldstein, M. (2023, May 12). Have Airline Passengers Given Up On Getting Good Customer Service? Forbes. https://www.forbes.com/sites/michaelgoldstein/2023/05/12/have-airline-passengers-given-up-on-getting-good-customer-service/
2. Hotz, N. (2018, September 10). What is CRISP DM? Data Science Process Alliance. https://www.datascience-pm.com/crisp-dm-2/
3. Kullolli, T., Trebicka, B., & Fortuzi, S. (2024). Understanding Customer Satisfaction Factors: A Logistic Regression Analysis. Journal of Educational and Social Research, 14, 218. https://doi.org/10.36941/jesr-2024-0038
4. Lennart. (2023, December 14). A new deep dive into passenger frustration with airlines. TNMT. https://tnmt.com/passenger-frustration-with-airlines/
5. Lestari, Y., & Murjito, E. (2020). Factor Determinants of Customer Satisfaction with Airline Services Using Big Data Approaches. Jurnal Pendidikan Ekonomi Dan Bisnis (JPEB), 8, 34–42. https://doi.org/10.21009/JPEB.008.1.4
6. Xie, M.-P., & Zhao, W.-Y. (2010). The analysis of customers’ satisfaction degree based on decision tree model. 2928–2931. https://doi.org/10.1109/FSKD.2010.5569280
7. Zahraee, S. M., Shiwakoti, N., Jiang, H., Qi, Z., He, Y., Guo, T., & Li, Y. (2023). A study on airlines’ responses and customer satisfaction during the COVID-19 pandemic. International Journal of Transportation Science and Technology, 12(4), 1017–1037. https://doi.org/10.1016/j.ijtst.2022.11.004

