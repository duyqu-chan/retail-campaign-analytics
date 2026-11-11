# Retail Campaign Analytics & Promotion Uplift Modeling

## Project Overview
This analysis aims to quantify the impact of promotional campaigns on sales performance. By clustering products and stores based on their baseline (non-promotion) velocity, this project measures the "promotion uplift" to provide data-driven recommendations for future marketing strategies.

## Executive Summary of Findings
* **Clustering Logic:** Products and stores are segmented into **Fast, Medium, and Slow** categories using the mean weekly sales per store during non-promotion periods through a quantile-based approach.
* **Top Performers:** **Fast items** drive the highest absolute volume increase, while certain **Medium items** exhibit the highest percentage "lift".
* **Store Sensitivity:** Fast Stores (Store Cluster 1) show the most stable reaction, whereas specific clusters demonstrate higher "Promo-Sensitivity".
* **Primary Driver:** The interaction between the **Promotion Period** and **Product Velocity** is typically the strongest predictor of sales change.
* **Statistical Significance:** There is a statistically significant difference in promotional lift between **Fast and Slow** cohorts, with Fast items and stores capturing the majority of the promotional ROI.

## Data Engineering & Preprocessing
* **Memory Optimization:** Evaluated the range of the quantity column and down-casted `SalesQuantity` to `int16` to efficiently reduce memory usage.
* **Zero-Filling Pipeline:** Created a skeleton DataFrame using `MultiIndex` for all unique Date, StoreCode, and ProductCode combinations to accurately fill missing combinations with zero sales. The interim dataset was saved in parquet format for efficient storage.
* **Promotion Event Alignment:** Standardized mixed date formats (month-first and day-first formats) across 6 distinct promotion periods. These periods align closely with major 2015 US retail events, including Valentine's Day, Memorial Day, Back-to-School, and Pre-Black Friday.

## Methodology: Performance Clustering
* **Baseline Calculation:** Filtered the dataset to isolate non-promotional days to establish organic sales baselines. 
* **Product Segmentation:** Calculated the total sales divided by the number of stores and total weeks for each product. Applied `pd.qcut` to separate items into 3 distinct quantiles (Slow, Medium, Fast).
* **Store Segmentation:** Grouped stores by weekly average sales during non-promotion periods and labeled them into Slow, Medium, and Fast tiers using quantiles.

## Installation & Usage
To run the analysis in your local environment:
1. Clone the repository:
   `git clone https://github.com/duyqu-chan/retail-campaign-analytics.git`
2. Install dependencies:
   `pip install -r requirements.txt`
3. Launch Jupyter Notebook and run `notebooks/01_campaign_uplift_analysis.ipynb`.