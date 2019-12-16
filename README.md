This project is part of the Capstone project for Udacity's Data Science Nanodegree.

The project analyses log data for two months for the "Sparkify" music streaming service (similar to Spotify or Pandora). The project uses Spark running on IBM Cloud on a medium-sized dataset (230MB)

To observe the behavior for users who stayed vs. users who churned, several user attributes are computed and compared across these users. The insights from the data are that users that cancel tend to be new/recently registered, and less engaged with the platform.

The project also builds two churn models: 1) a Logistic Regression, and 2) a Multi-Layer Perceptron (MLP). F1 score was used as the optimization metric. The MLP model provided slightly better results, with an F1 score of 0.78 for test data (vs. 0.76 for the Logistic Regression).

The project includes:
- The Jupyter Notebook used in the IBM cloud.
- A a blog post documenting all project steps from start to finish.

-----
I. INSTALLATION

The project uses the following libraries:<br>
*numpy==1.16.5<br>
scipy==1.3.1<br>
pandas==0.25.1<br>
matplotlib==3.1.1<br>
pyspark==2.4.4<br>
scikit_learn==0.22<br>
ibmos2spark==1.0.1*

-----
II. FILE DESCRIPTIONS

| app <br>
| - templates <br>
|   | - master.html *# main page of web app <br>*
|   | - go.html *# classification result page of web app <br>*
| - run.py *# Flask file that runs app <br>*
| - custom_scorer_module.py *# the used custom scoring function for the model <br>*

| data <br>
| - disaster_categories.csv *# data to process <br>*
| - disaster_messages.csv *# data to process <br>*
| - process_data.py *# ETL Pipeline preparation script <br>*
| - DisasterResponse.db *# database with cleaned data <br>*
| - output.txt *# captured output in one run of the process_data.py <br>*

| models <br>
| - train_classifier.py *# script that creates the machine learning model <br>*
| - (classifier.pkl) *# saved model; missing due to GitHub size requirements <br>*
| - output.txt *# captured output in one run of the train_classifier.py <br>*
| - custom_scorer_module.py *# the used custom scoring function for the model <br>*

| Chart.png  *# screenshot of the web-page with a chart <br>*
| Classification.png  *# screenshot of the web-page outputing classification results <br>*

| README.md *# this file*


-----
III. RESULTS

The model achieves an accuracy rate of ~95%, correctly predicting no category for 90% of the cases and correctly classifying the messages for one of the agencies in 5% of the cases. The model used the accuracy ratio for scoring ((TP + TN)/Total Population). In real-life, different weights would be assigned to different prediction categories and the model would be optimized for that (e.g. TP = 100; FP = 10; FN = 50; TN = 1).

Achieved overall confusion matrix (across all 36 output categories) in %:<br>

| 		|	| Predicted category	|	|
|---------------|------:|:---------------------:|:-----:|
| 		|	| False			|True	|
| Real category	|False	| 90.0% 		| 1.1%	|
|               |True	| 3.9%	 		| 4.9%	|


IV. KEY TECHNICALITIES

1. The ETL Pipeline
	Loads the messages and categories datasets.
	Merges the two datasets.
	Cleans the data.
	Calculates the top 10 tokenized words present in each category.
	Stores the results in a SQLite database with two tables: 1) "messages" 2) "words".

2. The ML Pipeline
	Loads data from the SQLite database.
	Splits the dataset into training and test sets.
	Builds a text processing and machine learning pipeline using a RandomForest MultiOutputClassifier. The evaluation of the clasifier is done using a custom scoring function (Accuracy ratio = (TP + TN)/ Total Population; F-score was not used as it does not take the True Negatives rate into account
	Trains and tunes a model using GridSearchCV. To save processing time, parameters were optimized individually. (This does not guarantee the best global parameters, but should be close).
	Outputs results on the test set.
	Exports the final model as a pickle file.

3. Flask Web App
	Visualises the data using Plotly.
	Processes an input message and outputs classification results.

V. LICENSING, AUTHORS, ACKNOWLEDGEMENTS

Author: Dumitru Furtuna.

Dataset: Udacity and Figure Eight.

Templates: Python code structure and much of the flask web app was provided by Udacity.
