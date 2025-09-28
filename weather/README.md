# Weather Comparison: Seattle vs Copanhagen

> A brief description of what the project does and its purpose.

---

## Project Overview

The point of this project is to to compate Seattle's weather to Copanhagen's. I will be using data from
[NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) to see if the two cities are similar or different. 

- **Objective:** Compare Seattle's weather with Copenhagen's to identify similarities and differences in rainfall and temperature patterns.
- **Domain:** Environmental.
- **Key Techniques:** (e.g., Regression, Classification, Clustering, NLP, Time Series)

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

- **Source:** https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
- **Description:** Daily precipitation measured in Seattle and Copanhagen from January 1, 2018 to December 31, 2022. The data was retrieved from the National Centers for Environmental information [NOAA](https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND) tool. To find the raw datasets, you can nagivate to the data folder in the github repository. The main variables for this data are *STATION_NAME:* which descripes the name of the station (city/airport name), *DATE:* the year of the record, followed by month and day, and finally the *PRCP:* which describes the precipitation (mm or inches as per preferences)
- **License:** (if applicable)

---

## Analysis

Describe the notebooks and/or scripts used to perform the analysis. Specify the order in which the code should be run to reproduce the results.

---

## Results

Include a short discussion of the findings and what they imply.

---

## Authors

- Your Name - [Hamda Hassan](https://github.com/yourhandle)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Tools/libraries used
- Tutorials or papers referenced
- Inspiration or collaborators
