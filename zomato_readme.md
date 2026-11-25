# 🍽️ Zomato Exploratory Data Analysis (EDA)

## 📌 Project Overview

This project performs Exploratory Data Analysis (EDA) on the Zomato Restaurant Dataset using Python. The goal is to understand restaurant ratings, country-wise distribution, online delivery availability, currency usage, and other business insights.

The analysis is performed using:

- Pandas
- NumPy
- Matplotlib
- Seaborn

---

## 📂 Dataset Information

This project uses two datasets:

### 1. zomato.csv
Contains restaurant-related information such as:

- Restaurant Name
- Country Code
- City
- Cuisines
- Average Cost for Two
- Currency
- Online Delivery
- Table Booking
- Aggregate Rating
- Votes

### 2. Zomato_CountryCode.xlsx
Contains mapping between:

- Country Code
- Country Name

This dataset is used to identify the countries corresponding to country codes in the main dataset.

---

## 🛠️ Technologies Used

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## 🔍 Project Workflow

### Step 1: Import Libraries

Required libraries were imported for data manipulation, analysis, and visualization.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

### Step 2: Load the Dataset

```python
df_countrycode = pd.read_excel("Zomato_CountryCode.xlsx")
df_data = pd.read_csv("zomato.csv", encoding="latin-1")
```

---

### Step 3: Initial Data Exploration

#### Display First Five Rows

```python
df_data.head()
```

This helps understand the dataset structure and available columns.

#### Dataset Information

```python
df_data.info()
```

**Observations:**

- Total Rows: 9551
- Total Columns: 21
- Mix of numerical and categorical features
- One column contains missing values

---

### Step 4: Statistical Summary

```python
df_data.describe()
```

This provides:

- Mean
- Median
- Standard Deviation
- Minimum Values
- Maximum Values
- Quartiles

for all numerical columns.

---

### Step 5: Missing Value Analysis

```python
df_data.isnull().sum()
```

**Results:**

| Column | Missing Values |
|----------|----------|
| Cuisines | 9 |

Only the **Cuisines** column contains missing values.

---

### Step 6: Merge Dataset

To identify country names, both datasets were merged using the Country Code column.

```python
final_df = pd.merge(
    df_data,
    df_countrycode,
    on="Country Code",
    how="left"
)
```

This added a new column:

- Country

---

## 🌍 Country-wise Analysis

### Restaurant Distribution by Country

```python
final_df.Country.value_counts()
```

### Top Countries

| Country | Restaurants |
|----------|------------|
| India | 8652 |
| United States | 434 |
| United Kingdom | 80 |

### Key Observation

More than 90% of restaurants in the dataset belong to India.

---

### Country Distribution Visualization

```python
plt.pie(countryvalues[:3], labels=countrynames[:3])
plt.show()
```

The pie chart shows the restaurant contribution of the top three countries.

---

## ⭐ Rating Analysis

### Create Rating Summary

```python
ratings = final_df.groupby(
    ['Aggregate rating',
     'Rating color',
     'Rating text']
).size().reset_index().rename(
    columns={0:'Rating Count'}
)
```

---

### Rating Categories

| Rating Color | Rating Description |
|-------------|-------------------|
| White | Not Rated |
| Red | Poor |
| Orange | Average |
| Yellow | Good |
| Green | Very Good |
| Dark Green | Excellent |

---

### Rating Visualization

```python
sns.barplot(
    x='Aggregate rating',
    y='Rating Count',
    hue='Rating color',
    data=ratings
)
```

### Key Findings

- Many restaurants are not rated.
- Most restaurants fall into the Average and Good categories.
- Very few restaurants have Excellent ratings.

---

## ❌ Country-wise Unrated Restaurants

Restaurants with White rating color are considered "Not Rated".

### Analysis

```python
final_df[final_df['Rating color'] == 'White'] \
.groupby('Country') \
.size() \
.reset_index()
```

### Results

| Country | Count |
|----------|--------|
| India | 2139 |
| Brazil | 5 |
| United States | 3 |
| United Kingdom | 1 |

### Observation

India has the highest number of unrated restaurants.

---

## 💰 Currency Analysis

Identify currencies used in different countries.

```python
final_df[['Country','Currency']] \
.groupby(['Country','Currency']) \
.size() \
.reset_index()
```

### Sample Results

| Country | Currency |
|----------|-----------|
| India | Indian Rupees (Rs.) |
| United States | Dollar ($) |
| United Kingdom | Pounds (£) |
| UAE | Emirati Dirham (AED) |
| Turkey | Turkish Lira (TL) |

### Observation

Every country uses its own local currency for restaurant transactions.

---

## 🚚 Online Delivery Analysis

Find countries that support online delivery.

```python
final_df[
    final_df['Has Online delivery'] == 'Yes'
].Country.value_counts()
```

### Results

| Country | Restaurants with Online Delivery |
|----------|------------|
| India | 2423 |
| UAE | 28 |

### Observation

Online delivery is available only in:

- 🇮🇳 India
- 🇦🇪 UAE

India has the highest number of restaurants providing online delivery services.

---

## 📈 Key Insights

### 1. India Dominates the Dataset

- 8652 restaurants belong to India.
- More than 90% of the dataset represents Indian restaurants.

### 2. Minimal Missing Data

- Only 9 missing values were found.
- Missing values exist only in the Cuisines column.

### 3. Ratings Distribution

- A significant number of restaurants are not rated.
- Average and Good ratings are the most common.

### 4. Online Delivery Availability

- Available only in India and UAE.
- India leads in online delivery adoption.

### 5. Currency Diversity

- Different countries use different currencies.
- Useful for region-wise business analysis.

---

## 🚀 Future Improvements

Further analysis can be performed on:

- Top Cities by Restaurant Count
- Most Popular Cuisines
- Cost vs Rating Analysis
- City-wise Restaurant Distribution
- Votes vs Ratings Analysis
- Geographic Mapping using Latitude and Longitude
- Interactive Dashboards using Power BI or Plotly

---

## 📁 Project Structure

```
Zomato-EDA/
│
├── Dataset/
│   ├── zomato.csv
│   └── Zomato_CountryCode.xlsx
│
├── Zomato_EDA.ipynb
├── README.md
└── requirements.txt
```

---

## 👨‍💻 Author

**Krishna**

Aspiring Data Analyst | Machine Learning Enthusiast

---

⭐ If you found this project helpful, consider giving it a star on GitHub.