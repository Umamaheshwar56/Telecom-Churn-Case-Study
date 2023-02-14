** TELECOM - CHURN - CASE - STUDY

# BUSINESS PROBLEM OVERVIEW

* All telecom customers can choose any service providers and actively switch from one operator to another. In our highly competitive telecom market, the    
  telecom industry undergone an annual average churn rate of 15-25%. 
  
* The fact that it costs 5-10 times more to get a new customer than to retain an existing customers, customer retention has now become even more important than  
  customer acquisition.
* Retaining high profitable customers is the prime business goal of the telecome industries.

* To minimise the customer churn, telecom industries need to decide which customers are at high risk of churn.

* In Our Case study, we analyse customer-level data of a leading telecom firm, build predictive models to identify customers who is in
  high risk of churn and identify the main indicators of churning.

# CHURN - UNDERSTANDING

* Two main payment model in telecom industry - Postpaid (customers pay a monthly/annual bill after using the services) and Prepaid (customers pay/recharge with a   
  certain amount in advance and then use the services).

* In the postpaid connection model, when customers want to switch to another operator, they usually inform the existing operator to terminate the services, and we directly know that this is an occurence of churn.

* However, in the prepaid connection model, customers who want to switch to another network can simply stop using the services without any prior information, and it is dofficult to know whether someone has actually churned or is not using the services temporarily (e.g. someone may be on a trip abroad for a month or two and then intend to resume using the services again).

* Therefore, churn prediction is usually more critical and significant for the telecome industry, and the term ‘churn’ should be understande carefully. In addition the   prepaid is the most common model in India and southeast Asia, while postpaid is familiar in Europe and North America.

* This project is based on the Indian and Southeast Asian market.

# CHURN - DEFINITION

* There are different ways to define churn, such as:

# Revenue Based Churn: 

* Customers who have not utilised any revenue-generating facilities such as mobile internet, outgoing calls, SMS etc. ie. they don’t generate 
  revenue but use the services. 

# Usage-based churn: 

* Customers who have not done any usage, either incoming or outgoing - in terms of calls, internet etc. over a period of time.

* A potential shortcoming of this definition is that when the customer has stopped using the services for a while, it may be too late to take any corrective actions to 
  retain them.
  
* In this project, we will use the usage-based definition to define churn.

# High-value Churn

* In India and the southeast Asia markets, approximately 80% of revenue comes from the top 20% customers (called high-value customers). Thus, if we can reduce 
  churn of the high-value customers, we will be able to reduce significant revenue leakage.

* In our  project, we will show high-value customers based on a certain metric (mentioned later below) and predict churn only on high-value customers.


# Understanding the Business Objective and the Data

* The business objective is to predict the churn in the last (i.e. the ninth) month using the data (features) from the first three months. 

* The dataset contains customer-level information for four consecutive months - June, July, August and September. The months are encoded as 6, 7, 8 and 9,  
  respectively.

* Understand  Customer Behaviour During Churn.

* Customers generally do not switch to another competitor suddenly, but over the period of time they churn. In churn prediction, we assume that there are three phases 
  of customer lifecycle :

    * The ‘good’ phase: In this phase, the customer is happy with the service and behaves as usual.

    * The ‘action’ phase: The customer experience starts to sore in this phase, for e.g. he/she gets a compelling offer from a competitor, faces unjust charges, 
      becomes unhappy with service quality etc. The customer usually shows different behaviour than the ‘good’ months. Also, it is crucial to identify   
      high-churn-risk customers in this phase, since some corrective actions can be taken at this point (such as matching the competitor’s offer/improving the service 
      quality etc.)

    * The ‘churn’ phase: In this phase, the customer is said to have churned. We define churn based on this phase. Also, it is important to note that at the time of 
      prediction (i.e. the action months), this data is not available to us for prediction. Thus, after tagging churn as 1/0 based on this phase, we discard all data 
      corresponding to this phase.

* Since we are working over a four-month window, the first two months are the ‘good’ phase, the third month is the ‘action’ phase, while the fourth month 
  is the ‘churn’ phase.

# DATASET & DATA DICTIONARY

The dataset can be downloaded from the link provided: https://drive.google.com/file/d/1SWnADIda31mVFevFcfkGtcgBHTKKI94J/view.

* The data dictionary contains meanings of abbreviations. Some frequent ones are loc (local), IC (incoming), OG (outgoing), T2T (telecom 
  operator to telecom operator), T2O (telecom operator to another operator), RECH (recharge) etc.

* The attributes containing 6, 7, 8, 9 as suffixes imply that those correspond to the months 6, 7, 8, 9 respectively.

# Data Preparation

The following data preparation steps are crucial for this problem:

* Derive new features is the most important parts of data preparation. We use our business understanding to derive features that we think could be important indicators 
  of churn.

* Filter high-value customers as mentioned, we need to predict churn only for the high-value customers. Those who have recharged with an amount more than or equal to 
  X, where X is the 70th percentile of the average recharge amount in the first two months (the good phase).

* Tag churners and remove attributes of the churn phase, Now tag the churned customers (churn=1, else 0) based on the fourth month as follows: Those who have not made 
  any calls (either incoming or outgoing) AND have not used mobile internet even once in the churn phase. The attributes we need to use to tag churners are:

  total_ic_mou_9
  total_og_mou_9
  vol_2g_mb_9
  vol_3g_mb_9

* After tagging churners, then emove all the attributes corresponding to the churn phase (all attributes having ‘ _9’, etc. in their names).

# MODELLING

* Build models to predict churn. The predictive model will give two purposes:

    * It will be used to predict whether a high-value customer will churn or not. By knowing this, the company can take action steps such as providing special plans,   
      discounts on recharge etc.

    * It will be used to identify important variables that are strong predictors of churn. 

* In some cases, both of the above-stated goals can be achieved by a single machine learning model. But here, we have a large number of attributes, and thus we should 
  try using a dimensionality reduction technique such as PCA and then build a predictive model. After PCA, we can use any classification model.

* Since the rate of churn is typically low (about 5-10%, this is called class-imbalance) - we will try using techniques to handle class imbalance.

* The following suggestive steps to build the model:

* Preprocess data (convert columns to appropriate formats, handle missing values, etc.)
* Conduct appropriate exploratory analysis to extract useful insights.
* Derive new features.
* Reduce the number of variables using PCA.
* Train a variety of models, tune model hyperparameters, etc. (handle class imbalance using appropriate techniques).
* Evaluate the models using appropriate evaluation metrics. Note that it is more important to identify churners than the non-churners accurately - choose an 
  appropriate evaluation metric which reflects this business goal.
* Finally, choose a model based on some evaluation metric.

* The above model will be able to achieve one goal - To predict customers who will churn. We can’t use the above model to identify the important 
  features for churn. That’s because PCA usually creates components which are not easy to interpret.

Therefore, we will build another model with the main objective of identifying important predictor attributes which help the business understand indicators of churn. A good choice to identify important variables is a logistic regression model or a model from the tree family. In case of logistic regression, we will make sure to handle multi-collinearity.

After identifying important predictors, display them visually - we can use plots, summary tables etc. - whatever we think best conveys the importance of features.
Finally, recommend strategies to manage customer churn based on our observations.

# STRATEGIES CAN BE IMPLEMENTED

* Promotional offers can also be very helpful.

* A drop in Local Minutes of usage might be because of unsatisfactory network, focus on customer satisfaction service because of poor network or unsuitable customer 
  schemes/plans. Efforts shall be made to provide a better network and focus on customer satisfaction.
  
* Based on the usage / last recharge/ net usage, routine feedback calls should be made for customer satisfaction and services that can understand their grievances &  
  expectations. Proper steps should be taken to avoid them from churning. 
  
* Various attractive offers can be introduced to customers showing a sudden drop in the total amount spent on calls & data recharge in the action phase to lure them.

* Customized plans should be provided to such customers to stop them from churning.
