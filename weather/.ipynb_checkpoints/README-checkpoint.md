# Weather Comparison: Seattle vs Copenhagen

> This project compares weather patterns between Seattle and Copenhagen using daily precipitation data from NOAA. Its purpose is to analyze and visualize differences between the two cities.

---

## Project Overview

The point of this project is to compare Seattle's weather to Copanhagen's. I will be using data from
[NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) to see if the two cities are similar or different. By cleaning and analyzing daily precipitation data from both cities, I examined total rainfall, average precipitation, and the number of rainy days to identify similarities and differences. Findings show that Seattle receives more total precipitation than Copenhagen. I compared one station in Seattle to one station in Copenhagen, so this data does not prove that all of Seattle rains more than all of Copenhagen, just that specific station.

- **Objective:** Compare Seattle's weather with Copenhagen's to identify similarities and differences in rainfall patterns.
- **Domain:** Environmental.
- **Key Techniques:** (Data exploration, Data ranges, Data filtering, Time Series Analysis, Line graphs)

---

## Project Structure

```
├── data/                 # Raw and processed data
├── code/                 # Jupyter notebooks and Python scripts
├── reports/              # Generated reports and visualizations
├── requirements.txt      # Dependencies
└── README.md             # Project documentation
```

---

## Data

- **Source:** [Link to Data]('DATA5100/weather/data')
- **Description:** Daily precipitation measured in Seattle and Copanhagen from January 1, 2018 to December 31, 2022. The data was retrieved from the National Centers for Environmental information [NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) tool. To find the raw datasets, you can nagivate to the data folder in the github repository. The main variables for this data are *STATION_NAME:* which describes the name of the station (city/airport name), *DATE:* the year of the record, followed by month and day, and finally the *PRCP:* which describes the precipitation (mm or inches as per preferences). The size of the Seattle dataset is (1658, 10) and Copenhagen's size is (13725, 5).
- **License:** (N/A)

---

## Analysis

- The analysis was performed in a single Jupyter Notebook, which contains both code cells and Markdown cells for explanations.
- The notebook is structured so that code can be run from top to bottom to reproduce all results.
- The file that performs the data analysis can be found inside the code folder. It's called "Weather_Data.ipynb"
- The clean data file can also be found under the data folder. "clean_seattle_copanhagen_weather.csv"

---

## Data Analysis

- **Business Understanding:** Reviewed the project requirements and defined the key questions to answer.
- **Question:** How do precipitation patterns compare between Seattle and Copenhagen from 2018 to 2022?

### Data Collection, Understanding, and Preparation
- Used Python with pandas and numpy to explore both datasets.
- Checked for missing values, duplicates, and date ranges outside 2018–2022.
- Cleaned and combined the datasets into a single dataset containing relevant information for both cities.

### Loading the Data
```python
import pandas as pd

# Load Seattle weather data
df_seattle = pd.read_csv('/Users/hamdahassan/DATA5100/weather/data/seattle_rain.csv')

# Load Copenhagen weather data
df_copanhagen = pd.read_csv('/Users/hamdahassan/DATA5100/weather/data/Copanhagen_rain.csv')


### Reviewing the Datasets

```python
# View the first few rows of the Seattle dataset
df_seattle.head()

# Check how many unique stations are in the Seattle dataset
df_seattle['STATION'].nunique()

# Check the date range in the Seattle dataset (did the same for Copenhagen as well)
df_seattle['DATE'].agg(['min', 'max'])

### Joining the Datasets

```python
# Merge Seattle and Copenhagen datasets on the DATE column
df = df_copanhagen[['DATE', 'PRCP']].merge(
    df_seattle[['DATE', 'PRCP']], on='DATE', how='outer'
)

### Data Analysis and Visualization:
- Calculated total precipitation, mean daily precipitation, and rainy days for each city.
- Created visualizations to compare precipitation patterns: line graphs for daily trends, bar charts for total precipitation and rainy days.

### Comparing Average Daily Precipitation

To compare the typical daily rainfall between Seattle and Copenhagen, I created a bar chart showing the average precipitation for each city. This visualization makes it easy to see which city generally receives more rain per day.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.barplot(data=final_df, x='city', y='precipitation', hue='city', palette=['skyblue', 'lightgreen'])
plt.xlabel("City", fontsize=18)
plt.ylabel("Precipitation (inches)", fontsize=18)
plt.title("Average Daily Precipitation by City", fontsize=16)
plt.tick_params(labelsize=15)
plt.show()

### Comparing the Number of Rainy Days

To understand how often it rains in each city, I created a bar chart showing the total number of rainy days for Seattle and Copenhagen. This helps highlight the frequency of rainfall.

```python
# Prepare the data for plotting
rainy_df = rainy_days.reset_index()
rainy_df.columns = ['City', 'Rainy_Days']

# Create the bar chart
plt.figure(figsize=(8,5))
sns.barplot(data=rainy_df, x='City', y='Rainy_Days', palette=['lightblue','lightgreen'])
plt.title("Number of Rainy Days: Seattle vs Copenhagen", fontsize=16)
plt.ylabel("Number of Rainy Days", fontsize=14)
plt.show()
---

## Results

The data analysis shows that Seattle recorded more total precipitation than Copenhagen (196.17 inches vs. 115.66 inches). Seattle also had more rainy days (1,018 vs. 777) during the period examined. This does not mean that all of Seattle receives more rain than all of Copenhagen—only that the specific Seattle station measured more rainfall than the Copenhagen station included in our analysis.
---

## Authors

- [Hamda Hassan](https://github.com/hamdahass)

---

## License

This project and its contents are intended for educational purposes only

---

## Acknowledgements

- pandas, numpy, matplotlib, seaborn
- Class readings, Lectures, w3schools
- N/A
