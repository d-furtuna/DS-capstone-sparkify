This project is part of the Capstone project for Udacity's Data Science Nanodegree.

The project analyses log data for two months for the "Sparkify" music streaming service (similar to Spotify or Pandora). The project uses Spark running on IBM Cloud on a medium-sized dataset (230MB).

To observe the behavior for users who stayed vs. users who churned, several user attributes are computed and compared across these users. The insights from the data are that users that cancel, tend to be new/recently registered, and less engaged with the platform.

The project further builds two churn models: 1) a Logistic Regression, and 2) a Multi-Layer Perceptron (MLP). F1 score was used as the optimization metric. The MLP model provided slightly better results, with an F1 score of 0.78 for test data (vs. 0.76 for the Logistic Regression).

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

| *191216 Sparkify IBM.ipynb* The Jupyter notebook run in the IBM cloud<br>
| *191222 Blog post.pdf* The blog post<br>
| *README.md* this file


-----
III. RESULTS

When predicting churn users, the Logistic Regression provided an F1 score for test data of 0.76. The MLP model provided slightly better results, with an F1 score of 0.78. In real-life, different weights would be assigned to different prediction categories and the model would be optimized with the given weights (e.g. TP = 100; FP = 10; FN = 50; TN = 1).


IV. KEY TECHNICALITIES

The project used Spark Python API (PySpark) to perform exploratory data analysis at scale (i.e. cluster computing system for Big Data). The steps followed in the notebook are:

1. Load and Clean Dataset<br>
- The dataset file *medium-sparkify-event-data.json* contains 2 months (1-Oct-18 to 1-Dec-18) of Sparkify log data. Dataset is loaded, cleaned, and checked for invalid or missing data (e.g. Logged Out users are filtered out). The dataset file is not included in the github repo due to size limitations. 

2. Exploratory Data Analysis<br>
- Churn is defined using the *Cancellation Confirmation* page, which happen for both paid and free users.
- Various user attributes are computed and compared for churn and non-churn users.
- Comparing these attributes between churned and non-churned users, the behavior of these two groups is observed.

3. Feature Engineering and Selection<br>
- The defined user attributes were calculated over different timeframes, in order to select the attributes for a future model.
- Data was split in training and test sets.
- A two-sample Kolmogorov–Smirnov (K-S) test was used on training data to understand the discriminatory power of attributes.
Attributes with the highest discriminatory power (K-S p-val < 5%) were selected for a future model. To reduce collinearity, only one attribute per time-frame was selected, and attributes with a correlation coefficient higher than 0.9 with already selected attributes were also excluded.


4. Modeling<br>
- Two machine learning methods were applied and evaluated:
	Logistic regression
	Multi-Layer Perceptron with 3 layers containing (11 (inputs), 4, 2 (predicted labels)) nodes
- F1 score was used as the optimization metric. Both the Logistic Regression and the Multi-Layer Perceptron returned a probability that the user will churn. For the Logistic Regression, the threshold which maximized the F1 score was determined through a pyspark.ml function (using fMeasureByThreshold). For the MLP model the threshold was established by iterating through a series of thresholds and selecting the one which maximized the F1 score. For both models, training and threshold selection was done on training data, and final model evaluation done on test data.


V. LICENSING, AUTHORS, ACKNOWLEDGEMENTS

Author: Dumitru Furtuna.

Dataset: Udacity.

Templates: scikit-learn.org (for function plotting the confusion matrix)
