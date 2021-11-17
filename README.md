# Predict Song Skips on Spotify based on Acoustic Data

		 	 	 		



Sandesh Paudel
Pdlsandesh317@gmail.com 
Technocolab Software’s 
2021-11-16




## Overview:
Spotify, a music streaming company, have the problem of incorporating the sequential nature of a listening session to predict whether a user will skip a given music track or not. Modelling sequential music skips provides streaming companies like Spotify the ability to better understand the needs of the user base, resulting in a better user experience by reducing the need to manually skip certain music tracks. Given information about the first half of a Spotify user’s listening session, the task is to predict whether each track in the second half of the session will be skipped or not. We model this task using a Gradient Boosting Tree.

 The main task of this project is to predict which music tracks a user will skip in the second half of the session conditioned on the first half. This problem can be considered a type of session-based recommendation, since no explicit user profile is available, and the user preferences should therefore be estimated within the first half of the session. After preprocessing of data is completed we build the model using LightGBM and SVM to predict whether the user will skip the song or not 
The accuracy of our LightGBM model is 87.5%. Our deployed code is released at. https://github.com/paudel-sandesh/Deployment_spotify_skip_prediciton 











## Methodology:
For this project, we follow simple machine learning life cycles all the steps in our life cycle are followed as below:
1: 	Datasets
2:	Data Preprocessing 
3: 	Data analysis and visualization 
4: 	Modelling 
5: 	Testing and result
6:  	Deployment

## Datasets:

Approximately 130 million listening sessions were provided for the training set, and each session contained between 10 and 20 tracks. The test set comprised approximately 30 million listening sessions, and detailed data was provided for the first half of each session, with the second half of each session to be predicted.

For this project, we only take a sample of 10,000 sessions data. where half of the tracks of each session are taken for the training and half of the tracks for testing.

Our datasets were divided into two main files where in the first file we have user behaviour features having 21 columns of the song like:
Hour of the day
Season length 
Context type
History user behaviour 

And the second file contains acoustics features having 29 columns like:
Track beat strength 
Track acoustics vectors 
Tracks loudness etc.


## Data Preprocessing:
In order to pre-process the data for training, we merged user behaviour and acoustic features using track ids for each session. Later the following pre-processing techniques are employed

1, Handling missing values
2, Converting binary categorical features to numeric:
3, One hot Encoding 
4, Outlier detection 
5, Scaling using min-max scalar
		
	
## Data Analysis and Visualization:
After preprocessing we gather useful information from the data. We find which features are more imported and how many values are there in these features this help a lot in data understanding and outlier detection 
We did most of the data analysis using an external python library called SweetViz which help us to do advanced data analysis in an easy manner

Acousticness 				Duration





			

# Modelling:
	
Two types of models were attempted:
 • gradient boosted trees 
 • SVM 
 			
				
### Gradient Boosting trees:
A model was trained for each label, or target, track position. That is, a model was trained for the first track position to be predicted, another for the second track position to be predicted, and so forth. Identifying good parameters for training the model is a big task in model building. The parameters ultimately used in training the model were:
    learning_rate':0.23, 
   'boosting_type':'dart',
              'objective':'binary',
              'metric':['auc', 'binary_logloss'],
              'num_leaves':2500,
              'max_depth':5,
              "min_data_in_leaf": 200,
              "lambda_l1": 15,
              "lambda_l2": 70,
              "min_gain_to_split": 2,
              "bagging_fraction": 0.7,
              "bagging_freq": 1,
              "feature_fraction": 0.9

 
### SVM:
Support vector machines are sets of supervised learning methods used for classification and regression problems. The main reason for using SVM in our project is it works very well with high dimensional spaces for SVM we got an accuracy of 87%
We use many default parameters and linear in the kernel for training the model

## Deployment:
Here I use called Flask framework and Heroku cloud for the deployment. And I created a simple frontend using HTML and bootstrap. 
	The main challenge for deployment is the webserver I have to get the acoustics features of the song based on the name of the song for this first I got the track-id of the song in response by sending the name of the song as a request and further I send a request for acoustics features based in track ids from Spotify WEB API 


## Conclusion:
Building a sequential skip prediction was quite challenging. This project is very beneficial for streaming services like Spotify on their recommended system. The following accuracy of prediction is obtained using Machine Learning methods like LGBT and SVM, which is 87.5% and 87.07% respectively. 
We can further improve this project using seq2seq Lstm and attention models to get the best accuracy and provide the best user experience on the platform.

