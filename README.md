# Car Price Analysis

This project explores the relationships between car prices and a range of market, vehicle and engineering characteristics. The analysis uses exploratory data analysis (EDA), data cleaning, feature extraction, grouped descriptive statistics, correlation analysis and visualisation to identify characteristics that may be useful for understanding and eventually predicting car prices.

The project is designed to provide insights from both an **engineering perspective**, by examining relationships between vehicle and engine characteristics, and a **market-pricing perspective**, by investigating how characteristics such as manufacturer, engine size and vehicle size are associated with price.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

The dataset used in this project is the **Car Price Prediction** dataset, available from Kaggle:

[Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data?utm_source=chatgpt.com)

The dataset contains **205 observations and 26 original columns**, with each row representing a car. The variables include:

* A unique car identifier and car name
* Insurance risk information
* Fuel and aspiration type
* Body and drivetrain configuration
* Physical vehicle dimensions and weight
* Engine design and size
* Internal engine measurements
* Engine performance characteristics
* Fuel-efficiency measures
* Car price

The target variable for potential future predictive modelling is `price`.

During the analysis, two additional features were created:

* `manufacturer`, extracted from `CarName`
* `cylinder_count`, which converts the categorical cylinder descriptions into numerical values

A further engineered feature, `footprint`, was created by multiplying car length by car width to provide a simple combined measure of the vehicle's physical footprint.

The notebook also identified and corrected several inconsistent spellings in the `CarName` column, including manufacturer and model names. No missing values or duplicate rows were identified in the original dataset.

## Business Requirements

The project takes the perspective of a hypothetical automotive pricing client, such as a car dealership, manufacturer, pricing analyst or market research partner.

The primary business requirement is to:

> **Understand which market, engineering and physical vehicle characteristics are most strongly associated with car price and identify promising features for future car price prediction models.**

The analysis aims to support questions such as:

* Which manufacturers have the highest average car prices in this dataset?
* Do higher-priced manufacturers tend to produce cars with different engineering characteristics?
* Are larger and heavier vehicles associated with higher prices?
* Which numerical vehicle features are strongly correlated and may contain overlapping information?
* Which variables should be investigated further as candidate predictors in a future multiple linear regression or other machine-learning model?

For a pricing client, this information could support more informed comparisons between vehicles and help identify the characteristics associated with different price segments. For an engineering or product-development audience, it can help illustrate how physical size, engine characteristics and performance-related variables are related within the dataset.

## Hypothesis and How to Validate

The main hypothesis is that:

> **Some vehicle characteristics provide more useful information about car price than others, and market characteristics such as manufacturer, together with broad engineering characteristics such as engine size and vehicle size, may be stronger candidate predictors than highly specific or redundant features.**

This hypothesis was investigated through exploratory analysis rather than treated as established in advance.

Validation involved:

* Inspecting the structure and data types of the dataset
* Checking for missing and duplicated values
* Correcting inconsistent car-name spellings
* Extracting a manufacturer variable from car names
* Converting cylinder number into a numerical feature
* Grouping cars by manufacturer and comparing descriptive price statistics
* Comparing manufacturer-level engineering characteristics
* Calculating correlations between numerical variables
* Visualising relationships using bar charts, scatter plots and heatmaps
* Identifying groups of highly correlated variables that may introduce redundancy or multicollinearity into a future regression model

The analysis found that manufacturer, engine size and several vehicle size-related variables showed strong positive associations with price. However, these findings should be interpreted as **exploratory associations within this dataset** rather than evidence that individual features independently cause higher prices.

Further validation would require a predictive modelling stage, including train/test evaluation, multiple linear regression diagnostics and assessment of multicollinearity.

## Project Plan

The project followed the following high-level process:

1. **Understand the dataset**

   * Inspect the dataset structure, shape, columns and data types.
   * Identify the apparent meaning and broad category of each variable.

2. **Check data quality**

   * Check for missing values and duplicate observations.
   * Inspect unique values to identify inconsistent categorical labels and spelling errors.

3. **Clean and prepare the data**

   * Correct obvious spelling inconsistencies in `CarName`.
   * Retain the original variables while creating additional features where useful.

4. **Engineer and extract features**

   * Extract `manufacturer` from `CarName`.
   * Convert categorical cylinder descriptions into `cylinder_count`.
   * Create a `footprint` feature from car length and width.

5. **Conduct exploratory data analysis**

   * Compare price distributions and descriptive statistics between manufacturers.
   * Investigate whether higher-priced manufacturers tend to have larger or more powerful engines.
   * Examine relationships between vehicle size, weight and price.
   * Explore the correlation structure of numerical vehicle characteristics.

6. **Interpret the results**

   * Identify promising candidate predictors of price.
   * Consider the possibility of multicollinearity and redundant information.
   * Identify limitations and areas requiring further automotive domain knowledge.

7. **Plan future modelling**

   * Use the exploratory findings to inform feature selection and the construction of a future multiple linear regression or alternative predictive model.

The data was managed in a single Pandas DataFrame throughout the project. Cleaning and feature engineering were performed before the main exploratory analyses so that grouping and visualisation used more consistent categories.

Exploratory and descriptive methodologies were chosen because the initial objective was to understand the data before building a predictive model. This approach allowed potentially important relationships and correlated feature groups to be identified before making modelling assumptions.

## The Rationale to Map the Business Requirements to the Data Visualisations

The visualisations were selected to answer specific business and analytical questions:

* **Average price by manufacturer:** helps a pricing or market analyst identify broad differences in the price positioning of manufacturers.
* **Manufacturer average engine size versus average price:** investigates whether differences in market price may be partly associated with differences in the engineering characteristics of cars produced by different manufacturers.
* **Vehicle size, weight and price correlation heatmap:** helps identify physical characteristics associated with price and highlights variables that may provide overlapping information.
* **Vehicle footprint versus price scatter plot:** explores whether a simple engineered measure combining vehicle length and width is associated with price.
* **Numerical feature correlation heatmap:** helps identify groups of highly correlated features that may require feature selection, combination or further investigation before predictive modelling.

Together, these visualisations support a hypothetical client interested in understanding how engineering characteristics and market positioning relate to vehicle prices, while also providing an evidence base for selecting features for future modelling.

## Analysis Techniques Used

The project used the following data analysis techniques:

### Data inspection

Pandas methods such as:

* `df.info()`
* `df.shape`
* `df.columns`
* `df.dtypes`
* `isnull().sum()`
* `duplicated().sum()`
* `nunique()`
* `unique()`

were used to understand the structure and quality of the dataset.

### Data cleaning

String replacement was used to correct obvious spelling inconsistencies in car manufacturer and model names. This was particularly important before extracting manufacturer information and performing grouped analysis.

A limitation is that the cleaning process relied partly on manual inspection of unique values. A larger real-world dataset would benefit from more systematic validation, standardised reference categories or domain-specific data-quality checks.

### Feature engineering

New features were created using existing variables:

* `manufacturer` was extracted from `CarName`
* `cylinder_count` converted text categories into numerical counts
* `footprint` combined `carlength` and `carwidth`

These transformations were chosen because they created variables with clearer analytical interpretations for market and engineering comparisons.

### Grouped descriptive analysis

`groupby()`, `agg()`, `query()` and `sort_values()` were used to compare manufacturers according to:

* Number of cars
* Mean and median price
* Minimum and maximum price
* Average engine size
* Average horsepower
* Average curb weight
* Average city fuel efficiency

Grouping was useful because it allowed individual observations to be summarised at a market or manufacturer level.

### Correlation analysis

Pearson correlation was used to investigate linear relationships between numerical features. This helped identify:

* Variables strongly associated with price
* Groups of vehicle-size characteristics that are highly correlated
* Potential redundancy between numerical predictors

A limitation is that correlation only measures particular types of relationships and does not establish causation. It can also miss non-linear relationships and cannot by itself determine which variables would be the best independent predictors in a multiple regression model.

### Data visualisation

Matplotlib and Seaborn were used to create:

* Bar charts
* Scatter plots
* Correlation heatmaps

The analysis was structured progressively: first understanding and cleaning the data, then creating useful features, then examining specific business questions, and finally considering how the findings could inform later predictive modelling.

### Alternative approaches

The notebook deliberately stops before implementing a full machine-learning model. Future approaches could include:

* Multiple linear regression
* Feature selection based on model performance
* Variance Inflation Factor (VIF) analysis for multicollinearity
* Regularised regression such as Ridge or Lasso
* Principal Component Analysis for selected correlated numerical features
* Methods suitable for mixed numerical and categorical data
* Non-linear models for comparison with linear regression

These approaches would allow the exploratory findings to be tested more formally.

### Use of Generative AI

Generative AI, including ChatGPT, was used as an ideation and learning aid during the project. It helped with:

* Understanding the likely meanings of automotive variables
* Grouping variables conceptually for initial data comprehension
* Generating ideas for exploratory questions
* Discussing possible feature-engineering approaches
* Explaining Pandas operations and analysis concepts
* Suggesting alternative ways to structure analyses and future modelling

AI-generated suggestions were reviewed and adapted to the actual dataset rather than accepted automatically. The final analysis decisions and interpretations were based on the code outputs and exploratory results produced in the notebook.

## Unfixed Bugs

No known software bugs prevented the notebook from running the implemented analyses.

However, the project has several **limitations and unfinished areas** that should not be described as bugs:

* The dataset contains only 205 observations, limiting the strength and generalisability of conclusions.
* Several manufacturer categories have small sample sizes, making their average prices less reliable.
* The manual spelling-cleaning process may not identify every possible inconsistency in a larger dataset.
* The `footprint` variable is a simplified measure of vehicle size and does not represent all physical dimensions.
* Correlation analysis identifies associations but does not establish independent predictive effects.
* Multicollinearity was identified as a potential issue but was not formally tested using methods such as VIF.
* A multiple linear regression model was proposed as a next step but was not implemented in the current notebook.
* The dataset does not provide sufficient contextual information to establish whether all observations accurately represent the wider American car market.

A significant knowledge gap identified during the project was **automotive business and engineering domain knowledge**. This was addressed by researching the conceptual meaning of variables and using the analysis to distinguish between broad engineering characteristics and highly specific vehicle features. Further domain research would be required before making strong real-world automotive claims.

## Development Roadmap

Future development of the project could include the following steps:

1. **Complete additional data validation**

   * Standardise remaining text formatting.
   * Check category frequencies and investigate very small groups.
   * Consider whether extreme observations should be analysed separately.

2. **Develop a predictive baseline**

   * Create a train/test split.
   * Establish a simple baseline prediction using the training-set mean price.

3. **Build multiple linear regression models**

   * Start with a small number of engineering features.
   * Add vehicle-size characteristics.
   * Add categorical variables using appropriate encoding.
   * Compare models with and without manufacturer information.

4. **Evaluate multicollinearity**

   * Calculate VIF values.
   * Compare models containing correlated features with reduced or engineered feature sets.
   * Investigate whether PCA is useful for selected numerical feature groups.

5. **Compare feature-engineering approaches**

   * Test whether `footprint` improves prediction compared with its component variables.
   * Create and test additional interpretable features, such as power-to-weight ratio.
   * Compare original and engineered features using out-of-sample performance.

6. **Evaluate predictive performance**

   * Use metrics such as MAE, RMSE and R².
   * Compare training and test performance.
   * Inspect residuals and regression assumptions.

7. **Develop domain knowledge**

   * Learn more about automotive engineering variables and their market significance.
   * Investigate how real-world vehicle pricing analysts distinguish engineering cost, performance, brand positioning and consumer demand.

The main challenge encountered during the project was moving from a dataset containing many technical automotive variables to a coherent analytical framework that could be understood by both technical and business audiences. This was addressed by grouping variables conceptually, investigating their meanings and beginning with exploratory questions rather than immediately applying a predictive model.

Future learning priorities include regression diagnostics, feature selection, multicollinearity analysis and more advanced methods for analysing mixed numerical and categorical datasets.

## Main Data Analysis Libraries

### Pandas

Pandas was used for data loading, cleaning, transformation and grouped analysis.

Examples include:

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

NumPy was imported as part of the numerical analysis environment and is available for numerical operations and future feature engineering or modelling extensions.

### Matplotlib

Matplotlib was used to construct and customise visualisations, including:

* Figure size
* Axis labels
* Plot titles
* Tick rotation

For example:

```python
plt.figure(figsize=(12, 6))
plt.xticks(rotation=45)
plt.xlabel('Manufacturer')
plt.ylabel('Average Price')
plt.show()
```

### Seaborn

Seaborn was used to create higher-level statistical visualisations, including:

* Bar plots
* Scatter plots
* Correlation heatmaps

For example:

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

* The dataset was obtained from the [Car Price Prediction dataset on Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data?utm_source=chatgpt.com).
* The initial project structure was adapted from the Code Institute project README template.
* ChatGPT was used for ideation, explanation of automotive variables, exploratory-analysis planning, Pandas guidance and code discussion. AI assistance was reviewed and adapted to the requirements and outputs of the project.
* Pandas, Matplotlib and Seaborn documentation should be referenced for any implementation details or code patterns directly adapted from their official documentation.

### Media

No external photographs or other media assets were used as part of the notebook analysis.

The Code Institute logo displayed in the project README is provided through the Code Institute image resource included in the template.

## Acknowledgements

Thanks to Code Institute for the project template and learning framework that guided the structure of this project.

Thanks to the Kaggle dataset contributor for making the car-price dataset publicly available for analysis and learning.

Thanks to ChatGPT for assistance with ideation, data-analysis concepts, automotive feature interpretation and code explanations during the development of the project.
