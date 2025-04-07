![Distribution plot](https://github.com/benjaminlaeuchli/lemoncar/blob/main/Numerical%20Distribution%20plot.png?raw=true)


# Auto Dealership Kick Prediction Model

## Description

Auto dealerships face a significant challenge when purchasing used cars at auctions, with the risk of buying vehicles that turn out to be "kicks" (bad buys). These cars often have hidden mechanical issues, tampered odometers, or problems with the vehicle title that make them unsellable, leading to financial losses for dealerships. The goal of this project is to predict whether a car purchased at an auction will be a kick, allowing dealerships to make more informed decisions, avoid costly mistakes, and improve their inventory selection.

## Objective

The objective is to build a model that predicts whether a car bought at an auto auction will be a bad buy (kick). This model helps dealerships identify high-risk vehicles before making a purchase, ultimately saving money on repairs, transportation costs, and losses from reselling problematic cars.

## Key Features

- **VehicleAge**: Age of the vehicle at the time of purchase.
- **VehBCost**: Base cost of the vehicle.
- **MMRAcquisitionAuctionAveragePrice**: Average price at the acquisition auction.
- **VehOdo**: Odometer reading (mileage).
- **MMRCurrentAuctionAveragePrice**: Average price at the current auction.
- **MMRCurrentRetailAveragePrice**: Average retail price of the vehicle.
- **WarrantyCost**: Cost of any warranties associated with the vehicle.

## Model Selection Journey

When I started this project, my first instinct was to try out several classic models that might work well for this problem: **KNN**, **Logistic Regression**, and **Decision Trees**. I felt these models could give me a good start, and so I evaluated them carefully based on their ability to predict whether a car was a kick or not.

### KNN

The **K-Nearest Neighbors (KNN)** model provided decent recall, which meant it could identify a fair number of actual "kick" cars. However, KNN's **precision** was quite low, meaning it also classified many good cars as kicks, leading to a high number of false positives. This resulted in a **low F1-score**, and the model just wasn’t reliable enough for identifying which cars would actually turn out to be bad buys.

### Decision Trees

Next, I tried **Decision Trees**, which are easy to interpret and understand. They showed better precision compared to KNN, but their **recall** for the minority class (kick cars) was still relatively poor. This imbalance in precision and recall left the model lacking when it came to identifying all of the potentially problematic cars. I realized I needed something that could strike a better balance between these two metrics.

### Logistic Regression

I then tested **Logistic Regression**, which gave a solid **recall** (it could identify many of the kick cars) but still suffered from a **low precision**. This imbalance was a recurring issue across the models I tried—high recall, but poor precision, leading to suboptimal F1-scores.

### The Shift to Random Forest

After seeing the results from KNN, Decision Trees, and Logistic Regression, it became clear that I needed a model that could better balance **precision** and **recall**, especially when handling the **class imbalance**. I wanted a more robust and reliable model that could also capture the **non-linear relationships** in the data that these simpler models struggled with.

This is when I decided to switch to a **Random Forest** pipeline. **Random Forest** is an **ensemble method**, meaning it aggregates the predictions of multiple decision trees, which helps smooth out the biases that individual trees might introduce. This ensemble approach allows Random Forest to better handle class imbalance and provide a more accurate balance between precision and recall.

Additionally, Random Forest is particularly good at capturing **complex, non-linear relationships** in the data—something that KNN, Logistic Regression, and Decision Trees were not fully capable of. The ensemble nature of Random Forest helps improve **generalization**, reducing the risk of overfitting to the training data.

### Why Random Forest?

- **Better Precision and Recall**: The Random Forest model offered a more balanced tradeoff between precision and recall, crucial for identifying problematic cars while minimizing false positives.
- **Ensemble Power**: By aggregating predictions from multiple trees, Random Forest helped mitigate biases and overfitting.
- **Non-linear Relationships**: Random Forest can capture complex patterns in the data that simpler models might miss, improving overall prediction accuracy.

## Feature Importance

Once I had settled on the Random Forest model, I also took a closer look at the **feature importance** scores. These scores tell us which features are most influential in predicting whether a car will be a kick. The top features identified were:

1. **VehicleAge** (Importance Score: 0.079797)
2. **VehBCost** (Importance Score: 0.048676)
3. **MMRAcquisitionAuctionAveragePrice** (Importance Score: 0.047091)
4. **VehOdo** (Importance Score: 0.046200)
5. **MMRCurrentAuctionAveragePrice** (Importance Score: 0.046138)

These features were most predictive of whether a car would turn out to be a kick. For example, **VehicleAge** was particularly important, suggesting that older cars are more likely to have hidden issues. While the importance scores may seem low (ranging from 0 to 1), they are normalized and reflect the relative influence of each feature.

## Conclusion

Switching to **Random Forest** proved to be the right decision after evaluating the performance of KNN, Decision Trees, and Logistic Regression. The Random Forest model offered a **better balance** between precision and recall, which was essential for correctly identifying kick cars. Its ability to handle **class imbalance**, capture **non-linear relationships**, and **generalize** better made it a more suitable choice for predicting bad buys.

By using Random Forest, dealerships can make more informed decisions, avoiding costly mistakes when purchasing cars at auctions. This model helps to save on repair costs, transportation fees, and market losses, ultimately improving both profitability and customer satisfaction.
