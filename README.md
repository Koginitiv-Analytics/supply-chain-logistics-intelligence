# 📦 Supply Chain Inventory & ABC Reorder Point Analysis

## 🎯 Executive Summary
This project analyzes a dataset of 100 SKUs to optimize inventory levels, establish automated safety stock/reorder thresholds, and perform ABC revenue classification to prevent stockouts on high-value products.

## 🛠️ Tech Stack & Domain Concepts
* **Language & Libraries:** Python (Pandas, NumPy)
* **Supply Chain Metrics:** Safety Stock, Reorder Point (ROP), ABC Inventory Classification (80/15/5 Revenue Split), Average Daily Sales

## 📊 Key Findings & Insights
* **Reorder Alerts:** Identified **42 out of 100 SKUs** currently sitting below their calculated Reorder Point.
* **Urgent Class A SKUs:** **36 of the 42 flagged SKUs** belong to **Class A** (top 80% revenue drivers). Immediate purchase orders are required to prevent revenue loss.

## 💻 Python Implementation (Calculations)
```python
# Reorder Point & Safety Stock
df['Avg_Daily_Sales'] = df['Order quantities'] / 30
df['Safety_Stock'] = np.ceil(df['Avg_Daily_Sales'] * 3)
df['Reorder_Point'] = np.ceil((df['Avg_Daily_Sales'] * df['Lead times']) + df['Safety_Stock'])
df['Reorder_Alert'] = df['Stock levels'] < df['Reorder_Point']

# ABC Inventory Categorization
df['Cum_Percen'] = (df['Total_Revenue'].cumsum() / df['Total_Revenue'].sum()) * 10
