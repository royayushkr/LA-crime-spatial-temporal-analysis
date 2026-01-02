# Los Angeles Crime Data: Spatial & Temporal Pattern Analysis

## 📌 Project Overview
This project supports the Los Angeles Police Department (LAPD) by analyzing a dataset of reported crimes to identify actionable patterns in criminal behavior. By leveraging data manipulation techniques, the analysis determines how resources might be allocated effectively by pinpointing peak crime hours, identifying high-risk locations for night crimes, and categorizing victim demographics.

## 🚀 Key Business Questions
* **Temporal Analysis:** At what time of day do crimes occur most frequently?
* **Spatial Analysis:** Which geographic area requires the most vigilance during "night hours" (10 PM – 3:59 AM)?
* **Demographic Analysis:** Which age groups are most frequently targeted as victims?

## 🛠️ Technical Stack
* **Language:** Python 3.x
* **Libraries:**
    * **Pandas:** Data cleaning, string manipulation, time-series extraction, and binning.
    * **Matplotlib/Seaborn:** Visualization libraries (imported for potential plotting).
* **Data Source:** Modified subset of Los Angeles Open Data (`crimes.csv`) containing records such as Date Reported, Time Occurred, Area Name, and Victim Age.

## 📊 Methodology & Insights

### 1. Temporal Analysis: Peak Crime Hour
* **Method:** Extracted the first two digits from the military time column (`TIME OCC`) to create an integer-based `HOUR` feature.
* **Key Finding:** The frequency of crimes peaks at **12:00 (Noon)**, with **13,663** reported incidents.

### 2. Spatial Analysis: Night Crime Hotspots
* **Method:** "Night" was defined as the hours between 10:00 PM and 3:59 AM. The analysis filtered the dataset for these specific hours and grouped results by `AREA NAME`.
* **Key Finding:** The **Central** area has the largest frequency of night crimes, making it a critical focus area for nocturnal patrol resource allocation.

### 3. Victim Demographics: Age Binning
* **Method:** Victim ages were categorized into distinct bins (`0-17`, `18-25`, `26-34`, `35-44`, `45-54`, `55-64`, `65+`) using `pd.cut` to analyze distribution patterns.
* **Key Finding:** The **26-34** age group is the most frequently victimized (47,470 counts), followed closely by the **35-44** age group (42,157 counts).

## 💻 Code Highlight: Custom Filtering & Binning
The project utilized Pandas for efficient logical filtering and categorical binning to derive insights.

```python
# Filtering for specific "Night" hours (10 PM - 3:59 AM)
night_crimes = crimes[crimes['HOUR'].isin([22, 23, 0, 1, 2, 3])]
peak_night_crime_location = night_crimes['AREA NAME'].value_counts().idxmax()

# Binning victim ages into demographically relevant categories
bins = [0, 17, 25, 34, 44, 54, 64, float('inf')]
labels = ['0-17', '18-25', '26-34', '35-44', '45-54', '55-64', '65+']
victim_ages = pd.cut(crimes['Vict Age'], bins=bins, labels=labels, right=True).value_counts()
