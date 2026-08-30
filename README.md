# 🚌 Pune Traffic Analysis Dashboard

An interactive **Pune Traffic Analysis Dashboard** built using **Python and Microsoft Power BI** to analyze public transportation routes, traffic delays, passenger demand, speed, occupancy, weather conditions, risk levels, fuel consumption, and complaints.

This project demonstrates an end-to-end **Data Analyst workflow**, including data cleaning, Exploratory Data Analysis (EDA), visualization, Power Query, DAX, KPI development, and interactive Power BI dashboard creation.

---

# 📌 Project Overview

The project analyzes Pune traffic and bus-route data to understand transportation performance and identify important traffic patterns.

The analysis focuses on:

* 🚌 Route performance
* ⏱️ Travel delays
* 👥 Passenger demand
* 🚦 Traffic signals
* 🛣️ Route distance
* 🏎️ Average speed
* 🌦️ Weather conditions
* ⚠️ Risk levels
* 🕐 Peak-hour traffic
* 🎫 Ticket revenue
* 🚌 Bus occupancy
* 👨‍✈️ Driver experience
* ⛽ Fuel consumption
* 🛑 Skipped stops
* 📢 Passenger complaints

---

# 🎯 Project Objectives

* Clean and prepare traffic data.
* Perform Exploratory Data Analysis using Python.
* Identify traffic delay patterns.
* Analyze passenger demand.
* Analyze route performance.
* Compare scheduled and actual travel time.
* Study the relationship between distance and delay.
* Analyze weather and traffic conditions.
* Identify high-risk routes.
* Analyze bus occupancy.
* Analyze fuel consumption.
* Create meaningful KPIs.
* Build an interactive Power BI dashboard.
* Generate actionable transportation insights.

---

# 📂 Dataset

### Dataset Name

```text
Pune_Traffic_Dataset.csv
```

### Dataset Columns

```text
route_id
route_name
start_stop
end_stop
distance_km
scheduled_time_min
actual_time_min
avg_speed_kmph
day_of_week
time_of_day
passenger_count
weather
traffic_signal_count
stop_count
speed_reduction_index
risk_level
peak_hour_flag
ticket_price_inr
occupancy_percent
bus_type
driver_experience_years
num_stops_skipped
fuel_consumption_liters
complaint_count
delay_min
```

---

# 🔍 1. Exploratory Data Analysis (EDA)

EDA was performed using **Python, Pandas, NumPy, Matplotlib, and Seaborn** before developing the Power BI dashboard.

The purpose of EDA was to understand the dataset, identify patterns, detect outliers, and determine the most useful KPIs and visualizations.

---

## 🛠️ EDA Tools

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook

---

# 🧹 Data Cleaning

The following data-cleaning steps were performed:

1. Imported the CSV dataset.
2. Checked dataset dimensions.
3. Checked column names.
4. Checked data types.
5. Checked missing values.
6. Checked duplicate records.
7. Generated statistical summaries.
8. Checked unique categorical values.
9. Identified invalid numerical values.
10. Checked outliers.
11. Standardized categorical values.
12. Validated route and traffic measurements.
13. Prepared the cleaned dataset for Power BI.

### Python Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("Pune_Traffic_Dataset.csv")

print("Dataset Shape:", df.shape)

display(df.head())

df.info()

print("\nMissing Values:")
print(df.isnull().sum())

print("\nDuplicate Rows:")
print(df.duplicated().sum())

display(df.describe())
```

---

# 📊 EDA Analysis

## 1. Route Analysis

Analyzed:

* Total number of routes
* Route frequency
* Route distance
* Start stops
* End stops
* Scheduled travel time
* Actual travel time

```python
plt.figure(figsize=(10, 6))

sns.countplot(
    y="route_name",
    data=df,
    order=df["route_name"].value_counts().index
)

plt.title("Route Distribution")
plt.xlabel("Number of Records")
plt.ylabel("Route")

plt.show()
```

---

# ⏱️ 2. Delay Analysis

Analyzed traffic delays across routes and travel conditions.

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["delay_min"],
    bins=30,
    kde=True
)

plt.title("Traffic Delay Distribution")
plt.xlabel("Delay (Minutes)")
plt.ylabel("Frequency")

plt.show()
```

### Average Delay by Route

```python
plt.figure(figsize=(10, 6))

df.groupby("route_name")["delay_min"].mean().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Average Delay by Route")
plt.xlabel("Route")
plt.ylabel("Average Delay (Minutes)")

plt.xticks(rotation=45)

plt.show()
```

---

# 🛣️ 3. Distance Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["distance_km"],
    bins=30,
    kde=True
)

plt.title("Route Distance Distribution")
plt.xlabel("Distance (KM)")
plt.ylabel("Frequency")

plt.show()
```

---

# 🏎️ 4. Average Speed Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["avg_speed_kmph"],
    bins=30,
    kde=True
)

plt.title("Average Speed Distribution")
plt.xlabel("Average Speed (KM/H)")
plt.ylabel("Frequency")

plt.show()
```

### Speed by Route

```python
plt.figure(figsize=(10, 6))

df.groupby("route_name")["avg_speed_kmph"].mean().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Average Speed by Route")
plt.xlabel("Route")
plt.ylabel("Average Speed (KM/H)")

plt.xticks(rotation=45)

plt.show()
```

---

# 👥 5. Passenger Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["passenger_count"],
    bins=30,
    kde=True
)

plt.title("Passenger Count Distribution")
plt.xlabel("Passenger Count")
plt.ylabel("Frequency")

plt.show()
```

### Passenger Count by Route

```python
plt.figure(figsize=(10, 6))

df.groupby("route_name")["passenger_count"].sum().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Passenger Demand by Route")
plt.xlabel("Route")
plt.ylabel("Total Passengers")

plt.xticks(rotation=45)

plt.show()
```

---

# 🚌 6. Bus Occupancy Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["occupancy_percent"],
    bins=30,
    kde=True
)

plt.title("Bus Occupancy Distribution")
plt.xlabel("Occupancy (%)")
plt.ylabel("Frequency")

plt.show()
```

### Occupancy by Bus Type

```python
plt.figure(figsize=(8, 5))

df.groupby("bus_type")["occupancy_percent"].mean().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Average Occupancy by Bus Type")
plt.xlabel("Bus Type")
plt.ylabel("Average Occupancy (%)")

plt.show()
```

---

# 🌦️ 7. Weather Analysis

```python
plt.figure(figsize=(8, 5))

sns.countplot(
    x="weather",
    data=df
)

plt.title("Traffic Records by Weather")
plt.xlabel("Weather")
plt.ylabel("Count")

plt.xticks(rotation=45)

plt.show()
```

### Weather vs Delay

```python
plt.figure(figsize=(8, 5))

df.groupby("weather")["delay_min"].mean().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Average Delay by Weather")
plt.xlabel("Weather")
plt.ylabel("Average Delay (Minutes)")

plt.show()
```

---

# ⚠️ 8. Risk Level Analysis

```python
plt.figure(figsize=(8, 5))

df["risk_level"].value_counts().plot(kind="bar")

plt.title("Traffic Risk Level Distribution")
plt.xlabel("Risk Level")
plt.ylabel("Number of Records")

plt.show()
```

### Risk Level by Route

```python
pd.crosstab(
    df["route_name"],
    df["risk_level"]
).plot(
    kind="bar",
    figsize=(12, 6)
)

plt.title("Risk Level by Route")
plt.xlabel("Route")
plt.ylabel("Count")

plt.xticks(rotation=45)

plt.show()
```

---

# 🕐 9. Peak Hour Analysis

```python
plt.figure(figsize=(8, 5))

df["peak_hour_flag"].value_counts().plot(kind="bar")

plt.title("Peak Hour Distribution")
plt.xlabel("Peak Hour")
plt.ylabel("Number of Records")

plt.show()
```

### Peak Hour vs Delay

```python
plt.figure(figsize=(8, 5))

df.groupby("peak_hour_flag")["delay_min"].mean().plot(
    kind="bar"
)

plt.title("Average Delay: Peak vs Non-Peak")
plt.xlabel("Peak Hour Flag")
plt.ylabel("Average Delay (Minutes)")

plt.show()
```

---

# 📅 10. Day of Week Analysis

```python
plt.figure(figsize=(10, 5))

df["day_of_week"].value_counts().plot(
    kind="bar"
)

plt.title("Traffic Records by Day of Week")
plt.xlabel("Day")
plt.ylabel("Count")

plt.show()
```

---

# 🕒 11. Time of Day Analysis

```python
plt.figure(figsize=(8, 5))

df["time_of_day"].value_counts().plot(
    kind="bar"
)

plt.title("Traffic by Time of Day")
plt.xlabel("Time of Day")
plt.ylabel("Count")

plt.show()
```

---

# 🚦 12. Traffic Signal Analysis

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="traffic_signal_count",
    y="delay_min"
)

plt.title("Traffic Signals vs Delay")
plt.xlabel("Traffic Signal Count")
plt.ylabel("Delay (Minutes)")

plt.show()
```

---

# 🛑 13. Stop Analysis

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="stop_count",
    y="actual_time_min"
)

plt.title("Number of Stops vs Actual Travel Time")
plt.xlabel("Stop Count")
plt.ylabel("Actual Travel Time (Minutes)")

plt.show()
```

---

# ⛽ 14. Fuel Consumption Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["fuel_consumption_liters"],
    bins=30,
    kde=True
)

plt.title("Fuel Consumption Distribution")
plt.xlabel("Fuel Consumption (Liters)")
plt.ylabel("Frequency")

plt.show()
```

### Distance vs Fuel Consumption

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="distance_km",
    y="fuel_consumption_liters"
)

plt.title("Distance vs Fuel Consumption")
plt.xlabel("Distance (KM)")
plt.ylabel("Fuel Consumption (Liters)")

plt.show()
```

---

# 📢 15. Complaint Analysis

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    df["complaint_count"],
    bins=30,
    kde=True
)

plt.title("Complaint Distribution")
plt.xlabel("Complaint Count")
plt.ylabel("Frequency")

plt.show()
```

### Complaints by Route

```python
plt.figure(figsize=(10, 6))

df.groupby("route_name")["complaint_count"].sum().sort_values(
    ascending=False
).plot(kind="bar")

plt.title("Complaints by Route")
plt.xlabel("Route")
plt.ylabel("Total Complaints")

plt.xticks(rotation=45)

plt.show()
```

---

# 🔗 16. Correlation Analysis

```python
plt.figure(figsize=(14, 10))

corr = df.select_dtypes(
    include="number"
).corr()

sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm",
    fmt=".2f"
)

plt.title("Pune Traffic Correlation Heatmap")

plt.show()
```

---

# 📈 17. Important Relationships

### Distance vs Delay

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="distance_km",
    y="delay_min"
)

plt.title("Distance vs Delay")
plt.xlabel("Distance (KM)")
plt.ylabel("Delay (Minutes)")

plt.show()
```

### Passenger Count vs Occupancy

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="passenger_count",
    y="occupancy_percent"
)

plt.title("Passenger Count vs Occupancy")
plt.xlabel("Passenger Count")
plt.ylabel("Occupancy (%)")

plt.show()
```

### Speed Reduction vs Delay

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="speed_reduction_index",
    y="delay_min"
)

plt.title("Speed Reduction Index vs Delay")
plt.xlabel("Speed Reduction Index")
plt.ylabel("Delay (Minutes)")

plt.show()
```

---

# 📊 18. Outlier Analysis

```python
numeric_columns = df.select_dtypes(
    include="number"
).columns

for col in numeric_columns:

    plt.figure(figsize=(8, 4))

    sns.boxplot(
        y=df[col]
    )

    plt.title(f"Outlier Analysis - {col}")

    plt.show()
```

---

# 🧮 Outlier Detection Using IQR

```python
num_cols = df.select_dtypes(
    include="number"
).columns

for col in num_cols:

    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[
        (df[col] < lower) |
        (df[col] > upper)
    ]

    print(col, ":", len(outliers))
```

---

# 💡 EDA Key Findings

The EDA helps identify:

* Routes with the highest passenger demand.
* Routes experiencing the highest delays.
* Routes with lower average speeds.
* Peak-hour traffic patterns.
* Weather conditions associated with delays.
* High-risk traffic routes.
* Bus types with high occupancy.
* Routes with higher fuel consumption.
* Routes generating more complaints.
* Relationships between distance and delay.
* Relationships between distance and fuel consumption.
* Relationships between passenger demand and occupancy.

---

# 📊 2. Power BI Dashboard

After completing Python EDA, the cleaned dataset was imported into **Microsoft Power BI**.

The dashboard converts the EDA findings into an interactive business intelligence report.

---

## 🛠️ Power BI Tools

* Microsoft Power BI
* Power Query
* DAX
* Data Modeling
* KPI Cards
* Bar Charts
* Column Charts
* Line Charts
* Donut Charts
* Map Visuals
* Slicers
* Tooltips
* Conditional Formatting

---

# 📌 Dashboard KPIs

Recommended KPI cards:

### 🚌 Total Routes

```DAX
Total Routes =
DISTINCTCOUNT(Traffic[route_id])
```

### 👥 Total Passengers

```DAX
Total Passengers =
SUM(Traffic[passenger_count])
```

### ⏱️ Average Delay

```DAX
Average Delay =
AVERAGE(Traffic[delay_min])
```

### 🏎️ Average Speed

```DAX
Average Speed =
AVERAGE(Traffic[avg_speed_kmph])
```

### 🚌 Average Occupancy

```DAX
Average Occupancy =
AVERAGE(Traffic[occupancy_percent])
```

### ⛽ Total Fuel Consumption

```DAX
Total Fuel =
SUM(Traffic[fuel_consumption_liters])
```

### 📢 Total Complaints

```DAX
Total Complaints =
SUM(Traffic[complaint_count])
```

### 🛑 Stops Skipped

```DAX
Total Stops Skipped =
SUM(Traffic[num_stops_skipped])
```

### ⚠️ High-Risk Records

```DAX
High Risk Records =
CALCULATE(
    COUNTROWS(Traffic),
    Traffic[risk_level] = "High"
)
```

---

# 💰 Ticket Revenue

```DAX
Total Ticket Revenue =
SUMX(
    Traffic,
    Traffic[passenger_count] *
    Traffic[ticket_price_inr]
)
```

---

# ⏰ Scheduled vs Actual Time

```DAX
Average Scheduled Time =
AVERAGE(Traffic[scheduled_time_min])
```

```DAX
Average Actual Time =
AVERAGE(Traffic[actual_time_min])
```

---

# 📈 Dashboard Visualizations

## 🚌 Route Performance

* Passenger Count by Route
* Average Delay by Route
* Average Speed by Route
* Distance by Route

## ⏱️ Delay Analysis

* Delay by Route
* Delay by Day
* Delay by Time of Day
* Delay by Weather
* Peak vs Non-Peak Delay

## 👥 Passenger Analysis

* Passenger Count by Route
* Passenger Count by Day
* Passenger Count by Time of Day
* Occupancy by Bus Type

## 🌦️ Weather Analysis

* Traffic Records by Weather
* Average Delay by Weather
* Risk Level by Weather

## ⚠️ Risk Analysis

* Risk Level Distribution
* High-Risk Routes
* Risk by Time of Day
* Risk by Weather

## ⛽ Fuel Analysis

* Fuel Consumption by Route
* Fuel Consumption by Bus Type
* Distance vs Fuel Consumption

## 📢 Complaint Analysis

* Complaints by Route
* Complaints by Risk Level
* Complaints by Delay

---

# 🎛️ Dashboard Slicers

Recommended slicers:

```text
Route Name
Start Stop
End Stop
Day of Week
Time of Day
Weather
Risk Level
Peak Hour Flag
Bus Type
```

These filters allow users to dynamically explore the traffic data.

---

# 🗺️ Map Analysis

A map visual can be created using:

```text
Start Stop
End Stop
Route Name
Passenger Count
Average Delay
```

If latitude and longitude are added to the dataset later, the dashboard can provide more accurate geographic route analysis.

---

# 🎨 Recommended Dashboard Layout

```text
┌─────────────────────────────────────────────────────────────┐
│              🚌 PUNE TRAFFIC ANALYTICS                     │
├────────────┬────────────┬────────────┬────────────┬────────┤
│ Total      │ Passengers │ Avg Delay  │ Avg Speed  │ Risk   │
│ Routes     │            │            │            │ Routes │
├────────────┴────────────┴────────────┴────────────┴────────┤
│                                                             │
│  Passenger Count by Route       Average Delay by Route     │
│                                                             │
├──────────────────────────────┬──────────────────────────────┤
│ Delay by Weather              │ Risk Level Distribution    │
│                              │                              │
├──────────────────────────────┼──────────────────────────────┤
│ Fuel Consumption by Route     │ Occupancy by Bus Type      │
│                              │                              │
├──────────────────────────────┴──────────────────────────────┤
│                    Interactive Map                           │
└─────────────────────────────────────────────────────────────┘
```

---

# 📸 EDA Preview

Add your Python EDA screenshots inside the `Images` folder.

markdown
<img width="1077" height="1306" alt="image" src="https://github.com/user-attachments/assets/1d0dc3e0-aac0-4090-9f09-3adc5f5d6730" />

<img width="884" height="580" alt="image" src="https://github.com/user-attachments/assets/98685d5c-afc5-4bca-8158-444532d63f03" />
<img width="919" height="580" alt="image" src="https://github.com/user-attachments/assets/e092b411-4d8a-4289-849b-e4011c7c313d" />
<img width="1080" height="700" alt="image" src="https://github.com/user-attachments/assets/094f972b-f924-4b42-8919-c02350c030c9" />
<img width="665" height="633" alt="image" src="https://github.com/user-attachments/assets/ea4ff10d-d4df-4543-a5a5-3ba6369e565b" />
<img width="639" height="608" alt="image" src="https://github.com/user-attachments/assets/b8b42aa8-786b-49c1-990c-116bf1e2d3b4" />
<img width="639" height="608" alt="image" src="https://github.com/user-attachments/assets/104d2436-a0f4-40a5-a800-5d194ba865fe" />
<img width="639" height="608" alt="image" src="https://github.com/user-attachments/assets/301743ed-8987-4174-9a04-660aad6b2c0a" />
<img width="648" height="608" alt="image" src="https://github.com/user-attachments/assets/cfa36176-5740-4bd9-bc24-50cb34f752e5" />










# 📸 Power BI Dashboard Preview

Add your Power BI dashboard screenshot:

---markdown
<img width="1009" height="747" alt="Screenshot 2026-08-11 095611" src="https://github.com/user-attachments/assets/715e6fbd-05e3-4c92-952f-d9f2f51b58fa" />


---

# 🚀 Project Workflow

```text
Raw CSV Dataset
       ↓
Data Cleaning
       ↓
Python EDA
       ↓
EDA Visualizations
       ↓
Outlier Analysis
       ↓
Business Insights
       ↓
Power Query
       ↓
Data Modeling
       ↓
DAX Measures
       ↓
KPI Cards
       ↓
Power BI Visualizations
       ↓
Interactive Slicers
       ↓
Pune Traffic Dashboard
```

---

# 📁 Repository Structure

```text
Pune-Traffic-Analysis/
│
├── Dataset/
│   └── Pune_Traffic_Dataset.csv
│
├── EDA/
│   └── Pune_Traffic_EDA.ipynb
│
├── Dashboard/
│   └── Pune_Traffic_Dashboard.pbix
│
├── Images/
│   ├── EDA_Route_Distribution.png
│   ├── EDA_Delay_Analysis.png
│   ├── EDA_Passenger_Analysis.png
│   ├── EDA_Speed_Analysis.png
│   ├── EDA_Weather_Analysis.png
│   ├── EDA_Risk_Analysis.png
│   ├── EDA_Fuel_Analysis.png
│   ├── EDA_Complaint_Analysis.png
│   ├── EDA_Correlation_Heatmap.png
│   └── Pune_Traffic_Dashboard.png
│
├── README.md
└── LICENSE
```

---

# 💡 Key Insights

* Identified high-delay routes.
* Analyzed passenger demand across routes.
* Compared scheduled and actual travel time.
* Analyzed peak-hour traffic.
* Studied weather-related traffic delays.
* Identified high-risk traffic conditions.
* Compared occupancy across bus types.
* Analyzed fuel consumption.
* Identified routes with higher complaint counts.
* Studied the relationship between route distance and delay.
* Studied the relationship between traffic signals and delay.
* Analyzed the impact of speed reduction on travel delay.

---

# 📚 Skills Demonstrated

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Exploratory Data Analysis
* Data Cleaning
* Data Transformation
* Power Query
* Power BI
* DAX
* Data Modeling
* KPI Development
* Dashboard Design
* Data Visualization
* Business Intelligence
* Traffic Analytics
* Data Storytelling

---

# 🧠 Key Learnings

* Learned how to perform complete EDA on transportation data.
* Learned how to identify traffic patterns using Python.
* Improved data-cleaning and transformation skills.
* Learned how to identify outliers using IQR.
* Created meaningful transportation KPIs.
* Learned how to create DAX measures.
* Built an interactive Power BI dashboard.
* Improved dashboard design and data storytelling.
* Learned how to convert raw traffic data into business insights.

---

# ✅ Advantages

* Provides a centralized view of Pune traffic performance.
* Helps identify routes with high delays.
* Tracks passenger demand.
* Monitors average speed.
* Analyzes bus occupancy.
* Identifies high-risk routes.
* Analyzes weather-related traffic patterns.
* Tracks fuel consumption.
* Monitors passenger complaints.
* Provides interactive filters.
* Reduces manual reporting.
* Helps transportation teams identify operational issues.
* Supports data-driven decision-making.
* Demonstrates practical Python and Power BI skills.
* Suitable for Data Analyst portfolios and resumes.

---

# ❌ Disadvantages

* The analysis depends on the quality of the source dataset.
* Historical data may not represent current traffic conditions.
* The project does not provide live GPS tracking.
* Real-time traffic incidents are not included.
* The dashboard cannot predict future traffic conditions.
* Manual refresh may be required when new data is added.
* Large datasets may affect Power BI performance.
* Geographic analysis is limited without latitude and longitude.
* External factors such as road construction may not be captured.
* Advanced machine-learning prediction is not included.

---

# 🎁 Benefits

* Helps understand Pune transportation performance.
* Supports route performance analysis.
* Helps identify traffic delay patterns.
* Supports passenger demand analysis.
* Helps monitor peak-hour congestion.
* Supports fuel-efficiency analysis.
* Helps identify high-risk routes.
* Provides quick KPI monitoring.
* Makes complex traffic data easier to understand.
* Saves time in reporting.
* Improves data-driven decision-making.
* Provides an interactive business intelligence solution.

---

# ⚠️ Limitations

* Does not provide real-time traffic information.
* Does not provide live bus GPS tracking.
* Does not predict future traffic conditions.
* Dataset accuracy directly affects the analysis.
* Exact geographic analysis requires latitude and longitude.
* Does not include all possible traffic factors.
* Does not include live accident information.
* Does not include road-construction data.
* Manual data refresh may be required.
* Advanced predictive analytics is outside the current project scope.

---

# 📌 Scope

The scope of this project includes:

* Route analysis
* Passenger analysis
* Delay analysis
* Speed analysis
* Occupancy analysis
* Weather analysis
* Risk analysis
* Peak-hour analysis
* Fuel analysis
* Complaint analysis
* Traffic signal analysis
* Interactive Power BI reporting

The project can be extended with real-time traffic APIs, GPS tracking, machine-learning prediction, route optimization, and automated dashboard refresh.

---

# 🚀 Future Enhancements

* Add real-time traffic APIs.
* Add GPS-based bus tracking.
* Add latitude and longitude.
* Add live congestion monitoring.
* Add machine-learning traffic prediction.
* Add delay forecasting.
* Add route optimization.
* Add accident analysis.
* Add passenger demand forecasting.
* Add fuel-efficiency prediction.
* Add automated Power BI refresh.
* Add real-time traffic alerts.

---

# 🏢 Business Use Cases

This project can be useful for:

* 🚌 Public Transportation Departments
* 🚦 Traffic Management Teams
* 🏙️ Smart City Projects
* 📊 Data Analysts
* 🚌 Bus Operators
* 🏢 Transportation Companies
* 🏛️ Government Departments
* 📈 Business Intelligence Teams

---

# 👨‍💻 Author

**Dashrath Landge**

**Aspiring Data Analyst**

### Technical Skills

* Python
* SQL
* Power BI
* Excel
* Pandas
* NumPy
* Matplotlib
* Seaborn
* DAX
* Power Query
* Data Analytics
* Data Visualization

---

# ⭐ Project

If you find this project useful, please consider giving the repository a ⭐ **Star**.

Thank you for visiting my **Pune Traffic Analysis Dashboard**!
