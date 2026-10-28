# 🪔 Diwali Sales Analysis (Python)

Exploratory Data Analysis (EDA) of Diwali festival sales data using **Python, Pandas, Matplotlib and Seaborn**. The goal is to understand *who* buys during Diwali, *where* they are from, and *what* they buy, so that a business can target the right customers and improve sales.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation & Usage](#-installation--usage)
- [Data Cleaning](#-data-cleaning)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Key Insights](#-key-insights)
- [Conclusion](#-conclusion)

---

## 📖 Project Overview

Every festive season, retailers want to know which customer segments drive the most revenue. This project cleans a Diwali sales dataset and analyses it across multiple dimensions:

- Gender
- Age group
- State / Zone
- Marital status
- Occupation
- Product category and product ID

---

## 📂 Dataset

**File:** `Diwali Sales Data.csv`  
**Size:** 11,251 rows × 15 columns

| Column | Description |
|---|---|
| `User_ID` | Unique customer ID |
| `Cust_name` | Customer name |
| `Product_ID` | Unique product ID |
| `Gender` | Gender of the customer (M/F) |
| `Age Group` | Age bracket (e.g. 26-35) |
| `Age` | Age of the customer |
| `Marital_Status` | 0 = Unmarried, 1 = Married |
| `State` | State of the customer |
| `Zone` | Geographic zone (Central, Southern, etc.) |
| `Occupation` | Customer's occupation / sector |
| `Product_Category` | Category of the purchased product |
| `Orders` | Number of orders placed |
| `Amount` | Order amount (₹) |
| `Status`, `unnamed1` | Empty columns (dropped during cleaning) |

---

## 🛠 Tech Stack

- **Python 3**
- **NumPy**: numerical operations
- **Pandas**: data manipulation and analysis
- **Matplotlib**: plotting
- **Seaborn**: statistical visualisation
- **Jupyter Notebook**

---

## 🗂 Project Structure

```
Python_Diwali_Sales_Analysis/
│
├── Diwali Sales Data.csv          # Raw dataset
├── Diwali_Sales_Analysis.ipynb    # Analysis notebook
└── README.md
```

---

## ⚙️ Installation & Usage

**1. Clone the repository**

```bash
git clone https://github.com/rishabhnmishra/Python_Diwali_Sales_Analysis.git
cd Python_Diwali_Sales_Analysis
```

**2. Install the dependencies**

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

**3. Launch the notebook**

```bash
jupyter notebook Diwali_Sales_Analysis.ipynb
```

---

## 🧹 Data Cleaning

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
df = pd.read_csv('Diwali Sales Data.csv', encoding='unicode_escape')

# Drop unrelated / blank columns
df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

# Check and drop null values
pd.isnull(df).sum()
df.dropna(inplace=True)

# Change data type
df['Amount'] = df['Amount'].astype('int')
```

Steps performed:

1. Loaded the CSV with `unicode_escape` encoding.
2. Dropped the two completely empty columns (`Status`, `unnamed1`).
3. Removed rows with null values (12 missing `Amount` entries).
4. Converted `Amount` from `float` to `int`.
5. Generated summary statistics with `describe()`.

---

## 📊 Exploratory Data Analysis

Example of the analysis pattern used throughout the notebook:

```python
# Total sales amount by gender
sales_gen = (
    df.groupby(['Gender'], as_index=False)['Amount']
      .sum()
      .sort_values(by='Amount', ascending=False)
)
sns.barplot(x='Gender', y='Amount', data=sales_gen)
```

The notebook analyses both **order counts** (`countplot`) and **total sales amount** (`groupby` + `barplot`) for each of these dimensions:

| Dimension | Analysis |
|---|---|
| Gender | Buyer count and total spend |
| Age Group | Buyer count by gender and total spend |
| State | Top 10 states by orders and by sales |
| Marital Status | Buyer count and spend split by gender |
| Occupation | Buyer count and total spend |
| Product Category | Most sold categories and revenue |
| Product ID | Top 10 most sold products |

---

## 💡 Key Insights

- **Gender:** Most buyers are women, and they also have higher purchasing power than men.
- **Age:** The 26–35 age group contributes the most buyers and revenue.
- **Geography:** Uttar Pradesh, Maharashtra and Karnataka lead in orders and sales.
- **Marital status:** Married women are the biggest spenders.
- **Occupation:** Most buyers work in IT, Healthcare and Aviation.
- **Products:** Food, Clothing and Electronics are the top-selling categories.

---

## ✅ Conclusion

> **Married women aged 26–35 from Uttar Pradesh, Maharashtra and Karnataka, working in IT, Healthcare and Aviation, are most likely to buy products from the Food, Clothing and Electronics categories.**

Businesses can use these insights to target marketing campaigns, plan inventory and personalise festive offers.
