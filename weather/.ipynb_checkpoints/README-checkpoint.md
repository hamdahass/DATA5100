# Weather Comparison: Seattle vs Copenhagen

> This project compares weather patterns between Seattle and Copenhagen using daily precipitation data from NOAA. Its purpose is to analyze and visualize differences between the two cities.

---

## Project Overview

The point of this project is to compate Seattle's weather to Copanhagen's. I will be using data from
[NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) to see if the two cities are similar or different. By cleaning and analyzing daily precipitation data from both cities, I examined total rainfall, average precipitation, and the number of rainy days to identify similarities and differences. Findings show that Seattle receives more total precipitation than Copenhagen. I compared one station in Seattle to one station in Copenhagen, so this data is not prove that all of Seattle rains more than all of Copenhagen, just that specific station.

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
- **Description:** Daily precipitation measured in Seattle and Copanhagen from January 1, 2018 to December 31, 2022. The data was retrieved from the National Centers for Environmental information [NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) tool. To find the raw datasets, you can nagivate to the data folder in the github repository. The main variables for this data are *STATION_NAME:* which descripes the name of the station (city/airport name), *DATE:* the year of the record, followed by month and day, and finally the *PRCP:* which describes the precipitation (mm or inches as per preferences). The size of the Seattle dataset is (1658, 10) and Copenhagen's size is (13725, 5).
- **License:** (N/A)

---

## Analysis

- The analysis was performed in a single Jupyter Notebook, which contains both code cells and Markdown cells for explanations.
- The notebook is structured so that code can be run from top to bottom to reproduce all results.

---

## Results

The data analysis shows that the Seattle recorded more total precipitation than the Copenhagen (393 inches vs. 302 inches). Seattle also had more rainy days (2507 vs 2285) during the period examined. This doesn't mean Seattle gets more rain than all of Copenhagen, only that the specific Seattle station measured more rainfall than the Copenhagen station we analyzed.

---

## Authors

- [Hamda Hassan](https://github.com/hamdahass)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- pandas, numpy, matplotlib, seaborn
- Class readings, Lectures, w3schools
- N/A
