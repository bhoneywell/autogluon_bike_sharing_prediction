# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Brianna Honeywell

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
When I tried to submit my initial prediction I had to make sure the output was deemed acceptable by Kaggle so I made sure to replace any negative values with 0. I made sure the data was formatted as a dataframe so I could easily write it back to csv. I also checked the values to make sure none of the predictions were negative. If they were, I replaced the values with 0.

### What was the top ranked model that performed?
The top ranked model from my initial training was WeightedEnsemble_L3. This was also the top ranked model from my final iteration. This was according to the evaluation metric I specified which was root mean squared error. 

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
From the exploratory analysis I saw in particular that the datetime value varied quite a bit so I wanted to see if that variation played a part in the various outputs of the count of bikes. That led me to introduce the additional datetime field of 'day' to see if usage varied for different days of the year. I also recognized that autogluon wasn't recognizing my categorical variables correctly so I had to specify those. 

### How much better did your model preform after adding additional features and why do you think that is?
My model improved by .005(Kaggle Score)/.237(Model score) after adding additional features. I think it improved only slightly because I only added one feature that was on the right track, but I could've added more. This is what led me to introduce additional datetime features in the next model. If I had introduced multiple fields that could've addressed multiple concerns that might've led to more improvement. 

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
 My model improved by 1.27686 (Kaggle Score) / 17.776814 (Model Score)  after trying different hyperparameters

### If you were given more time with this dataset, where do you think you would spend more time?
I would spend more time feature engineering. I still don't think I've done all I can with regards to the datetime fields necessary. I'd like to see which of those fields 
ended up being ranked the highest and removing those that were redundant. I also would've looked outside of just datetime fields to introduce. 

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|   |        model | time | problem_type |             eval_metric |     new_fields | hyperparameters |                        hyperparameter_tune_kwargs | score   |
|--:|-------------:|-----:|-------------:|------------------------:|---------------:|----------------:|--------------------------------------------------:|---------|
| 0 |      initial |  600 |      default | root_mean_squared_error |        default |         default |                                           default | 1.79368 |
| 1 | add_features |  600 |      default | root_mean_squared_error |      added day |         default |                                           default | 1.78832 |
| 2 |          hpo | 1200 |   regression | root_mean_squared_error | added day,hour |           light | {'num_trials': 5, 'search_strategy': 'random',... | 0.51146 |

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](model_test_score.png)

## Summary


After the initial model I performed two iterations to see how I could improve the model's performance. In the first iteration I opted to introduce a new field and makes sure all input variables were interpreted correctly. The new input variable was breaking the datetime field down by day to see if there were any trends that could influence the model depending on which day it happened. Additionally, for the sake of the autogluon model I set season and weather to be interpretted as categorical variable. Previously they were interpretted as numerical which may have led to the lower initial score. 

The next iteration I opted to add more new fields as well as hyperparameters. I added a new datetime field because I wasn't sure if day was granular enough to track all of the date variablility. I also tuned the hyperparameters. I made sure the problem type was specified to regression so the model didn't have to iterate through other options. I also added more time for the model to train so it could get as accurate as possible. Initially, I changed the evaluation metric for the last model to r2, but then I couldn't compare them appropriately. I also changed the model to light so it would take up less memory.