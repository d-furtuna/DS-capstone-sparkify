# Sparkify Capstone Project
This project is part of the Capstone project for Udacity's Data Science Nanodegree.<br>
The project analyses log data for two months for "Sparkify" music streaming service (which is similar to Spotify or Pandora), **to observe the behavior for users who stayed vs. users who churned.** Churn analysis is a very important business problem to help companies increase customer retention and loyalty.<br>
To gain insights on churn and non-churn users, the project computes several user attributes from the log data. The data show that **users that cancel, tend to be new/recently registered, and less engaged with the platform.**<br>
To predict churn, the project further builds two churn models: 1) a Logistic Regression, and 2) a Multi-Layer Perceptron (MLP). F1 score was used as the optimization metric for both models. **The MLP model provided slightly better results, with an F1 score of 0.78 for test data (vs. 0.76 for the Logistic Regression).**<br>
The rest of the page describes the followed project steps.

## 1. Load and Clean Dataset
The project uses Spark Python API (PySpark) running on IBM Cloud on a medium-sized dataset (230MB) of Sparkify log data. PySpark was the chosen analysis language in order to perform data science at scale (i.e. Bid Data).<br>
The dataset contains in total **543,705 records** (i.e. log entries) spread across **448 users**, out of which **99 users have visited the "Cancellation Confirmation" page (i.e. churned)**. The dataset spans 2 months of records (1-Oct-18 to 1-Dec-18) for the users.<br>

![Figure 1 Columns of Sparkify log data](/Blog_figures/1.png)

	
/Blog figures/2.png	
/Blog figures/3.png	
/Blog figures/4.png	
/Blog figures/5.png	
/Blog figures/6.png	
/Blog figures/7.png
