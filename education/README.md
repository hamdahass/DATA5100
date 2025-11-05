# Socioeconomic Factors Affecting School Performance

> This project examines educational inequality in U.S. high schools by analyzing how socioeconomic factors influence student performance on standardized exams such as the ACT and SAT.

---

## Project Overview

Provide a short and concise overview of the project. Mention the problem it solves, the data used, and the key outcomes or findings.

- **Objective:** The point of this analysis is to explore inequality of educational opportunity in U.S. high schools by analyzing how socioeconomic factors relate to student performance on standardized exams such as the ACT and SAT. Using data from the 2016–2017 school year, drawn from the EdGap dataset and the U.S. Department of Education's Common Core of Data, the analysis combines socioeconomic and school-level variables including median household income, unemployment rate, number of teachers, and percentage of students eligible for free or reduced lunch. After cleaning the data, only 20 states remained in the final dataset, which should be considered when interpreting the results. Through regression modeling, the analysis found that the percentage of students qualifying for free or reduced lunch is the strongest predictor of average ACT scores. This variable is closely tied to each school's economic context, making it a more direct indicator of educational inequality than broader regional measures like unemployment or school size.
  
- **Domain:** U.S. Education
- **Key Techniques:** (e.g., Regression modeling, Single model inputs, Quadratic regression)

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

- **Source:** [Link to Data](https://github.com/hamdahass/DATA5100/tree/main/education/data)
- **Description:** This project uses three datasets. The first, "EdGap" (2016–2017), contains information on average ACT and SAT scores for U.S. high schools along with socioeconomic characteristics, such as median household income and unemployment rate. The second dataset, "School Information", includes identifying information for each school, such as school name, state, and academic year. It provides the context needed to align records across sources. The third dataset, "Teacher Data," comes from the Common Core of Data and includes the number of teachers per school, which was used to explore how staffing levels relate to academic performance.
- **License:** (N/A)

---

## Analysis

- The analysis was performed in a single Jupyter Notebook, which contains both code cells and Markdown cells for explanations.
- The notebook is structured so that code can be run from top to bottom to reproduce all results.
- The file that performs the data analysis can be found inside the code folder. It's called "Education.ipynb"
- The clean data file can also be found under the data folder. "education_clean.csv"

---

## Imported the needed libraries 
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

import seaborn as sns

#Set the plotting style.
sns.set_style("whitegrid")
```

## Importing Libraries for Statistical Modeling and Evaluation
```
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

import statsmodels.formula.api as smf
from sklearn.metrics import mean_squared_error
from sklearn.metrics import mean_absolute_error

from statsmodels.stats.anova import anova_lm
```

## Load all the datasets
```
edgap = pd.read_excel('/Users/hamdahassan/DATA5100/education/data/EdGap_data.xlsx', dtype={'NCESSCH School ID': object})
school_information = pd.read_csv('/Users/hamdahassan/DATA5100/education/data/ccd_sch_029_1617_w_1a_11212017.csv', encoding='unicode_escape')
teacher_data = pd.read_csv('/Users/hamdahassan/DATA5100/education/data/ccd_sch_059_1617_l_2a_11212017.csv', encoding='unicode_escape')
```

## Exploring the contents of the datasets
```
edgap.head()
school_information.head()
teacher_data.info()
```

## Data preperatin
- Select relevant subsets of the data. Get only the columns needed from the school information datatset.
- get only the Teachers, and NCESSCH from the teacher_data
- Then explore the contents to see that everything is there.
  
```
school_information = school_information[['SCHOOL_YEAR', 'NCESSCH', 'LSTATE', 'LZIP', 'SCH_TYPE_TEXT', 'LEVEL', 'CHARTER_TEXT']]
teacher_data = teacher_data[['NCESSCH', 'TEACHERS']]

```
## Renaming the data columns
```
edgap = edgap.rename(
    columns={
        "NCESSCH School ID": "id",
        "CT Pct Adults with College Degree": "percent_college",
        "CT Unemployment Rate": "rate_unemployment",
        "CT Pct Childre In Married Couple Family": "percent_married",
        "CT Median Household Income": "median_income",
        "School ACT average (or equivalent if SAT score)": "average_act",
        "School Pct Free and Reduced Lunch": "percent_lunch",
    }
)

school_information = school_information.rename(
    columns={
        "SCHOOL_YEAR": "year",
        "NCESSCH": "id",
        "LSTATE": "state",
        "LZIP": "zip_code",
        "SCH_TYPE_TEXT": "school_type",
        "LEVEL": "school_level",
        "CHARTER_TEXT": "charter"
    }
)

teacher_data = teacher_data.rename(columns={
    'NCESSCH': 'id',
    'TEACHERS': 'teachers'
})

```

## Merging dataset after the changes 

```
df = pd.merge(edgap, school_information, how='left', on='id')
df = pd.merge(df, teacher_data, how='left', on='id')

```

## Data Imputation using iterative imputer 
```
predictor_variables = [
    'rate_unemployment',
    'percent_college',
    'percent_married',
    'median_income',
    'percent_lunch',
    'state',
    'charter',
    'teachers'
]

imputer = IterativeImputer()
numerical_predictors = df[predictor_variables].select_dtypes(include='number').columns.to_list()
print(numerical_predictors)

imputer.fit(df.loc[:, numerical_predictors])
df.loc[:, numerical_predictors] = imputer.transform(df.loc[:, numerical_predictors])
```

## Export the data
```
df.to_csv('education_clean.csv', encoding='utf-8-sig', index=Fals
```

---

## Charter vs. Noncharter schools chart.
- Initially, I wanted to explore the relationship between school type (charter vs. non-charter) and average ACT scores. However, after examining the values in the "charter" column and summarizing the data, I found that the variable is highly imbalanced with far more non-charter schools than charter schools. Because of this uneven distribution, the "charter" variable is not a reliable predictor of ACT performance, as it cannot fairly represent variation across school types.

```
plt.figure(figsize=(6,6))
sns.countplot(data=df, x='charter', palette=['#4c72b0', '#dd8452'])
plt.title('Number of Charter vs. Non-Charter Schools', fontsize=16)
plt.xlabel('Charter Status', fontsize=14)
plt.ylabel('Number of Schools', fontsize=14)
plt.tick_params(labelsize=12)
plt.show()

```

## Single input model: ACT VS  Unemployment Rate (fit the model using a formula)
- The model output shows a statistically significant negative relationship between unemployment rate and ACT performance.
- The coefficient for unemployment (–19.21) indicates that as unemployment increases, ACT scores decrease.
The R-squared value (0.188) suggests that about 19% of the variation in ACT scores is explained by unemployment rate alone, indicating a moderate fit, which
means this variable is not a great predictor for ACT scores.

```
model_unemployment = smf.ols(formula='average_act ~ rate_unemployment', data=df).fit()
print(model_unemployment.summary())

```

## Single input model: ACT VS Percent Lunch 
- This model estimates the relationship between the percentage of students receiving free or reduced lunch and average ACT scores.
- The model shows a strong and statistically significant negative relationship (p < 0.001), where higher lunch participation is associated with lower ACT scores.
- The R-squared value of 0.614 indicates that this single variable explains 61% of the variation in ACT scores.

```
model_lunch = smf.ols(formula='average_act ~ percent_lunch', data=df).fit()
print(model_lunch.summary())
```

## Results

The results show that the percentage of students eligible for free or reduced lunch is the strongest predictor, explaining over 60% of the variation in ACT performance. In comparison, unemployment rate and teacher count showed much weaker relationships, explaining 19% and 3% of the variation. These findings highlight how school-level economic disadvantage is closely tied to student academic outcomes. This measure directly reflects economic disadvantage at the school level, whereas broader indicators such as unemployment rate were far less informative.


## Improvements made to the code

- Imports Cleaned: All library imports were separated onto individual lines and spacing was corrected.

- Model Evaluation Consolidated: The calculation and display of model evaluation metrics (R-squared, RMSE, and MAE) for all regression models were consolidated into single, clean code cells, replacing fragmented calculations.

- y_hat Explicitly Defined: The line to calculate predicted values (y_hat = model.predict()) was explicitly included before each metrics block to ensure calculations were accurate and to avoid errors.

- Visualization Enhanced: Visualization code was improved with explicit titles and axis labels to clearly document the regression plots.


---

## Authors

- [Hamda Hassan](https://github.com/hamdahass)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- pandas, numpy, matplotlib, seaborn
- Linear regression models, Quadratic model
- Class readings, Lectures, w3schools
- N/A
