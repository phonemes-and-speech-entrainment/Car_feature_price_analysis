# Car Price Analysis

This project explores relationships between car prices and market, vehicle and engineering characteristics using exploratory data analysis (EDA), data cleaning, feature engineering, descriptive statistics, correlation analysis and visualisation.

The analysis considers both an **engineering perspective**, examining vehicle and engine characteristics, and a **market-pricing perspective**, investigating how manufacturer, engine size and vehicle size relate to price.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

The project uses the **Car Price Prediction** dataset from Kaggle:

[Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data)

The dataset contains **205 observations and 26 original columns**, with each row representing a car. Variables cover:

* Car identity and manufacturer
* Insurance risk
* Fuel, aspiration, body and drivetrain
* Vehicle dimensions and weight
* Engine characteristics and performance
* Fuel efficiency
* Price

The target variable for future modelling is `price`.

Three features were engineered:

* `manufacturer` — extracted from `CarName`
* `cylinder_count` — numerical cylinder count
* `footprint` — `carlength × carwidth`

Inconsistent `CarName` spellings were corrected. No missing values or duplicate rows were found.

## Business Requirements

The project adopts the perspective of a hypothetical dealership, manufacturer, pricing analyst or market research client.

The primary requirement is to:

> **Understand which market, engineering and physical vehicle characteristics are most strongly associated with car price and identify promising features for future prediction models.**

Key questions include:

* Which manufacturers have the highest prices?
* Do manufacturers differ in engineering characteristics?
* Are larger and heavier cars more expensive?
* Which numerical features are strongly correlated?
* Which variables are promising candidate predictors?

The findings can support vehicle comparisons, price segmentation and future predictive modelling.

## Hypothesis and How to Validate

The main hypothesis is:

> **Some vehicle characteristics are more useful for understanding car price than others, with manufacturer, engine size and vehicle size potentially being stronger predictors than highly specific or redundant features.**

This was investigated through:

* Dataset and data-quality checks
* Cleaning inconsistent car names
* Feature extraction and engineering
* Manufacturer-level descriptive statistics
* Engineering comparisons between manufacturers
* Pearson correlation analysis
* Bar charts, scatter plots and heatmaps
* Identification of correlated features and potential multicollinearity

The analysis found strong positive associations between price and manufacturer, engine size and several vehicle-size variables. These are **exploratory associations**, not evidence of causation or independent predictive effects.

Further validation would require predictive modelling, train/test evaluation and regression diagnostics.

## Project Plan

1. **Understand the dataset**

   * Inspect structure, variables and data types.

2. **Check data quality**

   * Check missing values, duplicates and inconsistent categories.

3. **Clean and prepare the data**

   * Correct `CarName` spelling inconsistencies.

4. **Engineer and extract features**

   * Create `manufacturer`, `cylinder_count` and `footprint`.

5. **Conduct exploratory data analysis**

   * Compare manufacturer prices and engineering characteristics.
   * Examine size, weight, engine and price relationships.
   * Explore numerical correlations.

6. **Interpret the results**

   * Identify candidate predictors and potential redundancy.

7. **Plan future modelling**

   * Use findings to inform multiple linear regression or alternative models.

The analysis was performed in a single Pandas DataFrame, with cleaning and feature engineering completed before the main exploratory analysis.

## The Rationale to Map the Business Requirements to the Data Visualisations

* **Average price by manufacturer:** examines manufacturer price positioning.
* **Average engine size versus price:** investigates engineering differences associated with market price.
* **Vehicle size, weight and price heatmap:** identifies price associations and overlapping size information.
* **Footprint versus price scatter plot:** tests the engineered size measure.
* **Numerical correlation heatmap:** identifies highly correlated potential predictors.

Together, these visualisations connect the business questions with exploratory evidence and future feature selection.

## Analysis Techniques Used

### Data inspection

Pandas methods including `info()`, `shape`, `columns`, `dtypes`, `isnull()`, `duplicated()`, `nunique()` and `unique()` were used to understand the dataset.

### Data cleaning

String replacement corrected obvious spelling inconsistencies in `CarName`. Manual inspection was used, which may not scale well to larger datasets.

### Feature engineering

* `manufacturer` was extracted from `CarName`.
* `cylinder_count` converted cylinder descriptions into numerical values.
* `footprint` combined car length and width.

### Grouped descriptive analysis

`groupby()`, `agg()`, `query()` and `sort_values()` were used to compare manufacturers by price, engine size, horsepower, weight and fuel efficiency.

### Correlation analysis

Pearson correlation was used to identify linear relationships with price and groups of correlated numerical features. Correlation does not establish causation or determine independent predictive value.

### Data visualisation

Matplotlib and Seaborn were used for:

* Bar charts
* Scatter plots
* Correlation heatmaps

### Alternative approaches

Potential future approaches include:

* Multiple linear regression
* VIF analysis
* Ridge and Lasso regression
* PCA for selected numerical features
* Mixed-data modelling approaches
* Non-linear machine-learning models

## Use of Generative AI

ChatGPT was used as an ideation and learning aid for:

* Automotive variable interpretation
* Exploratory-question development
* Feature-engineering ideas
* Pandas and analytical concepts
* Future modelling approaches

AI suggestions were reviewed and adapted to the actual dataset and analysis results.

## Unfixed Bugs

VS Code .venv issues are discussed in detail inside the notebook, in an accessible manner.

Project limitations include:

* Only 205 observations
* Small manufacturer groups
* Partly manual spelling correction
* Simplified `footprint` measure
* Correlation cannot establish independent effects
* VIF was not formally calculated
* Predictive modelling was not implemented
* Limited context about how representative the dataset is of the wider American car market

A further limitation was limited automotive domain knowledge. Variable meanings were researched, but stronger real-world conclusions would require additional domain expertise.

## Development Roadmap

1. **Complete additional data validation**

   * Standardise text and investigate small groups and extreme observations.

2. **Develop a predictive baseline**

   * Use a train/test split and training-set mean price.

3. **Build multiple linear regression models**

   * Add engineering, size and categorical features incrementally.
   * Compare models with and without manufacturer.

4. **Evaluate multicollinearity**

   * Calculate VIF and compare reduced feature sets.
   * Investigate PCA for selected numerical groups.

5. **Compare feature engineering**

   * Test `footprint` against its component variables.
   * Investigate features such as power-to-weight ratio.

6. **Evaluate predictive performance**

   * Use MAE, RMSE and R².
   * Examine residuals and regression assumptions.

7. **Develop domain knowledge**

   * Research automotive engineering, pricing, performance, brand positioning and consumer demand.

The main challenge was translating many technical automotive variables into an analytical framework suitable for both technical and business audiences.

## Main Data Analysis Libraries

### Pandas

Used for data loading, cleaning, transformation and grouped analysis.

```python
df.info()
df.isnull().sum()
df.duplicated().sum()
```

Feature extraction:

```python
df['manufacturer'] = df['CarName'].str.split().str[0]
```

Grouped analysis:

```python
manufacturer_price = (
    df.groupby('manufacturer')['price']
    .agg(['count', 'mean', 'median', 'min', 'max'])
    .sort_values('mean', ascending=False)
)
```

### NumPy

Used for numerical operations and available for future feature engineering and modelling.

### Matplotlib

Used to customise charts, including figure size, labels, titles and tick rotation.

### Seaborn

Used for statistical visualisations including bar plots, scatter plots and correlation heatmaps.

## Credits

### Content

* Dataset obtained from the [Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data).
* Project structure adapted from the Code Institute README template.
* ChatGPT supported ideation, automotive-variable interpretation, exploratory planning, Pandas guidance and code discussion.
* AI-generated suggestions were reviewed and adapted to the project.
* Official Pandas, Matplotlib and Seaborn documentation should be referenced for directly adapted implementation details.

### Media

No external photographs or media were used.

The Code Institute logo is provided through the resource included in the project template.

## Acknowledgements

Thanks to Code Institute for the project template and learning framework.

Thanks to the Kaggle dataset contributor for making the dataset available.

Thanks to ChatGPT for assistance with ideation, data-analysis concepts, automotive feature interpretation and code explanations.
