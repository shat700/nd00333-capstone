# Heart Failure Prediction

## Introduction
Heart diseases are one of the most prominent causes of death these days. This is beacuse of habits such as smoking, junk eating, regular alcohol consumption and overall an unhealthy lifestyle. Some people can also be more prone to developing symptoms of a heart disease because of their genetics. Therefore, awareness is imperative in such cases. A machine learning model can play an important role in this case by predicting based on the 12 important factors whether death is imminent or not. This can be extremely helpful as it can make people understand how they need to modify their lifestyle to avoid the worst case scenario.

## Project Set Up and Installation
*OPTIONAL:* If your project has any special installation steps, this is where you should put it. To turn this project into a professional portfolio project, you are encouraged to explain how to set up this project in AzureML.
In order to work on this project, I first opened AzureML Studio and opened the notebook section to start working on the automl run, hyperdrive run, scoring script to be used in deployment of best model and train script to be used for training of the hyperdrive model. 

## Dataset

### Overview
*TODO*: Explain about the data you are using and where you got it from.
The dataset consists of 12 different factors that directly or indirectly are responsible for cardiovascular diseases. It was obtained from kaggle as an open dataset and imported in the form of a URL for this project, converted to pandas dataframe. An autoML and a hyperdrive run were performed to get the best model based on the primary metric 'Accuracy'. The best model obtained was 'VotingEnsemble' from the autoML run with the accuracy of ... as compared to that of ... obtained from the hyperdrive run.

### Task
*TODO*: Explain the task you are going to be solving with this dataset and the features you will be using for it.
The aim of the project is to develop a model that takes the input data and predicts whether a 'DEATH_EVENT' will occur or not. The output is in the form of binary where '0' means death did not happen and '1' means death happened. In order to develop this model, I first prepared the training script and the 2 notebooks for automl run and hyperdrive run. The scoring script was prepared later for model deployment stage.

### Access
*TODO*: Explain how you are accessing the data in your workspace.
The dataset is accessed in the Azure workspace in the form of a URL. The TabularDatasetFactory class converts the data to tabular form from csv format for AzureML and then I converted it into a pandas dataframe to finally work with in my project. 

## Automated ML
*TODO*: Give an overview of the `automl` settings and configuration you used for this experiment


### Results
*TODO*: What are the results you got with your automated ML model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Hyperparameter Tuning
*TODO*: What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search


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

