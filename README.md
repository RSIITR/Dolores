# Dolores - Competition organised by DSG-IITR 

# Problem Statement
Make it about machine learning – that seems to be a theme behind Google’s return to robotics, an effort that reportedly has more to do with software than creating mechanical creatures that resemble human beings. Nowadays companies are synthetically generating more and more datasets from the realistic simulation of the dynamics of robots. Your task is to predict the angular acceleration (target) of one of the robot arm's links. The training dataset contains features like angular positions, velocities and torques of the robot arm.


# Evaluation
The evaluation metric is RMSE(Root Mean Squared Error).

# Code description
Initially all necessary libraries are imported(not all at once):    
-> numpy is imported for simple mathematical operations.  
-> pandas for table manipulations.  
-> train_test_split for splitting a small percent of training data into cross-validation data.  
-> GBM Regressor and XGB Regressor for creating an ensemble model of the 2.  
-> mse metrics to check for the performance of the ensemble model on cross-validation data.  
-> matplotlib.pyplot for simple visualization of data.  
  
The 2 .csv files(train and test) are loaded into the notebook as dataframes using pandas library.  
  
## Preprocessing
Though the provided data isn't raw, it still contains primary key, unwanted keys and target column which are removed as a part of preprocessing. X and y are the feature and target matrices. The same is followed in the case of test data.  
Also. the feature data is checked for null values(if they existed), but luckily that isn't the case here, so the data is clean.  
  
## Simple Visualization  
Now, simple visualization is done to see for the behaviour or trends followed by each feature with the target. But looking at the scatter plots, there is no linear trend seen, so SVM and linear regression are ruled out. Best option to use here would be multiple tree-based models, as they avoid over-fitting.  

## Cross-validation  
Training data is split into temporary train and test data, 40% of training data is the cross-validation data.
Though there were many models that I used for cross-validation(like: RF, GBM, etc...) but ensemble model of GBM and XGBoost with 40% and 60% contribution each showed good results(as expected, because both are tree based models and avoid overfitting).
But the numbers 40% and 60% were just by chance, no tunung was done to find out their best values.  
After fitting, prediction was done on the cross_validation data, hence 'mse' metrics was used to check the performance of the model.     

## FInal prediction and submission  
The above ensemble model was used to fit the complete training data and hence used on the original test features to predict the target, which was passed into a dataframe(with relevant index column) for submission(in the form of a .csv file).
