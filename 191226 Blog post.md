# Sparkify Capstone Project
This project is part of the Capstone project for Udacity's Data Science Nanodegree.<br>
The project analyses log data for two months for "Sparkify" music streaming service (which is similar to Spotify or Pandora), **to observe the behavior for users who stayed vs. users who churned.** Churn analysis is a very important business problem to help companies increase customer retention and loyalty.<br>
To gain insights on churn and non-churn users, the project computes several user attributes from the log data. The data show that **users that cancel, tend to be new/recently registered, and less engaged with the platform.**<br>
To predict churn, the project further builds two churn models: 1) a Logistic Regression, and 2) a Multi-Layer Perceptron (MLP). F1 score was used as the optimization metric for both models. **The MLP model provided slightly better results, with an F1 score of 0.78 for test data (vs. 0.76 for the Logistic Regression).**<br>
The rest of the page describes the followed project steps.

## 1. Load and Clean Dataset
The project uses Spark Python API (PySpark) running on IBM Cloud on a medium-sized dataset (230MB) of Sparkify log data. PySpark was the chosen analysis language in order to perform data science at scale (i.e. Bid Data).<br>
The dataset contains in total **543,705 records** (i.e. log entries) spread across **448 users**, out of which **99 users have visited the "Cancellation Confirmation" page (i.e. churned)**. The dataset spans 2 months of records (1-Oct-18 to 1-Dec-18) for the users.<br>

*Figure 1 Columns of Sparkify log data*<br>
![Figure 1](/Blog_figures/1.png)

## 2. Exploratory Data Analysis
#### Churn frequency
Churn is defined using the Cancellation Confirmation page (presumably once a user visits this page he has deleted his account). This happens for both paid and free users. Since 99 of 448 users have churned, the **churn frequency is 22%.**<br>
#### Data Exploration
To observe the behavior for users who stayed vs. users who churned, various user attributes are computed and compared. These (per-user) attributes are:
* Count of each visited page (attribute name: *About, Add Friend, Add to Playlist, Cancel, Cancellation Confirmation, Downgrade, Error, Help, Home, Logout, NextSong, Roll Advert, Save Settings, Settings, Submit Downgrade, Submit Upgrade, Thumbs Down, Thumbs Up, Upgrade*)
* Gender (attribute name: *is_M, is_F*)
* Session statistics
	* Avg. length of listened songs (attribute name: *avg_length*)
	* Avg. number of items (e.g. songs) browsed or listened to in one session (attribute name: *avg_itemInSession*)
	* Count of sessions (attribute name: *sessionId*)
* Subscription level (attribute name: *is_free, is_paid*)
* Number of days since registration (attribute name: *days_registration*)

*Figure 2 First 5 rows of computed user attributes*<br>
![Figure 2](/Blog_figures/2.png)
#### Data understanding
Next, the attributes were compared between churned and non-churned users. Since the attributes have different scales (e.g. count of pages vs. average length of session), each attribute was normalized and displayed on a 0-1 scale.
*Figure 3 Scaled distribution of attributes for churn and non-churn users*<br>
![Figure 3](/Blog_figures/3.png)

Comparison of attributes reveals that **users that cancel tend to be new, and less engaged with the system.** In particular:
* Users that cancel visit fewer "engagement" pages and relatively more "negative" pages vs. users that do not cancel.
	* "Engagement" pages (visited less by churn users): Add Friend, Add to Playlist, Save Settings, Thumbs Up.
	* "Negative" pages (visited more by churn users): Roll Advert, Thumbs Down.
* Users that cancel have fewer sessions vs. users that do not cancel (as evidenced by count of sessions (sessionId))
* Users that cancel have registered recently (as evidenced by number of days since registration (days_registration))


