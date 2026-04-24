# B1. Problem Formulation
- ## (a)
    #### The target variable is the number of items sold, as the goal is to maximise sales.
    #### The input features could be store type, store size, monthly footfall, competition level, customer demographics, and promotion type. 
    #### This is a regression problem because we are trying to predict a number (items sold).


- ## (b)

    #### Using items sold is more reliable because it shows the actual demand for products, while revenue can be affected by prices, discounts, or different product costs. So, revenue may not clearly reflect how well a promotion works.

    #### This shows that in real-world ML projects, the target variable should be chosen carefully so that it directly represents the real goal and is not affected by unnecessary factors.



- ## (c)

    #### Instead of one global model, we can build separate models for different store types (urban, semi-urban, rural) or use a grouped approach. This is better because stores in different locations behave differently, so each model can learn patterns specific to that group and give more accurate results.


# B2. Data and EDA Strategy

- ## (a)
    #### Join all tables using store ID, promotion ID, and date. The final dataset has one row per store per month per promotion. Aggregate data such as total items sold, average footfall, and promotion-related summaries before modeling.


- ## (b)

    #### Before building the model, I would perform the following EDA:

    #### 1. Sales distribution (histogram)
         I would check how items sold are spread (normal or skewed).
         Helps decide if we need data transformation (like log).
    #### 2. Sales by promotion type (bar chart)
         I would compare average sales for each promotion.
         Helps understand which promotion performs better.
    #### 3.Sales by store type (urban, rural, etc.)
         I would check how different locations perform.
         Helps decide if we should build separate models or add store-type features.
    #### 4.Time-based trends (line chart over months)
        I would check seasonality (festivals, weekends).
         Helps create features like month, festival flag, etc.


- ## (c)
    #### This imbalance means the model will mostly learn from no-promotion data and may not understand how promotions affect sales. As a result, it may give poor predictions for promotion cases.

    #### To fix this, we can balance the data by oversampling promotion cases or undersampling non-promotion cases, and also give more importance (weights) to promotion data during training.



#  B3. Model Evaluation and Deployment

- ## (a)
    #### We should use a time-based split instead of a random split For example, use the first 2–2.5 years as training data and the last 6–12 months as test data.

    #### A random split is not appropriate because it mixes past and future data, which can cause the model to learn from future information. This gives unrealistic results.

#### For evaluation, we can use:

     MAE (Mean Absolute Error) → shows average error in number of items sold
     RMSE (Root Mean Squared Error) → gives more penalty to large errors

#### Interpretation:

    Lower MAE means predictions are closer to actual sales
    Lower RMSE means fewer large mistakes, which is important for business decisions

- ## (b) 

    #### I would use feature importance to see which factors are influencing the model’s decision in each month.

    #### For December, I would check which features (like festival season, high footfall, customer type) are important and leading to the recommendation of Loyalty Points Bonus.

    #### For March, I would again check feature importance to see if factors like lower demand or different customer behavior are making Flat Discount more effective.

    #### This shows that the model is reacting to changing conditions over time, such as seasonality, customer behavior, and store activity.

    #### To communicate this to the marketing team, I would explain in simple terms:
    #### “In December, customers are more active (festivals), so loyalty rewards work better. In March, demand is lower, so discounts help increase sales.”

- ## (c)
    #### First, after training, I would save the model using tools like joblib or pickle so it can be reused without training again.

    #### At the start of each month, I would collect new data (store details, recent footfall, calendar info, etc.) and apply the same preprocessing steps (like encoding, scaling, feature creation). Then this data is fed into the saved model to generate promotion recommendations for all stores.

    #### For monitoring, I would track:

    #### Prediction vs actual sales (to check accuracy)
    #### Error metrics like MAE over time
    #### Data changes (like sudden drop in footfall or new trends)

    #### If the error increases or data patterns change a lot, it means performance is dropping, so we should retrain the model with new data.