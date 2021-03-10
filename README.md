# Predictive analytics challenge: Patient’s survival
## Introduction
I worked on a predictive analytics challenge and details on this project comes from a Kaggle competition: “WiDS Datathon 2020”.[2] For this project, I worked on creating a model that can predict the patient’s survival by using existing data from the first 24 hours of intensive care. The dataset used for this project comes from MIT’s GOSSIS (Global Open Source Severity of Illness Score) initiative  and consists of more than 130,000 hospital Intensive Care Unit (ICU) visits from patients in one year. The datasets will be downloaded from kaggle competition page. [2] The dataset consists of a labeled training data with 91,713 encounters and a test data with 39308 encounters. The training data was used for building the model. The test data was used to test our model. The test data is unlabeled and comes without hospital_death variable that needs to be predicted by the model. It was a project worth doing because it focuses on social impact (patient health) and I can be a part of it. Also, this was my first hands-on experience on Kaggle competition which was a great experience 


## Research on Related Work
Related work on the project: “Survival prediction in intensive-care units based on aggregation of long-term disease history and acute physiology: a retrospective study of the Danish National Patient Registry and electronic patient records” [1]

The study uses neural networks algorithm to analyze patient’s disease history from the past 23 years to predict patients’ chances of survival in intensive care units. The dataset used for the study consists of more than 230,000 intensive care patients in Denmark spanning from 2004 to 2016. More specifically, the study uses registry data for long-term disease history and ICU admission, and acute ICU clinical data from EPRs, to create a machine learning model. 

The model makes three predictions: the risk of the patient dying in hospital (within any number of days of admission), within 30 days of admission, and within 90 days of admission. Once the model was developed, an external validation dataset, spanning from June 2012 to May 2016, was obtained from another hospital in Denmark to test the model and to measure its performance. 

Model performance was assessed with the Matthews correlation coefficient, the area under the receiver operating characteristics (ROC) curve, and positive predictive value.[1] 

# Steps Involved in accomplishing the project
In order to accomplish this, I followed the below steps:

#### 1.	Learn about the data:
A variety of scoring systems are used to quantify the severity of illness of patients admitted to the ICU and to predict their chances of survival to ICU and hospital discharge. Such prognostic scoring systems include the Simplified Acute Physiology Score (SAPS), the Mortality Probability Model (MPM) and the Acute Physiology and Chronic Health Evaluation (APACHE) scoring system.[3] APACHE has been used in our dataset to quantify the severity of illness of patients and to predict their chances of survival. APACHE was introduced in the early 1980s and few major revisions have occurred since then. APACHE II and III used in our dataset are two of such revisions and have been used in a significant number of ICUs for the past 15 years.

a.	Define research question – Will the patient survive or die?
b.	Data Validation and Cleaning – Prepared data by identifying any issues and by cleaning and transforming the data. 
i.	Dropped unnecessary columns before analyzing data - APACHE II and III are calculated using several vital measurements. A snippet of APACHE II calculator looks like the image below where the necessary measurements are used to calculate the APACHE II core:
                               ![image](https://user-images.githubusercontent.com/56932100/110676283-c9c85800-81a1-11eb-92fd-7f8f342d9a01.png) 

 
Similarly, APACHE III score is also calculated using several vital measurements.
Because our dataset includes both the vital measurements and the APACHE II and APACHE III scores, we do not need the variables that represent vital measurements. We only need APACHE II and APACHE III scores to study the patient's survival. That's why we remove such variables from our dataset as seen below.
We also remove height and weight as those are used to calculate the variable "bmi".
We further remove all ids as it will not help us in prediction of patient's survival. We also removed few more variables that we think do not contribute to the research question such as hospital_admit_source, icu_admit_source', icu_stay_type, readmission_status, and elective_surgery.
ii.	Checked for any missing values and adjusted those with either mean, median, or mode depending upon the variable 
iii.	Converted all categorical variables to numerical variables by creating new dummy coded variables
iv.	Performed statistical analysis and used feature scaling so that all the variables are having same scaling system.

c.	Exploratory Analysis – Understanding data to a much better extent to reveal data limitations, important features, and methods to answer research question. I performed univariate and multivariate analysis to achieve this.
d.	Refining research question – revisited research question after completing exploratory analysis

#### 2.	Machine Learning 
a.	Modeling Phase – Defined machine learning task and worked on understanding how the machine learns
i.	I performed Train-Test Spilt in order to build our model. Train data consists of the first 91713 rows and the test data consists of remaining 39308 rows. I made sure to build the model with train data only which was further split into train dataset and validation dataset. I used stratified shuffling split to consider all types of values equally. New train dataset consists of 73370 encounters and validation dataset consists of 18343 encounters. 
 
-	As of now, the modeling techniques used to predict patient’s survival are Supervised Learning: Classification Techniques as we are predicting whether the patient will survive or not. More specifically, I used the following classification techniques and compared the performance of each technique to select the final technique that outperformed all:
o	Logistic Regression
o	Decision Tree 
o	Random Forest 
o	Naïve Bayes
o	SVM 
o	Gradient Boosting
o	XG Boost
o	Neural Network

All of these algorithms are used to predict the probabilities of patient’s survival as our outcome variable “hospital_death” is a categorical variable and we are trying to predict if the patient will survive or not. However, in order to find which algorithm will perform the best and provide more accurate results, we have to perform all of these techniques and compare with each other. The one that outperforms all will be selected as our final model.


b.	Performance – Evaluate the usefulness of our model and if we need to improve it.


#### Conclusion
I worked on several techniques in order to come up with the final model. The final technique selected was XGBoost gradient classifier that performed the best among all while considering ROC curve as the performance measure. Please note it outperformed the previously selected technique, Gradient Boosting classifier and another newly applied Neural Network technique. 

The performance was measured using the area under Receiver Operating Characteristic (ROC) curve.

The final result is a model that predicts the patient survival.  More specifically, for a given data, the model provides a value of 1 to the variable “hospital_death”, if patient dies and a value of 0, if patient survives. The model also specifies the probability of patient’s survival. 

#### References (provide any background references)
1.	https://www.thelancet.com/journals/landig/article/PIIS2589-7500(19)30024-X/fulltext#seccestitle140
2.	https://www.kaggle.com/c/widsdatathon2020/overview
4.	https://bmcsurg.biomedcentral.com/articles/10.1186/1471-2482-9-11


