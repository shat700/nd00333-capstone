# Heart Failure Prediction

## Introduction
Heart diseases are one of the most prominent causes of death these days. This is because of habits such as smoking, junk eating, regular alcohol consumption and overall an unhealthy lifestyle. Some people can also be more prone to developing symptoms of a heart disease because of their genetics. Therefore, awareness is imperative in such cases. 
A machine learning model can play an important role in this case by predicting based on the different important factors whether death is imminent or not. This can be extremely helpful as it can make people understand how they need to modify their lifestyle to avoid the worst case scenario.

## Project Set Up and Installation
In order to work on this project, I first opened AzureML Studio and opened the notebook section to start working on the automl run, hyperdrive run, scoring script to be used in deployment of best model and train script to be used for training of the hyperdrive model. A compute cluster was set up to run the notebooks in AzureML. A CPU compute with vm_size="Standard_D3_V2" and max_nodes=4 was selected for this project.

## Dataset

### Overview
The dataset consists of 12 different factors that directly or indirectly are responsible for cardiovascular diseases. It was obtained from kaggle as an open dataset and imported in the form of a URL for this project, converted to pandas dataframe. An autoML and a hyperdrive run were performed to get the best model based on the primary metric 'accuracy'. The best model obtained was 'VotingEnsemble' from the autoML run with the accuracy of '0.88299' as compared to that of '0.75757' obtained from the hyperdrive run.

### Task
The aim of the project is to develop a model that takes the input data and predicts on the target column:'DEATH_EVENT' and determine the output in binary. Where '0' means death will not happen and '1' means death will happen. In order to develop this model, I first prepared the training script and the 2 notebooks for automl run and hyperdrive run. The scoring script was prepared later for model deployment stage.

### Access
The dataset is accessed in the Azure workspace in the form of a URL. The TabularDatasetFactory class converts the data to tabular form from csv format for AzureML and then I converted it into a pandas dataframe to finally work with in this project. 

## Automated ML
The task for autoML is set as 'classification' to be performed on the dataset. The automl settings include "n_cross_validations" which is used to determine the preditions of the model on new data that was not used in training the model, "primary_metric" as 'accuracy' which autoML will optimize for model selection in case of classification, "enable_early_stopping" is enabled in case the score for primary metric of a model does not improve in the first few iterations, "experiment_timeout_minutes" as 15 minutes (making it cost effective) being the amount of time all the iterations will take before the experiment completes and lastly, "max_concurrent_iterations" as 5 which is the number of iterations running in parallel to improve the efficiency of the autml run.
The automl settings are part of the AutoMLConfig class which is the configuration of the autoML experiment to be run in AzureML.

### Results
The best model obtained from the automl run was 'VotingEnsemble' with the highest accuracy of '0.88299'. However, by increasing the experiment timeout duration to 30 minutes and decreasing the maximum number of concurrent iterations, the score might improve but not substantially.

#### RunDetails

![rundetailsautoml1](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/rundetailsautoml1.png)

#### AutoML Run

![automlpipeline](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/automlpipeline.png)

#### Best AutoML Model 

![bestautomlrun1](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/bestautomlrun1.png)

#### AutoML best model parameters

![automlmodelparameters](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/automlmodelparameters.png)

## Hyperparameter Tuning
The algorithm chosen for this experiment was 'Logistic regression' to predict the probability of outcome on the target column of 'DEATH_EVENT'. Two-class logistic regression used in this project, is a binary classifier which identifies the probability of 2 outcomes i.e. whether 'DEATH_EVENT'=0 or 'DEATH_EVENT'=1. The parameters used for the hyperparameter search are an sklearn estimator, early termination policy as bandit policy to automatically terminate poorly performing runs thereby improving computational efficiency, 'Accuracy' as the primary metric with the goal to maximize it generating the best model and lastly, a total of 50 runs with 4 maximum concurrent or parallel runs to provide the hyperdrive substantial iterations to to generate the best metrics and with high efficiency. 
For parameter sampling, random sampler was used which supports discrete and continuous hyperparameters as well as early termination of low-performance runs. It is also helpful in improving results by doing initial search.

### Results
The best model obtained from the hyperdrive run was with the accuracy of '0.75757'. The performance of the hyperdrive run could be improved by increasing the maximum number of total runs from 50 to 100 thus letting it perform more iterations and come up with better metrics. Another possible solution could be the addition of 'cross-validation' parameter in HyperDriveConfig object to test the stability of the generated model. That should also authenticate and improve the quality of models obained from hyperdrive run. Lastly, a better vm size and vm priority could also improve the performance of the hyperdrive and result in better accuracy of the trained model.

#### RunDetails

![rundetailshyperdrive](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/rundetailshyperdrive.png)

#### Hyperdrive Run

![hyperdriverun](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/hyperdriverun.png)

#### Best Run

![hyperdrivebestrun](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/hyperdrivebestrun.png)

## Model Deployment
Since the 'accuracy' was found to be the higher in case of automl run, the model was saved as a pickle file and registered in AzureML directory. The model was previously saved as a joblib file but later as a pickle file because it contains the sklearn library. The model was then registered under the name of "Heart_failure_prediction" by importing workspace and providing the model path from outputs file. An 'AzureML-AutoML' environment was set up followed by the inference configuration that used scoring.py script to make predictions on the test data. The scoring script takes 2 functions: the init() function inputs the saved model as a pickle file and the run() function defines the sample input taken from the original dataset, used to query the endpoint. 
The model was deployed as an ACI (Azure Container Instance) webservice with enabled application insights and authentication. 
Followed by deployment, the scoring_uri and primary key were retrieved for the deployed webservice to be tested after sending a request by means of uri and key. The sample input is in the form of a 2-d array obtained from pandas dataframe inside a dictionary (json.loads). The keys inside the 2-d array form the columns with the respective values. The output obtained after sending the request was obtained as "{\"result\": [1, 1]}" . This implies that death occured in both the cases of sample input data. 
The result was cross-verified with the dataset. 

#### Scoring uri and primary key of the deployed webservice

![urikey](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/urikey.png)

#### Successful Deployment

![successfuldeployment](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/successfuldeployment.png)

#### Endpoint

![automlmodelendpoint](https://github.com/shat700/nd00333-capstone/blob/master/starter_file/automlmodelendpoint.png)

## Screen Recording

* https://youtu.be/K6mHger07DM

## References

* Deploy machine learning models to Azure: https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-and-where?tabs=azcli

* Consume an Azure Machine Learning model deployed as a web service: https://docs.microsoft.com/en-us/azure/machine-learning/how-to-consume-web-service?tabs=python



