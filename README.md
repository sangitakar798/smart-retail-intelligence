# 🌦️ India Weather Analysis & Heatwave Detection

---

## 📌 Project Overview

This project focuses on analyzing weather data across India to identify heatwave-prone regions, understand temperature trends, and explore relationships between different weather parameters.

**The workflow includes:**
- 🐍 Data Cleaning & Preprocessing (Python)
- 🗄️ SQL-based Analysis (MySQL)
- 📊 Data Visualization (Power BI & Python)

---

## 🎯 Objectives

- Identify locations with the highest heatwave occurrences
- Analyze temperature trends over time
- Study relationships between weather variables
- Build an interactive dashboard for insights

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| **Python** | Pandas, NumPy, Matplotlib, Seaborn, Folium |
| **SQL** | MySQL |
| **Visualization** | Power BI |
| **Database Connection** | SQLAlchemy |

---

## 📂 Dataset

Weather dataset containing:

| Feature | Description |
|---------|-------------|
| `temperature_min` / `temperature_max` | Daily temperature range |
| `humidity` | Relative humidity |
| `rainfall` / `snowfall` | Precipitation values |
| `wind_speed` | Wind speed |
| `pressure` | Atmospheric pressure |
| `heatwave` | Heatwave indicator (0 = No, 1 = Yes) |
| `latitude` / `longitude` | Geographic coordinates |

---

## ⚙️ Data Cleaning Steps

- **Missing Values** handled using:
  - Mean / Median imputation
  - Domain-based filling (e.g., `rainfall = 0`)
- Removed **duplicate records**
- Fixed **invalid negative values**
- Treated **outliers** using IQR capping method
- Converted `date` column to `datetime` format
- **Extracted features:**
  - Year, Month, Day
  - Day name, Weekend flag

---

## 🗄️ SQL Analysis

### 🔹 Heatwave by Location

```sql
SELECT latitude, longitude, SUM(heatwave) AS total_heatwaves
FROM india_weather_data
GROUP BY latitude, longitude
ORDER BY total_heatwaves DESC;
```

### 🔹 Monthly Heatwave Trend

```sql
SELECT EXTRACT(MONTH FROM date) AS month,
       SUM(heatwave) AS total_heatwaves
FROM india_weather_data
GROUP BY month
ORDER BY month;
```

### 🔹 Average Temperature by Region

```sql
SELECT latitude, longitude,
       AVG(temperature_max) AS avg_max_temp,
       AVG(temperature_min) AS avg_min_temp
FROM india_weather_data
GROUP BY latitude, longitude
ORDER BY avg_max_temp DESC;
```

### 🔹 Yearly Heatwave Summary

```sql
SELECT EXTRACT(YEAR FROM date) AS year,
       SUM(heatwave) AS total_heatwaves,
       AVG(temperature_max) AS avg_max_temp
FROM india_weather_data
GROUP BY year
ORDER BY year;
```

---

## 📊 Visualizations

### 🔥 Heatwave Hotspots (Map)
- Identified regions with highest heatwave frequency using latitude & longitude
- Interactive maps created using **Folium** and **Power BI**

### 📈 Temperature Trend
- Line chart showing temperature variation over time

### 📅 Monthly Analysis
- Bar chart for average temperature by month

### 🌧️ Rainfall Distribution
- Histogram showing rainfall patterns

### 🔗 Correlation Heatmap
- Identified relationships between:
  - Temperature
  - Humidity
  - Rainfall
  - Pressure

---

## 📍 Key Insights

- ✅ Certain regions show **consistently high heatwave occurrences**
- ✅ **Strong correlation** between max and min temperature
- ✅ Humidity variables are **highly correlated**
- ✅ Rainfall is **moderately linked** with cloud cover
- ✅ **Seasonal patterns** clearly visible in temperature trends

---

## 📊 Power BI Dashboard

The dashboard includes:

| Component | Description |
|-----------|-------------|
| 🌍 **Heatwave Map** | Geographical analysis of heatwave-prone zones |
| 📈 **Time-Series Trend** | Heatwave occurrences over time |
| 📊 **Monthly Comparison** | Average temperature by month |
| 📌 **KPI Cards** | Total Heatwaves, Avg Temperature, Total Rainfall |
| 🎛️ **Interactive Filters** | Year, Month slicers |

---

## 🚀 How to Run

### 1. Clone Repository

```bash
git clone https://github.com/your-username/weather-analysis.git
cd weather-analysis
```

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn folium sqlalchemy pymysql
```

### 3. Run Python Script

```bash
python weather_analysis.py
```

> Performs data cleaning, preprocessing, and generates visualizations.

### 4. Load Data into MySQL

```python
from sqlalchemy import create_engine

engine = create_engine("mysql+pymysql://username:password@localhost/weather_db")
df.to_sql('india_weather_data', engine, if_exists='replace', index=False)
```

### 5. Connect Power BI

- Open **Power BI Desktop**
- Use **MySQL connector** → Enter host and credentials
- Load the `india_weather_data` table
- Build the dashboard using the loaded data

---

## 📁 Project Structure

```
weather-analysis/
│
├── data/
│   └── india_weather_data.csv       # Raw dataset
│
├── notebooks/
│   └── weather_analysis.ipynb       # Jupyter notebook
│
├── scripts/
│   ├── data_cleaning.py             # Preprocessing script
│   ├── sql_queries.sql              # All SQL queries
│   └── visualization.py            # Charts & maps
│
├── dashboard/
│   └── weather_dashboard.pbix       # Power BI file
│
├── requirements.txt
└── README.md
```

---

## 🎯 Project Outcome

- ✅ Built an **end-to-end data analysis pipeline**
- ✅ Identified **heatwave-prone regions** using real-world data
- ✅ Created an **interactive dashboard** for decision-making
- ✅ Extracted meaningful patterns across **temperature, rainfall, and humidity**

---

## 📌 Future Improvements

- [ ] Add **city-level mapping** for more granular insights
- [ ] Use **Machine Learning** for heatwave prediction (e.g., Logistic Regression, Random Forest)
- [ ] Automate the **data pipeline** using Apache Airflow or cron jobs
- [ ] Integrate **real-time weather API** for live monitoring
- [ ] Expand dataset to include more **historical years**

---

## 👩‍💻 Author

**Sangita**

> Feel free to ⭐ this repository if you found it helpful!

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
