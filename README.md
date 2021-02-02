# Heart Failure Prediction

## Introduction
Heart diseases are one of the most prominent causes of death these days. This is beacuse of habits such as smoking, junk eating, regular alcohol consumption and overall an unhealthy lifestyle. Some people can also be more prone to developing symptoms of a heart disease because of their genetics. Therefore, awareness is imperative in such cases. 
A machine learning model can play an important role in this case by predicting based on the 12 important factors whether death is imminent or not. This can be extremely helpful as it can make people understand how they need to modify their lifestyle to avoid the worst case scenario.

## Project Set Up and Installation
In order to work on this project, I first opened AzureML Studio and opened the notebook section to start working on the automl run, hyperdrive run, scoring script to be used in deployment of best model and train script to be used for training of the hyperdrive model. A compute cluster was set up to run the notebooks in AzureML. A CPU compute with vm_size="Standard_D3_V2" and max_nodes=4 was selected for this project.

## Dataset

### Overview
The dataset consists of 12 different factors that directly or indirectly are responsible for cardiovascular diseases. It was obtained from kaggle as an open dataset and imported in the form of a URL for this project, converted to pandas dataframe. An autoML and a hyperdrive run were performed to get the best model based on the primary metric 'accuracy'. The best model obtained was 'VotingEnsemble' from the autoML run with the accuracy of '0.87966' as compared to that of '0.75757' obtained from the hyperdrive run.

### Task
The aim of the project is to develop a model that takes the input data and predicts on the target column:'DEATH_EVENT' and determine the output in binary. Where '0' means death will not happen and '1' means death will happen. In order to develop this model, I first prepared the training script and the 2 notebooks for automl run and hyperdrive run. The scoring script was prepared later for model deployment stage.

### Access
The dataset is accessed in the Azure workspace in the form of a URL. The TabularDatasetFactory class converts the data to tabular form from csv format for AzureML and then I converted it into a pandas dataframe to finally work with in this project. 

## Automated ML
The task for autoML is set as 'classification' to be performed on the dataset. The automl settings include "n_cross_validations" which is used to determine the preditions of the model on new data that was not used in training the model, "primary_metric" as 'accuracy' which autoML will optimize for model selection, "enable_early_stopping" is enabled in case the score for primary metric of a model does not improve in the first few iterations, "experiment_timeout_minutes" being the amount of time all the iterations will take before the experiment completes and lastly, "max_concurrent_iterations" which is the number of iterations running in parallel.
The automl settings are part of the AutoMLConfig class which is the configuration of the autoML experiment to be run in AzureML.

### Results
*TODO*: What are the results you got with your automated ML model? What were the parameters of the model? How could you have improved it?
The best model obtained from the automl run was 'VotingEnsemble' with the highest accuracy of '0.87966'. However, by increasing the experiment timeout duration to 30 minutes and decreasing the maximum number of concurrent iterations, the score might improve but not substantially.

####RunDetails
![rundetails_automl](rundetails_automl.png)

####Best AutoML Model 
![best_automl_run](best_automl_run.png)
*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Hyperparameter Tuning
*TODO*: What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search
The algorithm chosen for this experiment was 'Logistic regression' to predict the probability of outcome on the target column of 'DEATH_EVENT'. Two-class logistic regression is a binary classifier which identifies the probability of 2 outcomes i.e. whether 'DEATH_EVENT'=0 or 'DEATH_EVENT'=1. 



### Results
*TODO*: What are the results you got with your model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Model Deployment
*TODO*: Give an overview of the deployed model and instructions on how to query the endpoint with a sample input.

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:
- A working model
- Demo of the deployed  model
- Demo of a sample request sent to the endpoint and its response

## Future Improvements
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.

