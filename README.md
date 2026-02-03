# Industrial-Demand-Forecasting-Pipeline  
## Engineering Insights from 15M+ Transactions

**High-Throughput ETL | Machine Learning at Scale | Supply Chain Optimization**

---

## 📖 The Narrative: Scaling Intelligence from Berlin to Global Markets

In enterprise retail, the true challenge isn't just accumulating data—it’s the architectural speed at which you can transform **15,275,490 raw transaction records** into a precise roadmap for inventory growth.

This project documents the design of a **production-grade Machine Learning pipeline** deployed in the cloud, built to handle high-velocity retail data and predict complex demand patterns across ten Walmart stores. The system emphasizes **memory efficiency**, **computational speed**, and **future-facing generalization**.

---

## 🏗️ Chapter 1: The Ingestion Layer (Kaggle → Colab Cloud)

Processing over 15 million records requires more than a standard script—it demands a cloud-native ecosystem capable of handling deeply structured data at scale.

- **API Orchestration**  
  Engineered a secure ingestion bridge using the Kaggle API to stream raw Walmart CSV assets directly into a high-performance cloud environment.

- **Memory-Safe Loading**  
  Designed a custom **downcasting function** to iteratively convert high-precision numeric columns into memory-efficient types (`int8`, `int16`, `float32`), reducing RAM usage by **~70%**.

- **Storage Architecture**  
  Consolidated five disparate datasets—**Sales**, **Calendar**, and **Prices**—into a unified project directory (`m5_data`) to ensure low-latency access during training and feature generation.

---

## ⚙️ Chapter 2: Performance Engineering & ETL

To extract value from a dataset of this scale, the ETL pipeline was engineered as a multi-stage transformation system focused on efficiency and analytical depth.

- **Wide-to-Long Transformation ("Melt")**  
  Converted daily sales columns into a long-format structure, producing **15,275,490 individual event rows** and enabling sequential temporal learning.

- **Spatial & Temporal Merging**  
  Integrated global holiday calendars and **SNAP (Supplemental Nutrition Assistance Program)** indicators to contextualize demand shifts driven by external factors.

- **Feature Engineering**  
  - **Autoregressive Lag (`lag_1`)** to capture short-term momentum  
  - **7-Day Rolling Mean** to encode trend maturity and smoothing effects  

---

## ⚖️ Chapter 3: The LightGBM Framework

Retail demand modeling is as much about selecting the right objective function as it is about engineering features.

- **Sparsity Management**  
  Adopted the **Tweedie regression objective**, ideal for modeling zero-inflated sales distributions common in retail time series.

- **Validation Architecture**  
  Implemented a **90/10 temporal split**, training on **13,747,941 rows** and validating on the most recent sales window to ensure forward-looking generalization.

- **Optimization Strategy**  
  - Leveraged **Lazy Evaluation** via LightGBM’s dataset structure  
  - Applied **Early Stopping** callbacks to prevent overfitting while preserving compute efficiency  

---

## 📊 Business Intelligence Insights

Key signals extracted from the **15,275,490-record dataset**:

| Feature | Strategic Impact |
|------|------------------|
| **Lag_1 (Recency)** | Strongest predictor of demand, confirming short-term momentum dominance |
| **Sell Price** | High elasticity revealed opportunities for discount and revenue optimization |
| **Weekday (wday)** | Captured weekly seasonality, informing logistics and weekend demand surges |
| **Event Effects** | Quantified holiday-driven demand shifts for demographic-aware inventory planning |

---

## 🚀 Deployment & Cloud Execution

The pipeline outputs a **28-day future forecast**, visualized for high-engagement product zones.

```python
# Final Forecast Submission Generation
# Selected Item: HOBBIES_2_085_CA_1_evaluation

preds = model.predict(sample_data[features])

plt.plot(sample_data['date'], sample_data['sales'], label='Actual Sales')
plt.plot(sample_data['date'], preds, label='Model Prediction', linestyle='--')
plt.legend()
plt.show()
