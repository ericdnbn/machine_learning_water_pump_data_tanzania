![image](https://sswm.info/sites/default/files/inline-images/WATER%20CHARITY%20n.y.%20Deep-well%20hand%20piston%20pump%20including%20apron%20and%20drain%20in%20Gambia.jpg)
# Water Pump Functionality Analysis In Tanzania

## Business Problem
Using data from the Tanzanian Ministry of Water via DataDriven, our goal is to predict the functionality of water pumps across Tanzania. As noted on Kaggle, "Predictive analytics on this dataset could allow the Ministry to know in advance which pumps are most likely to be non-functional, so that they can triage their repair efforts. It's hard to find much simpler examples of how a good predictive model can directly save time and money."[https://www.kaggle.com/danielmartinalarcon/tanzanian-water-pumps](url)

## Data
We started out with ~59,400 rows of data. <br>
Our target class (functional and non functional) has a ~60%/~40% split. <br>

## Preparation
We dropped duplicate features and unnecessary features in the dataset. We also replaced null values with 'Unknown'.<br>

## EDA

![image](https://raw.githubusercontent.com/ericdnbn/phase_3_project/main/images/Non%20Functioning%20Pumps%20by%20Management%20Groups.png)<br>
We speculated that the company managing a well may have an impact on the percentage of failed pumps. VWC seems to be leading the way with almost 43% of their wells being non functional.<br><br>

![image](https://raw.githubusercontent.com/ericdnbn/phase_3_project/main/images/Water%20Quantity%20Non%20Functioning%20Pumps%20.png)<br>
Dry wells have the highest percentage of non functioning wells, at just about 97%. It is also interesting that waterpoints labeled as insufficient water have the second highest percentage of non functional wells. It seems the less water a well has, the higher the chance the pump is non functional.<br><br>

![image](https://raw.githubusercontent.com/ericdnbn/phase_3_project/main/images/Waterpoint%20Type%20Non%20Functioning%20Pumps.png)<br>
We found that waterpoint type is a good indicator of a well's functionality. If a waterpoint has multiple standpumps, there is over a 50% chance that the pump will be non functional. In the future, we would try to identify the 'Other' category to see which pumps are performing the worst.<br>

## Model Selection
We used Dummy Classifier, Logistic Regression, K Nearest Neighbors, Random Forest Classifier, and XGBoost models to find the prediciton accuracy.<br><br>

DummyClassifier:<br>
Mean Train Score: 0.6157575757575758<br>
Mean Test Score: 0.6157575757575758<br><br>

Logistic Regression:<br>
Mean Train Score: 0.7929812528577963<br>
Mean Test Score: 0.7913829654570398<br><br>

KNN:<br>
Mean Train Score: 0.9180331088664422<br>
Mean Test Score: 0.8168237934904602<br><br>

RandomForestClassifier:<br>
Mean Train Score: 0.8008793178700587<br>
Mean Test Score: 0.7836664484349669<br><br>

XGBoost:<br>
Mean Train Score: 0.9067957351290685<br>
Mean Test Score: 0.842864758698092<br><br>

Our second XGBoost model had the best ratio of bias to variance. Although the model is slightly overfit, it had the highest prediction accuracy.<br>

## Results
The best model was our second XGBoost model with hyperparameters of 'max_depth': 7, and 'n_estimators': 200. This model correctly predicted ~85.8% of the testing data.<br>

![image](https://raw.githubusercontent.com/ericdnbn/phase_3_project/main/images/Confusion%20Matrix.png)<br>

The XGBoost model predicts 12,743 water pumps in the testing data correctly. The model also predicts 1,458 water pumps as non-functional when they are functional and it preditcs 649 water pumps as functional when they are non-functional.

## Feature Importance
We investigated the most important features in our best model.<br>

![image](https://raw.githubusercontent.com/ericdnbn/phase_3_project/main/images/Feature%20Importance.png)<br>

We found that the feature quantity_dry had the biggest impact, ~28.2%, and waterpoint_type_other had the second biggest impact on the model, ~12.4%.

## Conclusion
Our final model, the XGBoost, gave us ~85.8% accuracy in predicting the functionality of a water well.<br><br>
Given the features that had the greatest impact on the functionality of water wells in Tanzania, our recommendations to the Tanzanian Ministry of Water are as follows:

* Perform regular checks on the quantity of water in the wells, and take preventative measures to decrease the chances of them being non-functional.
* Replace waterpoint types with the designation of ‘other’ with more effective and widespread types, like gravity waterpoints.
* Put policies in place that ensure the company managing a well are performing regular checks and maintenance. Screen companies seeking to construct a well using a rigorous standard to decide if their project may go forward.

## Future Steps
Identify the categories of certain features that are labeled as ‘other’ and ‘unknown’. This will create more clarity and specificity within the dataset, and theoretically, a model that can make even more accurate predictions.

Use machine learning to create a model that predicts the quantity of water in a well, dry or not, to help the Tanzanian Ministry of Water be more proactive in performing checks and maintenance.

Determine the impact of funders on the functionality of water wells.

## Repository Structure 
```
├── Working_Notebook
│   ├── Eric's Notebook.ipynb     
│   ├── Mitch_Wkbook.ipynb     
│   ├── Soo's Work.ipynb    
│   └── Soohyun's work.ipynb
├── data  
│   ├── Col_Descriptions.docx
│   ├── Test Set Values.csv
│   ├── Training Set Labels.csv
│   └── Training Set Values.csv
├── images  
├── .gitignore
├── Final Notebook.ipynb
├── Powerpoint_Tanzanian_Water_Pump.pdf
├── README.md
```
