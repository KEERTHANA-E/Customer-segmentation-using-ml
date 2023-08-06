# Customer-segmentation-using-ml

## Introduction

This project delves into customer segmentation and reorder prediction, utilizing machine learning to uncover behavior patterns. By categorizing customers and predicting their next purchases, businesses can tailor strategies for targeted marketing and efficient inventory management, fostering enhanced customer engagement and satisfaction.

### Objectives:

- Evaluate anonymized [data](https://www.kaggle.com/c/instacart-market-basket-analysis/data) comprising 3 million grocery orders by over 200,000 Instacart users, generously provided by Instacart.
- To discover underlying product and user correlations to enhance cross-selling and upselling strategies.
- Perform customer segmentation for focused marketing and predict customer behavior.
- Developed a Machine Learning model to predict which previously purchased product will include be in user’s next order

### Project Methodology

```
 Plots/                                      : Contains all plots
 Data Description and Analysis.ipynb         : Initial analysis to understand data
 Exploratory Data Analysis.ipynb             : EDA to analyze customer purchase pattern
 Customers Segmentation.ipynb                : Customer Segmentation based on product aisles
 XGBoost Model.ipynb                         : XGBoost model for product reorder prediction
```

<br />

## Data Description

- **aisles:** This dataset includes various aisles, encompassing a total of 134 distinct aisles.

- **departments:** Within this dataset, numerous departments are featured, amounting to a total of 21 unique departments.

- **orders:** This dataset documents all orders placed by diverse users. The ensuing analysis reveals the subsequent findings.
<p align="center">
  <img width="300" height="200" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/dow.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/orders.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/heatmap.png">
</p>

- **products:** With 49,688 items and corresponding aisle and department details, this dataset is a comprehensive product catalog.

- **order_products_prior:** This dataset reveals product order sequences and reordering details:
  - Encompasses details on 3,214,874 orders containing 49,677 products.
  - The percentage of reorder items in this set is 58.97%.

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/prior.png">
</p>
    
    
- **order_products_train:** This dataset echoes order-product associations and reordering data:
  
    - Covers 131,209 orders and 39,123 products.
    - The percentage of reorder items in this set is 59.86%.

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/train.png">
</p>

## Exploratory Data Analysis

For the analysis, I merged individual data files into a unified dataframe. To accommodate it within memory, I halved its size to 50% (from 4.1 GB to 2.0 GB) through type conversion while retaining all information intact.

- The following visualization illustrates the highest-ranking aisles determined by the total purchased products.

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/popular-aisles.png">
</p>

- As evident from the chart below, day-to-day food items exhibit a notably high reorder percentage. Conversely, products like vitamins, first-aid supplies, and beauty items display a lower reorder percentage. This aligns with the expected pattern, given that we frequently purchase groceries while not acquiring these items in every order.

<p align="center">
<img width="400" height="220" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/aisle-high-reorder.png"> 
<img width="400" height="220" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/aisle-low-reorder.png"> 
</p>

## Customer Segmentation

Customer segmentation involves categorizing customers into clusters sharing similar traits, enabling companies to tailor effective and relevant marketing strategies. This can be achieved by analyzing users' purchased products data. Given the extensive range of products and customers, I opted to use aisles which represent categories of products.
We have performed Principal component analysis to reduce dimensions, as KMeans does not produce the best results on higher dimensions. Using 10 principal components, we conducted K-means clustering. We have chosen the optimal number of clusters as 5 using the elbow method shown below.

<p align="center">
  <img width="600" height="300" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/elbow.png">
</p>

The clustering can be observed below along the first two main components.

<p align="center">
  <img width="600" height="400" src="https://github.com/KEERTHANA-E/Customer-segmentation-using-ml/blob/main/Plots/cluster.png">
</p>

The clustering creates into 5 organized clusters and after checking most common products, we can conclude following:

- Cluster 1 results into 5428 consumers who mostly order water seltzer sparkling water aisle.
- Cluster 2 results into 55784 consumers who mostly order fresh vegetables followed by fruits.
- Cluster 3 results into 7948 consumers who mostly order packaged produce and fresh fruits.
- Cluster 4 results into 37949 consumers who mostly order fruits followed by fresh vegetables.
- Cluster 5 results into 99100 consumers who orders products from many aisles. Their mean orders are low compared to other clusters which tells us that either they are not frequent users of Instacart or they are new users and do not have many orders yet.

## XGBoost Model:

XGBoost is a high-performance machine learning algorithm that excels at predictive tasks. It utilizes an ensemble of decision trees, optimizing both speed and accuracy, making it a preferred choice for various applications, including regression, classification, and ranking tasks. So,we have selected the XGBoost model to build an ML model that predicts which previously purchased product will be in the user’s next order.

- Below is the comprehensive classification report for the XGBoost model:
<p align="center">
  <img width="400" height="200" src="https://github.com/archd3sai/Instacart-Market-Basket-Analysis/blob/master/Plots/XGBoost-Report.png">
</p>

- Below is the confusion matrix, an essential tool for understanding the XGBoost model's performance:
<p align="center">
  <img width="600" height="300" src="https://github.com/archd3sai/Instacart-Market-Basket-Analysis/blob/master/Plots/XGBoost%20Performance.png">
</p>
