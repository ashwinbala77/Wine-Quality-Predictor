# Wine-Quality-Predictor
Machine Learning project done on R to create an effective model that predicts the quality of wines made in Bordeuax based on the tasting notes, price and year of creation. 

## Data Description
The dataset contains reviews for all the Bordeaux wines made in the 21st century. There are 14,349 unique wines collected, with scores ranging from 60 to a 100.
There are 989 column names, 985 of which are tasting notes that are of binary type variable (1 if tasting note is present in the wine, 0 if it is not). The other four variables are Name, Year, Score (our response variable) and Price. 

## Preprocessing and Missing Values in Dataset
The explanatory variable Price is in factor variable format and contains 4,610 missing values. This is around 32% of the total rows that we have, which was addressed by creating a model without those data points as well as running a model with those data points present or imputed. After comparing the results of each of these models, it was decided a suitable solution would be to create a subset of the data with no missing valuables for Price. The rest of the analysis within the project would be conducted with this subset of data. 

## Modelling
After analyzing the problem and dataset, we decided it would be appropriate to run three different models: linear regression, random forest, and XGBoost. Linear regression is appropriate as the response variable of Score could be explained by our explanatory variables of tasting notes, year, and price. The model gave coefficients for each variable and an expected score for each wine. We ran the linear regression model on both subsets of data: one with price and one without price. The most important aspect looked at was the RMSE values for each subset of data. Strengths of linear regression include the ability to easily see how close the predicted score is to the actual score. Furthermore, linear regression is the simplest of the three methods. Limitations include not being able to account for any nonlinearity in our dataset. Thus, the next method used is Random Forest. Random Forest helps us see how close our predicted wine quality scores are to the actual wine quality scores. Random Forest method also resulted in an RMSE value for each subset of data, ultimately showing us if price has a strong impact on wine quality scores. One of the limitations of random forest, however, is the amount of computational power required. For the third and final model, XGBoost was utilized. It is an appropriate method as it improves the models predictive performance, discourages overfitting, and allows us to tune each parameter to the data set. While tuning, the RMSE value was used as a guide for the optimal parameter values to be compiled in our final XGBoost model. 

## Results
The first linear regression model deployed with all the predictors but with no missing values rendered an RMSE value of 1.54166. Meanwhile, the linear regression model using the 
dataset excluding price entirely produced an RMSE value of 1.68511. After comparing the error of RMSE of both models, it was found that it would be in the best interest of the analysis to include price in the dataset as it improved the predictive performance of the model. This initial model informed our initial analysis and reaffirmed our preconceived notions that Price would be a predictor that would be quite influential on a Bordeaux wine’s score before we moved on to more sophisticated models. 

The results outlined in the Random Forest models were equally interesting. Before running the model on both data sets, the following hyperparameters were selected: 200 for ntree, 1 for nodesize, and 12 for mtry. Keeping these consistent in both models allowed for accurate comparison. Similar to the patterns observed within the linear regression models, the Random Forest model with price included produced an RMSE value (2.1105) lower than the model with this predictor excluded (2.2060). 

Building the final XGBoost model was the most thorough of those within our analysis, as each parameter was tuned to minimize RMSE. After evaluating Max Depth and Min Child Weight values of 10 and 15, respectively, were chosen as optimal. Gamma was then tuned, minimizing RMSE at a value of 0.00. The best subsample value was 0.6 and the best subsample ratio of columns was 1. Finally, the XGBoost model was run with various ETA values and 0.3 was optimal. All of these hyperparameters were compiled in the final XGBoost model. This tuning process was lengthy, but increasing the number of threads to 8 helped increase productivity. Had these hyperparameters not been tuned, our model would not have been utilized to its full potential. 

The trained XGBoost model deployed on the stratified data sample produced results that were easily interpretable. The XGBoost model’s SHAP plot provided our analysis with insight on which predictors affected wine score both positively and negatively. Some of these significant predictors represented in the SHAP plot such as Full Bodied, Tobacco, Blackberry and Fig indicate features of a Bordeaux wine that seem to be important when predicting a score.

## Conclusion
We were able to clean our data, tune our models, and create a useful model for predicting wine scores. However, there is a level of recognition that our model isn’t the be all r end all, nor is it 100% accurate. Some shortcomings of our data set include the potential of our samalias having different preferences than our group, our class, or anyone using our model. Furthermore, our model analyzes the tasting notes as individuals, but not as groups which is always prevalent in each distinct bottle. The surface has just been scratched in the industry of predicting wine scores, but this is a great indicator of the important statistics and features that are important to creating a good bottle of wine

### Credits
I would like to thank my group members; Madison Terreri, Chase Blackmun, Abigail Sweet and Charlie Pallett for working with me to create this model, the documentation and presentation. A large amount of credit must also go to our Machine Learning professor, Martin Barron on helping us with the tuning of the model and overall direction of the project. 
