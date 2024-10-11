# Customer-Churn-Analysis

Part I: Research Question

The research question that will be applied for this project is: what are the leading factors that cause a customer to churn?

The goal of analyzing this research question is to improve customer retention. By identifying key factors that lead to churn or prevent churn, marketing and services for the company can improve, along with customer retention.

Part II: Method Justification

For logistic regression, the target variable must be a binary categorical variable.  One must also ensure that there is no multicollinearity present within the predictor variables and that each data entry represents independent observations. According to Statistical Solutions logistic regression, “requires that the independent variables are linearly related to the log odds” (Assumptions of Logistic Regression, n.d.). In addition to these requirements, the sample size must be large for accurate analysis.

Python is a strong language to use for logistic regression along with data cleaning, exploration, and wrangling. Utilizing libraries and packages such as SHAP, Sklearn, Pandas, and NumPy makes the process systematically more efficient. Projects coded with python can be easily integrated into a data pipeline within the company’s current dashboards for continuous review. The SHAP library allows one to make an easy-to-understand visualizations of predictor variables and how each coeGenerate easy-to-understand visualizations of predictor variables and their corresponding coefficientsfficient contributes to the outcome in the logistic model.

 Logistic regression is an appropriate technique to analyze this research question because the target variable is binary.

Part III: Data Preparation

The goals of data cleaning are to identify missing values, outliers, and duplicates. There were about 2,000 out 10,000 missing values in a categorical variable “Internet Service”. This was treated by replacing missing values with the mode. Outliers in numerical variables were identified and preserved because each outlier is within reason to believe it is not an error. Each numerical variable was graphed to identify any outliers. Lines 3–12 in the Juypter notebook attached show the data treatment steps.

The distribution of churn shows that the company is successful in retaining customers, but there is still room for improvement because approximately 30% of customers churned.

The following numeric variables show a normal distribution: Age, Outages per week, email, tenure, and bandwidth GB used per year. The following numeric variables show skewness: Children, Income, contacts, yearly equipment failure, monthly charge, all survey questions. Normality for logistic regression is not an assumption so the skewness was not treated.
The following numeric variables have outliers: Children, Outages per week, email, income, contacts, yearly equipment failure, and all survey questions. All outliers were not removed because it was reasonable to infer that the outliers were not entry errors but real-world data. Income varies and outliers are expected with income. Survey questions may also have real outliers due to different customer experiences. Outages per week and yearly equipment failure outliers could be caused by weather and storms. Outliers in frequency of contact and email are also legitimate because some customers may have experienced extreme technical difficulty. Additionally, a household could have 10 children, so that was not removed either.

The following categorical variables show that most customers lean towards a certain preference for internet service with about 65% of customers preferring Fiber optic over DSL. About 50% of customers prefer month to month contracts vs a yearly contract,  about 20% of customers do not sign up for phone service, and around 1/3 of customers prefer to pay via electronic check. The distribution of the Techie variable shows that about 80% of customers do not identify as a techie. The gender variable shows about a 50:50 distribution of males and females with less than 10% of customers identifying as nonbinary. A little over 50% of customers use multiple services. About 55% of customers do not use device protection or online backup services, and about half of customers are signed up for streaming movies or streaming TV. 

The goals of data transformation are to ensure that there is no multicollinearity and that all variables are on a similar scale so that feature importance is weighted within the logistic equation accurately. Another important goal of data transformation is to re-express categorical variables as numeric. Lines 22-32 in the Jupyter notebook attached shows the code for these steps. Some variables were removed to prevent multicollinearity based on VIF Scores. The predictor variables were scaled using sklearn StandardScaler().

Part IV: Model Comparison and Analysis

The accuracy of the initial model along with a confusion matrix and AUC-ROC score is displayed below:
Accuracy: 0.90250000
Confusion Matrix:
[[1371   85]
[ 110  434]]
AUC-ROC Score: 0.869707498383969
Log Likelihood: -0.23033151

The initial model will be reduced by applying Recursive Feature Elimination. Selecting the best model with the best number of features to keep will be based on Log Likelihood, AUC_ROC Score, Accuracy, and model complexity. The intention of this research question is to easily identify when a customer may churn so having less features to measure for predictions will help expedite identification. The accuracy of the final model along with a confusion matrix and AUC-ROC score is displayed below:
Accuracy: 0.90250000
Confusion Matrix:
[[1371   85]
[ 110  434]]
AUC-ROC Score: 0.869707498383969
Log Likelihood: -0.23033151

Part V: Data Summary and Implications

A regression equation for the reduced model is displayed below: 

P(Churn=1) = 1 / 
(1 + e^(-3.1029  + -2.8834 * Bandwidth_GB_Year 
\+ -1.4509 * Contract_Two Year + -1.3974 * Contract_One year 
\+ -0.9195 * InternetService_Fiber Optic + -0.1056 * Phone_Yes 
\+ -0.0562 * Age + -0.0375 * Gender_Nonbinary + -0.0342 * Item8 
\+ 0.0302 * Contacts + 0.0482 * Income 
\+ 0.0602 * PaymentMethod_Credit Card (automatic) 
\+ 0.0954 * Children + 0.1252 * PaymentMethod_Mailed Check 
\+ 0.1531 * Gender_Male + 0.2591 * DeviceProtection_Yes 
\+ 0.3115 * PaymentMethod_Electronic Check + 0.4470 * Techie_Yes 
\+ 0.4508 * OnlineBackup_Yes + 0.8670 * Multiple_Yes 
\+ 1.6292 * StreamingTV_Yes + 1.8711 * StreamingMovies_Yes))

A SHAP graph is displayed in the jupyter notebook line 78 which visually represents the contribution and rank of each predictor variable with the most impactful feature scaled along the graph. The most important feature for predicting if a customer will churn or stay is Bandwidth GB used per year because the coefficient for this variable has the largest magnitude compared to all. 
All coefficients that have a positive sign indicate that those features will contribute to a customer churning. These variables include: 
Frequency of contacts, income, payment method, number of children in household, if a customer identifies as a techie and/or male, if a customer has device protection, online backup services, if a customer is signed up for multiple services, and Streaming movies or TV.
Variables that have a negative coefficient contribute to preventing churn. These variables include Bandwidth GB used per year, if a customer signed a contract, if a customer is signed up for Fiber optic internet and/or phone service, Age, if a customer identifies as nonbinary, and how a customer responds to question 8 in the survey. 

The accuracy of the final model is significant such that predictions are within 90% accuracy. An ROC curve in the jupyter notebook line 77 represents the final model’s ability to make predictions accurately versus false positive predictions. An ideal ROC curve for an optimized model will show the blue line curved to the top far left corner. This represents that the model predicts with accuracy and precision. However, this model has 21 features which may introduce overfitting by being trained specifically to this one data set. This model could potentially fail to make accurate predictions with new data due to overfitting. 

The statistical significance of this model is also represented in the percent change calculation of each coefficient. For example, if a customer identifies as a techie, there is a 56.3% chance increase that the customer will churn. If a customer signs a two-year contract, there is a 76% chance the customer will not churn. 

Coefficients for Class 0:
Children: 0.0954
Odds Ratio: 1.1001
Percent Change: 10.01%
------------------------------
Age: -0.0562
Odds Ratio: 0.9453
Percent Change: -5.47%
------------------------------
Income: 0.0482
Odds Ratio: 1.0494
Percent Change: 4.94%
------------------------------
Contacts: 0.0302
Odds Ratio: 1.0307
Percent Change: 3.07%
------------------------------
Bandwidth_GB_Year: -2.8834
Odds Ratio: 0.0559
Percent Change: -94.41%
------------------------------
Item8: -0.0342
Odds Ratio: 0.9664
Percent Change: -3.36%
------------------------------
Gender_Male: 0.1531
Odds Ratio: 1.1655
Percent Change: 16.55%
------------------------------
Gender_Nonbinary: -0.0375
Odds Ratio: 0.9632
Percent Change: -3.68%
------------------------------
Techie_Yes: 0.4470
Odds Ratio: 1.5637
Percent Change: 56.37%
------------------------------
Contract_One year: -1.3974
Odds Ratio: 0.2473
Percent Change: -75.27%
------------------------------
Contract_Two Year: -1.4509
Odds Ratio: 0.2344
Percent Change: -76.56%
------------------------------
InternetService_Fiber Optic: -0.9195
Odds Ratio: 0.3987
Percent Change: -60.13%
------------------------------
Phone_Yes: -0.1056
Odds Ratio: 0.8998
Percent Change: -10.02%
------------------------------
Multiple_Yes: 0.8670
Odds Ratio: 2.3798
Percent Change: 137.98%
------------------------------
OnlineBackup_Yes: 0.4508
Odds Ratio: 1.5695
Percent Change: 56.95%
------------------------------
DeviceProtection_Yes: 0.2591
Odds Ratio: 1.2958
Percent Change: 29.58%
------------------------------
StreamingTV_Yes: 1.6292
Odds Ratio: 5.0997
Percent Change: 409.97%
------------------------------
StreamingMovies_Yes: 1.8711
Odds Ratio: 6.4958
Percent Change: 549.58%
------------------------------
PaymentMethod_Credit Card (automatic): 0.0602
Odds Ratio: 1.0620
Percent Change: 6.20%
------------------------------
PaymentMethod_Electronic Check: 0.3115
Odds Ratio: 1.3655
Percent Change: 36.55%
------------------------------
PaymentMethod_Mailed Check: 0.1252
Odds Ratio: 1.1334
Percent Change: 13.34%
------------------------------

Part V

Based on results, there are a few ways the business can improve customer retention. One can infer if a customer has device protection, online backup services, or is signed up for multiple services, Streaming movies, or TV, they are more likely to churn.  Device protection, online backup services, and Streaming Movies or TV need to competitively improve. A more thorough audit of these services will help identify areas that need to improve or if pricing is higher than a competitor’s price. Methods that are currently effectively retaining customers should be amplified such as signing contracts, upselling popular services like fiber optic internet and phone service. A marketing campaign that is more tailored towards the tech savvy audience could also help improve customer retention. Based on the survey data, the customer's value feeling listened to the most. Another potential course of action could be incorporating the company’s brand image to reflect deep listening to customer feedback and training staff accordingly. 



 Bibliography for web sources applied to the coding aspect of the project.  

Creating subplots through a loop from a dataframe. (2021, March 19). Stack Overflow. https://stackoverflow.com/questions/66705955/creating-subplots-through-a-loop-from-a-dataframe

Li, S. (2017, September 29). Building A Logistic Regression in Python, Step by Step. Towards Data Science; Towards Data Science. https://towardsdatascience.com/building-a-logistic-regression-in-python-step-by-step-becd4d56c9c8

Mishra, A. (2022, May 13). Data Visualization in a loop using Seaborn and Matplotlib. Medium. https://aparnamishra144.medium.com/data-visualization-in-a-loop-using-seaborn-and-matplotlib-499ee540726d

Save plot to image file instead of displaying it. (n.d.). Stack Overflow. Retrieved October 25, 2023, from https://stackoverflow.com/questions/9622163/save-plot-to-image-file-instead-of-displaying-it

Scikit-Learn. (2019). sklearn.preprocessing.StandardScaler — scikit-learn 0.21.2 documentation. Scikit-Learn.org. https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html

scikit-learn. (2019). sklearn.metrics.confusion_matrix — scikit-learn 0.21.3 documentation. Scikit-Learn.org. https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html

SHAP Feature Importance with Feature Engineering. (n.d.). Kaggle.com. Retrieved October 23, 2023, from https://www.kaggle.com/code/wrosinski/shap-feature-importance-with-feature-engineering

sklearn.metrics.log_loss. (n.d.). Scikit-Learn. Retrieved October 21, 2023, from https://scikit-learn.org/stable/modules/generated/sklearn.metrics.log_loss.html

Receiver Operating Characteristic (ROC). (n.d.). Scikit-Learn. Retrieved October 24, 2023, from https://scikit-learn.org/1.1/auto_examples/model_selection/plot_roc.html

Prakash, P. (2023, May 13). Mastering Machine Learning Predictions in Scikit-Learn. Medium. https://medium.com/@preethiprakash29/mastering-machine-learning-predictions-in-scikit-learn-25e86881a70e#:~:text=The%20predict_proba%20method%20is%20used


Bibliography for in-text citations and summarized references

Assumptions of Logistic Regression. (n.d.). Statistics Solutions. Retrieved October 21, 2023, from https://www.statisticssolutions.com/free-resources/directory-of-statistical-analyses/assumptions-of-logistic-regression/

Choueiry, G. (n.d.). Interpret Logistic Regression Coefficients [For Beginners] – Quantifying Health. Quantifying Health. Retrieved October 24, 2023, from https://quantifyinghealth.com/interpret-logistic-regression-coefficients/

Sperandei, S. (2014). Understanding Logistic Regression Analysis. Biochemia Medica, 24(1), 12–18. https://doi.org/10.11613/bm.2014.003

What is a ROC Curve and How to Interpret It. (2018, July 5). Displayr. https://www.displayr.com/what-is-a-roc-curve-how-to-interpret-it/#:~:text=The%20ROC%20curve%20shows%20the

Zach. (2021, August 31). How to Interpret Log-Likelihood Values (With Examples). Statology. https://www.statology.org/interpret-log-likelihood/




