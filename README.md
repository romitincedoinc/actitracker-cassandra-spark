# actitracker-cassandra-spark

The availability of acceleration sensors creates exciting new opportunities for data mining and predictive analytics 
applications. 
In this post, we consider data from accelerometers to perform activity recognition. And thanks to this learning we 
want to identify the physical activity that a user is performing. 
Several possible applications ensue from this: activity reports, calories computation, alert sedentary, match music 
with the activity...In brief, a lot of applications to promote and encourage health and fitness. 

This project is inspired from the [WISDM Lab’s study](http://www.cis.fordham.edu/wisdm/index.php).

## Data description
We use labeled accelerometer data from users thanks to a device in their pocket during different activities 
(walking, sitting, jogging, ascending stairs, descending stairs, and standing).

The accelerometer measures acceleration in all three spatial dimensions as following:

- Z-axis captures the forward movement of the leg
- Y-axis captures the upward and downward movement of the leg
- X-axis captures the horizontal movement of the leg

## Determine and compute features for the model
Each of these activities demonstrate characteristics that we will use to define the features of the model. 
For example, the plot for walking shows a series of high peaks for the y-axis spaced out approximately 0.5 seconds 
intervals, while it is rather a 0.25 seconds interval for jogging. We also notice that the range of the y-axis 
acceleration for jogging is greater than for walking, and so on. This analysis step is essential and takes time to 
determine the best features to use for our model.

We determine a window (a few seconds) on which we will compute all these features.

After several tests with different features combination, the ones that I have chosen are described below:

- Average acceleration (for each axis)
- Standard deviation (for each axis)
- Average absolute difference (for each axis)
- Average resultant acceleration (1/n * sum [√(x² + y² + z²)])
- Average time between peaks (max) (for each axis)

## Decision Trees, Random Forest and Multinomial Logistic Regression
Just te recapp: we want to determine the user’s activity from data. 
And the possible activities are: walking, jogging, sitting, standing, downstairs and upstairs. 
So it is a classification problem.

After aggregating all these data, we will use a training data set to create predictive models using classification 
algorithms (supervised learning). And then we will involve predictions for the activity performing by users. 
Here we have chosen the implementation of the Random Forest, Gradient-Boosted Trees and Multinomial Logistic Regression 
algorithms using MLlib, the Spark’s scalable machine learning library.

The algorithms are applyied on 6 classes: Jogging, Walking, Standing, Sitting, Downstairs and Upstairs.

Remark: with the chosen features we have bad results to predict upstairs and dowstairs. So we need to define more 
relevant features to have a better prediction model.