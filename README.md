# CryptoClustering

In this challenge, I used Python and unsupervised learning (specifically k-means clustering) to predict if cryptocurrencies are affected by 24-hour or 7-day price changes.

### Prepare the Data

First, I normalised the data using the [skikit-learn] library, and [StandardScaler()].

### Find the Best Value for k Using the Original Scaled DataFrame

Using the elbow method, the following steps were taken to find the best value for [k]:
- Create a list with the number of [k] values from 1 to 11.
- Create an empty list to store the inertia values.
- Create a [for] loop to compute the inertia with each possible value of k.
- Create a dictionary with the data to plot the elbow curve.
- Plot a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.

<div style="width:60px ; height:60px">
![K-means Elbow](../Resources/K-means_elbow.png?raw=true "K-means Elbow")
<div>

### Cluster Cryptocurrencies with K-means Using the Original Scaled Data

I then clustered the cryptocurrencies for the best value for [k] on the original scaled data, using the following steps:
- Initialise the K-means model with the best value for [k].
- Fit the K-means model using the original scaled DataFrame.
- Predict the clusters to group the cryptocurrencies using the original scaled DataFrame.
- Create a copy of the original data and add a new column with the predicted clusters.
- Create a scatter plot using [hvPlot] as follows:
    - Set the x-axis as "PC1" and the y-axis as "PC2".
    - Colour the graph points with the labels found using K-means.
    - Add the "coin_id" column in the [hover_cols] parameter to identify the cryptocurrency represented by each data point.

### Optimise Clusters with Principal Component Analysis

Using the original scaled DataFrame, I performed a PCA and reduced the features to three principal components. About 89% of the total variance is condensed into the 3 PCA variables.
I then created a new DataFrame to include the PCA data, and set the "coin_id" as the index.

### Find the Best Value for k Using the PCA Data

I then used the elbow method on the PCA data to find the best value for [k]. 

### Cluster Cryptocurrencies with K-means Using the PCA Data

The same steps were taken as those with the original dataset, to cluster the cryptocurrencies for the best value for [k] on the PCA data, with the following amendments:
- Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
- Colour the graph points with the labels found using K-means.

### Observations and conclusions

Using the sclaled original dataframe, I determined that the best value for [k] is 4.

Using the PCA data, I determined that the best value for [k] is also 4, with no difference to the original data.

About 89% of the total variance is condensed into the 3 PCA variables.

After visually analysing the cluster analysis results side-by-side, using the PCA data makes the outliers seem more obvious, and the inertia between points is less. 
However, each cluster is as easily identifiable with little to no overlaps using either the K-means and PCA data, but with larger datasets this is might not be the case, therefore the PCA results would be more beneficial.

