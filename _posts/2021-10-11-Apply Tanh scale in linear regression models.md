![](/images/tanh_blog/tanh.png)
>tanh(x/a)

## In this blog i´ll show you how i use tanh scale  for reduce the error of linear regression models

I prove this scale in two projects
- [California housing prices](https://www.kaggle.com/camnugent/california-housing-prices) from kaggle
and
- León housing rents prices, i make this dataset.

In this two cases i´ve better results than apply linear regression model with other scale mathods. 

### Scaling process

For scale i use the next form of **tanh function**:

$$
featureScaled = \tanh\left(\frac{feature}{mean(feature)} \right)
$$

When the denominator is bigger, the function tends to be most smooth. In this cases the outliers helps to increase the mean value and smooth the curve.

First take a look of the datasets distribution

> California Housing distribution
![](/images/tanh_blog/california_dist.png)

> León Housing distribution
![](/images/tanh_blog/leon_dist.png)

In both cases can see the  distribution concentrate the mean at left and had a long tail at right.

Now i proceed to scale the data. According to the scalation formula:
For this process just need 


    import numpy as np

    #scale train data

    for col in X_train_scaled.columns:
        X_train_scaled[col] = np.tanh(X_train_scaled[col] / np.mean(X_train_scaled[col]))

    y_train_scaled = np.tanh(y_train_scaled / np.mean(y_train_scaled)) 


    # scale test data

    for col in X_test_scaled.columns:
        X_test_scaled[col] = np.tanh(X_test_scaled[col] / np.mean(X_test_scaled[col]))
    y_test_scaled = np.tanh(y_test_scaled / np.mean(y_test_scaled)) 

I scale train and test in different sets for don't to exchange information between they.

For this problem i scaled the features data and target data with **tanh function**, and with the others scales just scale 
the feature data, in this way i get the best results.

Later scale both dataset:

> California housing scaled
![](/images/tanh_blog/california_dist_scaled.png)

> León housing scaled
![](/images/tanh_blog/leon_dist_scaled.png)

The result a distribution with values between 0 to 1, but looks like a half to normal distribution in California's dataset, in León's dataset don't looks a shape of distribution knewed, but the size of california's dataset is bigger than León's dataset so... its ok.

### Linear Regression

Now for make the linear regression, i'll compare different methods.

    # import methods to make Linear Regression

    from sklearn.linear_model import LinearRegression, Ridge, Lasso
    from sklearn.tree import DecisionTreeRegressor
    from sklearn.ensemble import RandomForestRegressor 

    # for compute the error

    from sklearn.metrics import mean_squared_error

And to compare scalers, i'll use this different methods:

    from sklearn.preprocessing import StandardScaler
    from sklearn.preprocessing import MinMaxScaler
    from sklearn.preprocessing import RobustScaler
    from sklearn.preprocessing import PowerTransformer


#### After compute the model the results are:

And rescaling **tanh scale** result look at the rmse of each model

> California housing results
![](/images/tanh_blog/california_results_rescaledd.png)


#### Now let's compare with León housing results

Rescaling tanh scale results i get the next rmse

> León housing results
![](/images/tanh_blog/leon_results_rescaled.png)


Looking the results it can be seen that **tanh scale** give the best results.



