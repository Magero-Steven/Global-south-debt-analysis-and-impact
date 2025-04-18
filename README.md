# Global-south-debt-analysis-and-impact
---
## Table of Content
- [Project overview](#project-overview)
  
- [Data Sources](#data-sources)

- [Tools](#tools)

- [Data Wrangling](#data-wrangling)

- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)

- [Data Analysis](#data-analysis)

- [Findings](#findings)

- [Recommendations](#recommendations)

- [Limitataions](#limitataions)

- [Reference](#reference)
 
## Project overview
Analyzing debt patterns, economic vulnerabilities, and policy implications in developing economies using data science.![Bar plot Comparison](https://github.com/user-attachments/assets/2fa9c97b-e229-4571-a54b-164b92d6cf2e)



### Data Sources
Debt and export data: The Primary dataset"global_south_debt.csv"  is a combination of data scrapping from the World Bank Reports and Stista

### Tools

- Excel-Data cleaning
- MySQL - Joining Tables
- JuypterNotebooks
- Tableau - Dashbords/Reports
  
### Data Wrangling

The data preparation entailed the following:
1. Data Loading and Inspection(A snippet of what the columns had)
2. Identifying/Handling missing values.
3. Dataframe creation
4. Data Cleaning and formating

### Exploratory Data Analysis EDA
EDA aimed to answer the question below;
 - Which economy had the largest Debt to Export ratio?
 - Which economy had the lowest Debt to Export ratio?
 - How has the Global South Economies' debts grown?
 - what percentage of the GDP goes to  debt repayment interest INT?

   ![Trends Over the year](https://github.com/user-attachments/assets/cab46639-f926-40b2-88e8-bc49e848a11d)


### Data Analysis
Here is a snippet of the analysis

```python

  import pandas as pd
  from io import StringIO
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import mean_squared_error, r2_score
  import matplotlib.pyplot as plt



  # Independent variables (X) and Dependent variable (y)
  X = df[['EDT/GNP', 'EDT/X', 'INT/X']]  # Features
  y = df['TDS/X']  # Target

  # Split data into training and test sets (70% training, 30% testing)
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3,       random_state=42)

  # Create linear regression model
  model = LinearRegression()

  # Fit the model with training data
  model.fit(X_train, y_train)

  # Predict on the test data
  y_pred = model.predict(X_test)

  # Evaluate the model
  mse = mean_squared_error(y_test, y_pred)  # Mean Squared Error
  r2 = r2_score(y_test, y_pred)  # R-squared

  # Print evaluation metrics
  print(f"Mean Squared Error: {mse}")
  print(f"R-squared: {r2}")

  # Coefficients and intercept
  print(f"Coefficients: {model.coef_}")
  print(f"Intercept: {model.intercept_}")

  # Plot actual vs predicted
  plt.scatter(y_test, y_pred)
  plt.xlabel("Actual TDS/X")
  plt.ylabel("Predicted TDS/X")
  plt.title("Actual vs Predicted TDS/X")
  plt.show()
```
### Findings
 Mean Squared Error (MSE): 2.27
  The model’s predictions are, on average, off by approximately √2.27 ≈ 1.51     units in TDS/X (Total Debt Service as a percentage of exports). This           indicates relatively accurate predictions given the TDS/X range of 11.2–29.1.

  R-squared (R²): 0.849
  84.9% of the variance in TDS/X is explained by the predictors (EDT/GNP,        EDT/X, and INT/X). This suggests a strong fit, though the small sample size     (9 data points) raises potential overfitting concerns.

  -EDT/GNP (External Debt to GNP Ratio): Coefficient = -0.022
  For every 1-unit increase in EDT/GNP, TDS/X decreases by 0.022 units,         holding other variables constant.

  This weak negative relationship suggests that higher debt relative to GNP     is marginally associated with lower debt service burdens, though the         effect is minimal and may not be statistically significant.

  The effect is small, indicating that debt relative to exports has limited     direct impact on debt service.

  For every 1-unit increase in INT/X, TDS/X increases by 1.255 units,           holding other variables constant.

  This is the strongest predictor, as interest payments directly contribute     to total debt service. For example, a rise in INT/X from 6.0 (1980) to        13.9 (1988) increases TDS/X by ≈9.9 units—consistent with the observed       jump from 11.2 to 29.1.

  

### Recommendations
  - Multicollinearity Risk: Variables like EDT/X and INT/X may be correlated (e.g., higher debt could lead to higher interest payments), which could inflate coefficient variances.
  - Policy Focus: Managing interest rates or renegotiating debt terms (to reduce INT/X) would most effectively lower TDS/X.

- Debt Structure: While EDT/GNP and EDT/X have minor effects, their long-term trends should still be monitored to prevent systemic risks.
### Limitataions
- Sample Size Limitation: With only 9 data points, the model risks overfitting despite the high R². Validation with more data is recommended.
- This model provides actionable insights but should be supplemented with robustness checks (e.g., p-values, multicollinearity tests) for decision-making.
- The baseline TDS/X when all predictors are zero. This has limited             practical meaning since predictors like INT/X cannot realistically be zero.
### Reference
The Growing Debt Burdens of Global South Countries[Link](https://cepr.net/publications/the-growing-debt-burdens-of-global-south-countries-standing-in-the-way-of-climate-and-development-goals/)
