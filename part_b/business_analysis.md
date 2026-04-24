## B1. Problem Formulation

### (a) 

In this problem, the goal is to predict the number of items sold in a store based on different factors such as promotion type, store size, location type, and other variables.

The target variable here is **items_sold**, as the company wants to maximize the number of items sold.

The input features can include:
- promotion_type  
- store_size  
- location_type  
- competition_density  
- is_weekend  
- is_festival  
- month, year, day_of_week  

This is a **supervised machine learning problem**, specifically a **regression problem**, because the target variable (items_sold) is a continuous numerical value.

---

### (b)

Using total sales revenue may not always give a clear picture of performance because revenue can be affected by price changes, discounts, or product mix.

On the other hand, **items sold (sales volume)** is a more reliable measure because it directly shows how many products customers are buying, regardless of price variations.

This highlights an important principle in machine learning:  
**the target variable should be chosen carefully so that it truly reflects the business objective.**

---

### (c)

Using a single global model for all 50 stores may not give the best results because stores in different locations (urban, semi-urban, rural) may respond differently to promotions.

A better approach would be to:
- either build **separate models for different store types or locations**,  
- or include location-related features so the model can learn these differences.

This helps capture store-specific behavior and improves prediction accuracy.



## B2. Data and EDA Strategy

### (a)

The data is available in four different tables: transactions, store attributes, promotion details, and calendar data. These tables can be joined using common keys such as store_id and transaction_date.

First, the transactions table can be joined with the store attributes table using store_id. Then, promotion details can be joined based on promotion_type. Finally, the calendar table can be merged using transaction_date to include features like weekend and festival.

The final dataset should have one row representing **a single store’s transaction on a specific date**.

Before modelling, some aggregations can be done, such as:
- total items sold per store per day  
- average sales during promotions  
- grouping by month or weekday to identify patterns  

---

### (b)

Before building a model, the following EDA steps can be performed:

1. **Sales distribution plot**  
   To understand how items_sold is distributed and check for skewness or outliers.

2. **Sales vs promotion type**  
   To see which promotions lead to higher sales and identify effective strategies.

3. **Sales over time (trend analysis)**  
   To identify seasonal patterns such as monthly or weekly trends.

4. **Correlation analysis**  
   To understand relationships between numerical variables like competition_density and items_sold.

These analyses help in selecting important features and improving model performance.

---

### (c)

If 80% of transactions have no promotion, it creates a class imbalance in the data. This means the model may learn more about non-promotion cases and may not perform well in predicting the effect of promotions.

To handle this, we can:
- ensure proper feature representation of promotion types  
- use techniques like stratified sampling  
- focus on evaluation metrics carefully  

This helps the model learn patterns from both promotion and non-promotion data.





## B3. Model Evaluation and Deployment

### (a)

Since the data is time-based (monthly data over 3 years), the train-test split should be done based on time rather than randomly. The earlier data should be used for training, and the most recent data should be used for testing.

A random split is not appropriate because it can mix past and future data, which may lead to data leakage and unrealistic performance.

For evaluation, metrics like **RMSE and MAE** can be used:
- RMSE gives higher penalty to large errors and helps understand how far predictions are from actual values.
- MAE gives the average error in a simple and interpretable way.

These metrics help in understanding how accurate the model’s predictions are in terms of actual sales.

---

### (b)

If the model recommends different promotions for the same store in different months, it means that the model is considering time-based factors and other features.

Using feature importance, we can check which features influenced the decision. For example, month, promotion_type, or competition_density may have different impacts in different months.

This can be explained to the marketing team by showing that customer behavior changes over time, and the model adapts to these changes to suggest the most effective promotion.

---

### (c)

For deployment, the trained model can be saved using tools like joblib or pickle.

Each month, new data (such as store details, calendar features, and promotion options) will be prepared in the same format as the training data and passed to the model to generate predictions.

To monitor performance, we can track prediction errors over time. If the error starts increasing significantly, it may indicate that the model is no longer performing well, and retraining is required.

This ensures that the model remains accurate and useful for decision-making.

