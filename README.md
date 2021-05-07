# Neural Network

## Overview of the analysis

Alphabet Soup offers donations to charitable organizations.  They want to ensure that their funds donated will be targeted towards a successful project.  <br>
In order to select which applicants receive a donation, an analysis has been done using [charity_data.csv](https://github.com/taranahassan/Neural_Network_Charity_Analysis/blob/main/Resources/charity_data.csv), which consists of over 34,000 organizations that have been funded by Alphabet Soup in the past.  With this data a neural network model has been created to predict which future applicants might be successful in their project when funded by Alphabet Soup.


## Results

A deep learning model created initially produced an accuracy of 72.79% with a model loss of 56%.  <br>
![original_accuracy](https://user-images.githubusercontent.com/75437852/117384333-b9d2a900-aeb0-11eb-90e2-6c531b499f8c.PNG)<br>

The original model used the 'Relu' activation function at epochs of 100.  Below is the model structure: <br>
![original_structure](https://user-images.githubusercontent.com/75437852/117384403-dd95ef00-aeb0-11eb-946d-783668fe9a46.PNG)<br>

For better optimization to achieve an accuracy score of 75% or more, additional 3 models have been trained.

#### Attempt 1

**Data Processing** - *preprocessing of data was the same as original model*
* Columns "EIN" and "NAME" were dropped as they were not beneficial for a target or feature variables.
* "IS_SUCCESSFUL" column was selected as the target outcome.
* All remaining columns were featuers; "APPLICATION_TYPE", "AFFILIATION", "CLASSIFICATION", "USE_CASE", "ORGANIZATION", "STATUS", "INCOME_AMT", "SPECIAL_CONSIDERATIONS" and "ASK_AMT".
* Since "APPLICATION_TYPE" and "CLASSIFICATION" columns had more than 10 unique values, both columns required binning after identifying the density of each.

**Compiling, Training and Evaluating the Model**
* This model was defined with 3 layers; first layer with 80 neurons, second with 30 and last layer with 10.  The activation functions were all "Relu" except the output layer with the "Sigmoid" activation function. This model returned 6,271 in total trainable params.<br>
![structure1](https://user-images.githubusercontent.com/75437852/117470280-a06b4480-af24-11eb-81cc-52893732d7f7.PNG)<br>

* The model accuracy of 72.27% is very much similar to the original model and the model loss still at 56% using the same number of epochs of 100. <br>
![accuracy1](https://user-images.githubusercontent.com/75437852/117470316-a9f4ac80-af24-11eb-80c4-329b0bb01952.PNG)<br>

* An additional 3rd layer was introduced with 10 neurons and activation functions of "Relu" for all hidden layers.  Original layer performed above closer to 73%, therefore the same model structure as original was tested but with an additional layer increasing the parameters to see if that increases the model accuracy.  Unfortunately no significant difference was acheived implying that additional layers are not always necessary.

#### Attempt 2

**Data Processing** 
* Columns "EIN", "NAME" and "APPLICATION_TYPE were dropped as they were not beneficial for a target or feature variables. 
* "IS_SUCCESSFUL" column was selected as the target outcome.
* All remaining columns were featuers; "AFFILIATION", "CLASSIFICATION", "USE_CASE", "ORGANIZATION", "STATUS", "INCOME_AMT", "SPECIAL_CONSIDERATIONS" and "ASK_AMT".
* The "CLASSIFICATION" column had more than 10 unique values, both columns required binning after identifying the density.

**Compiling, Training and Evaluating the Model**
* Model was defined with 2 layers; first layer with 70 neurons and second with 20.  The activation functions were changed to "Tanh" for both layers and the output layer remained with "Sigmoid".  A total of 3,891 params - half the amount compared to Attempt 1. <br>
![structure2](https://user-images.githubusercontent.com/75437852/117470940-546ccf80-af25-11eb-8c3b-7ecd35ec59a0.PNG)<br>

* The model accuracy of 70.72% is lower than the original and attempted 1 model and the test loss is 2 points higher at 58.20%. Model was trained with 100 epochs as well. <br>
![accuracy2](https://user-images.githubusercontent.com/75437852/117471188-9a299800-af25-11eb-8f98-d2534e7c34a8.PNG)<br>

* In order to optimize better, an additional column was categorized as noisy variable since I couldn't find significance to the output and therefore dropped which then left 35 features.  Since the original model's accuracy was similar to Attempt 1, I reverted back to keeping only 2 hidden layers.  However the number of neurons were reduced following the rule of thumb; "2-3 times more than features".   Changing the activation fuction was to try and capture any negative values as well.
* As per the accuracy score, it is safe to assume that dropping the additional column for this model negatively impacted to a lower accuracy, returning less trainable data.  Proving the "APPLICATION_TYPE" data points are  significant and relevant for the prediction.  

#### Attempt 3

**Data Processing** 
* For this model - the data was preprocessed as the original.  Only dropping the "EIN" and "NAME" columns.  Also binning the "APPLICATION_TYPE" and "CLASSIFICATION" columns.

**Compiling, Training and Evaluating the Model**
* Model structure is the same as Attempt 1 with the number of layers and neurons per layer.  The activation functions were changed to "Sigmoid" for all hidden and output layers. <br>
![structure3](https://user-images.githubusercontent.com/75437852/117476884-56d22800-af2b-11eb-8fa6-184f2df343b9.PNG)<br>

* The model accuracy of 72.39% is slightly lower than the original and attempted 1 model, however the test loss is lower as well at 55.81%.<br>
![accuracy3](https://user-images.githubusercontent.com/75437852/117476909-5fc2f980-af2b-11eb-9aaf-9a81f24493d8.PNG)<br>

* When reviewing the validation set for the original model, the model acheived between 74-75% accuracy.  <br>
![epoch](https://user-images.githubusercontent.com/75437852/117478564-53d83700-af2d-11eb-885d-73418a1a7891.PNG)<br>

* Using the above validation set, the epoch was reduced to 84 for the 3rd model to achieve a higher accuracy than the previous attempts.  Unfortunately, the accuracy was still very similar in the 72% range.


## Summary

With 3 attempts of chaning the number of hidden layers, neurons and activation function, I was still not able to achieve an accuracy score of 75%.  Therefore I defined a function to create a sequential model with hyperparameters option.  The script is saved as [AlphabetSoupCharity_Optimization_trial](https://github.com/taranahassan/Neural_Network_Charity_Analysis/blob/main/AlphabetSoupCharity_Optimization_trial.ipynb).  This was created using Google Colaboratory due to time efficiency. <br>
After the results were completed
Summarize the overall results of the deep learning model. Include a recommendation for how a different model could solve this classification problem, and explain your recommendation, 
