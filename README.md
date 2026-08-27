# Car Price Analysis

This project explores relationships between car prices and market, vehicle and engineering characteristics. It uses exploratory data analysis (EDA), data cleaning, feature extraction, grouped descriptive statistics, correlation analysis and visualisation to identify characteristics that may be useful for understanding and eventually predicting car prices.

The project considers both an **engineering perspective**, examining vehicle and engine characteristics, and a **market-pricing perspective**, investigating how manufacturer, engine size and vehicle size relate to price.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

The dataset used is the **Car Price Prediction** dataset from Kaggle:

[Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data)

It contains **205 observations and 26 original columns**, with each row representing a car. Variables include:

* Car identifier and name
* Insurance risk
* Fuel and aspiration type
* Body and drivetrain configuration
* Vehicle dimensions and weight
* Engine design and size
* Internal engine measurements
* Engine performance
* Fuel efficiency
* Car price

The target variable for potential predictive modelling is `price`.

Three additional features were created:

* `manufacturer`, extracted from `CarName`
* `cylinder_count`, converting categorical cylinder descriptions into numerical values
* `footprint`, calculated by multiplying car length by car width as a simple measure of vehicle size

Several inconsistent spellings in `CarName` were corrected. No missing values or duplicate rows were identified.

## Business Requirements

The project takes the perspective of a hypothetical automotive pricing client, such as a dealership, manufacturer, pricing analyst or market research partner.

The primary requirement is to:

> **Understand which market, engineering and physical vehicle characteristics are most strongly associated with car price and identify promising features for future car price prediction models.**

The analysis investigates:

* Which manufacturers have the highest average prices?
* Do higher-priced manufacturers tend to have different engineering characteristics?
* Are larger and heavier vehicles associated with higher prices?
* Which numerical features are strongly correlated and potentially redundant?
* Which variables should be investigated as candidate predictors in a future regression or machine-learning model?

For a pricing client, these findings can support comparisons between vehicles and identify characteristics associated with different price segments. For engineering or product-development audiences, they illustrate relationships between physical size, engine characteristics and performance.

## Hypothesis and How to Validate

The main hypothesis is:

> **Some vehicle characteristics provide more useful information about car price than others, with market characteristics such as manufacturer and broad engineering characteristics such as engine size and vehicle size potentially being stronger candidate predictors than highly specific or redundant features.**

This was investigated as an exploratory hypothesis rather than an established conclusion.

Validation involved:

* Inspecting dataset structure and data types
* Checking missing and duplicated values
* Correcting inconsistent car-name spellings
* Extracting manufacturer
* Converting cylinder number to a numerical feature
* Comparing manufacturer-level price statistics
* Comparing manufacturer engineering characteristics
* Calculating numerical correlations
* Using bar charts, scatter plots and heatmaps
* Identifying highly correlated feature groups and potential multicollinearity

The analysis found strong positive associations between price and manufacturer, engine size and several vehicle-size variables. These are **exploratory associations within this dataset**, not evidence of independent causal effects.

Further validation would require train/test evaluation, multiple linear regression diagnostics and formal multicollinearity assessment.

## Project Plan

The project followed this process:

1. **Understand the dataset**

   * Inspect structure, shape, columns and data types.
   * Establish the broad meaning and category of each variable.

2. **Check data quality**

   * Check missing values and duplicates.
   * Inspect unique values for inconsistent labels and spelling errors.

3. **Clean and prepare the data**

   * Correct obvious `CarName` inconsistencies.
   * Retain original variables while creating additional features where useful.

4. **Engineer and extract features**

   * Extract `manufacturer` from `CarName`.
   * Create numerical `cylinder_count`.
   * Create `footprint` from car length and width.

5. **Conduct exploratory data analysis**

   * Compare manufacturer price distributions and statistics.
   * Investigate engine size and performance differences between manufacturers.
   * Examine vehicle size, weight and price relationships.
   * Explore numerical feature correlations.

6. **Interpret the results**

   * Identify promising candidate predictors.
   * Consider multicollinearity and redundant information.
   * Identify areas requiring further automotive domain knowledge.

7. **Plan future modelling**

   * Use exploratory findings to inform feature selection and future multiple linear regression or alternative predictive models.

All analysis was performed using a single Pandas DataFrame. Cleaning and feature engineering were completed before the main exploratory analyses so that grouping and visualisation used consistent categories.

Exploratory and descriptive methods were chosen to understand the dataset before making predictive modelling assumptions.

## The Rationale to Map the Business Requirements to the Data Visualisations

The visualisations were selected to address specific business and analytical questions:

* **Average price by manufacturer:** identifies broad differences in manufacturer price positioning.
* **Manufacturer average engine size versus average price:** investigates whether market-price differences may be associated with engineering characteristics.
* **Vehicle size, weight and price correlation heatmap:** identifies characteristics associated with price and potentially overlapping information.
* **Vehicle footprint versus price scatter plot:** examines whether the engineered footprint measure is associated with price.
* **Numerical feature correlation heatmap:** identifies highly correlated feature groups that may require selection, combination or further investigation.

Together, these visualisations help a hypothetical client understand relationships between engineering characteristics and market positioning while informing future feature selection.

## Analysis Techniques Used

### Data inspection

Pandas methods including:

* `df.info()`
* `df.shape`
* `df.columns`
* `df.dtypes`
* `isnull().sum()`
* `duplicated().sum()`
* `nunique()`
* `unique()`

were used to understand dataset structure and quality.

### Data cleaning

String replacement was used to correct obvious spelling inconsistencies in car names before extracting manufacturers and performing grouped analysis.

The process relied partly on manual inspection of unique values. A larger real-world dataset would benefit from systematic validation and standardised reference categories.

### Feature engineering

The following features were created:

* `manufacturer` — extracted from `CarName`
* `cylinder_count` — converts cylinder descriptions into numerical counts
* `footprint` — combines `carlength` and `carwidth`

These were selected because they provide clearer analytical interpretations for market and engineering comparisons.

### Grouped descriptive analysis

`groupby()`, `agg()`, `query()` and `sort_values()` were used to compare manufacturers by:

* Number of cars
* Mean and median price
* Minimum and maximum price
* Average engine size
* Average horsepower
* Average curb weight
* Average city fuel efficiency

Grouping allowed individual observations to be summarised at manufacturer level.

### Correlation analysis

Pearson correlation was used to investigate linear relationships between numerical features. This helped identify:

* Features strongly associated with price
* Highly correlated vehicle-size characteristics
* Potential redundancy between numerical predictors

Correlation does not establish causation, detect all non-linear relationships or determine which variables are independently useful in a multiple regression model.

### Data visualisation

Matplotlib and Seaborn were used for:

* Bar charts
* Scatter plots
* Correlation heatmaps

The analysis progressed from understanding and cleaning the data, through feature engineering and exploratory questions, to consideration of future predictive modelling.

### Alternative approaches

The current notebook stops before implementing a full machine-learning model. Future approaches could include:

* Multiple linear regression
* Feature selection based on model performance
* Variance Inflation Factor (VIF) analysis
* Ridge and Lasso regression
* Principal Component Analysis for selected numerical features
* Methods suitable for mixed numerical and categorical data
* Non-linear models

## Use of Generative AI

Generative AI, including ChatGPT, was used as an ideation and learning aid. It supported:

* Understanding automotive variables
* Grouping variables conceptually
* Generating exploratory questions
* Developing feature-engineering ideas
* Explaining Pandas operations and analytical concepts
* Suggesting alternative analytical and modelling approaches

AI suggestions were reviewed and adapted to the actual dataset. Final analysis decisions and interpretations were based on the notebook's code and results.

## Unfixed Bugs

No known software bugs prevented the implemented analyses from running.

However, the project has several **limitations and unfinished areas**:

* The dataset contains only 205 observations, limiting generalisability.
* Some manufacturers have small sample sizes, making their averages less reliable.
* Manual spelling correction may not identify every inconsistency in larger datasets.
* `footprint` is a simplified measure of vehicle size.
* Correlation does not establish independent predictive effects.
* Multicollinearity was identified as a potential issue but not formally tested using VIF.
* Multiple linear regression was proposed but not implemented.
* The dataset does not contain enough contextual information to establish how representative it is of the wider American car market.

A key knowledge gap was **automotive business and engineering domain knowledge**. This was addressed by researching variable meanings and distinguishing broad engineering characteristics from highly specific vehicle features. Further domain research would be required before making strong real-world automotive claims.

## Development Roadmap

Future development could include:

1. **Complete additional data validation**

   * Standardise remaining text formatting.
   * Check category frequencies and small groups.
   * Investigate extreme observations.

2. **Develop a predictive baseline**

   * Create a train/test split.
   * Use the training-set mean price as a simple baseline.

3. **Build multiple linear regression models**

   * Start with a small set of engineering features.
   * Add vehicle-size characteristics.
   * Encode categorical variables appropriately.
   * Compare models with and without manufacturer.

4. **Evaluate multicollinearity**

   * Calculate VIF values.
   * Compare models containing correlated features with reduced feature sets.
   * Investigate PCA for selected numerical groups.

5. **Compare feature-engineering approaches**

   * Test `footprint` against its component variables.
   * Explore interpretable features such as power-to-weight ratio.
   * Compare features using out-of-sample performance.

6. **Evaluate predictive performance**

   * Use MAE, RMSE and R².
   * Compare training and test performance.
   * Inspect residuals and regression assumptions.

7. **Develop domain knowledge**

   * Research automotive engineering variables and market significance.
   * Investigate how pricing analysts distinguish engineering cost, performance, brand positioning and consumer demand.

The main challenge was moving from numerous technical automotive variables to a coherent framework suitable for both technical and business audiences. This was addressed by grouping variables conceptually, researching their meanings and beginning with exploratory analysis rather than immediately applying a predictive model.

Future learning priorities include regression diagnostics, feature selection, multicollinearity and methods for mixed numerical and categorical data.

## Main Data Analysis Libraries

### Pandas

Pandas was used for data loading, cleaning, transformation and grouped analysis.

Examples:

```python
df.info()

df.isnull().sum()

df.duplicated().sum()
```

Feature extraction:

```python
df['manufacturer'] = df['CarName'].str.split().str[0]
```

Grouped descriptive analysis:

```python
manufacturer_price = (
    df.groupby('manufacturer')['price']
    .agg(['count', 'mean', 'median', 'min', 'max'])
    .sort_values('mean', ascending=False)
)
```

Filtering grouped results:

```python
manufacturer_price.query('count >= 3')
```

### NumPy

NumPy was imported for numerical operations and is available for future feature engineering and modelling extensions.

### Matplotlib

Matplotlib was used to customise visualisations, including figure size, axis labels, titles and tick rotation.

Example:

```python
plt.figure(figsize=(12, 6))

plt.xticks(rotation=45)

plt.xlabel('Manufacturer')

plt.ylabel('Average Price')

plt.show()
```

### Seaborn

Seaborn was used for higher-level statistical visualisations including bar plots, scatter plots and correlation heatmaps.

Example:

```python
sns.barplot(
    data=manufacturer_plot,
    x=manufacturer_plot.index,
    y='mean'
)
```

and:

```python
sns.heatmap(
    df[size_features].corr(),
    annot=True,
    cmap='coolwarm',
    fmt='.2f'
)
```

## Credits

### Content

* The dataset was obtained from the [Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data).
* The initial project structure was adapted from the Code Institute README template.
* ChatGPT supported ideation, automotive-variable interpretation, exploratory-analysis planning, Pandas guidance and code discussion.
* AI assistance was reviewed and adapted to the dataset and project requirements.
* Pandas, Matplotlib and Seaborn documentation should be referenced for implementation details or code patterns directly adapted from their documentation.

### Media

No external photographs or media assets were used in the notebook analysis.

The Code Institute logo in the README is provided through the Code Institute image resource included in the template.

## Acknowledgements

Thanks to Code Institute for the project template and learning framework that guided the project structure.

Thanks to the Kaggle dataset contributor for making the car-price dataset publicly available for analysis and learning.

Thanks to ChatGPT for assistance with ideation, data-analysis concepts, automotive feature interpretation and code explanations during development.
