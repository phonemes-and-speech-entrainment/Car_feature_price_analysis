# Car Price Prediction Project

![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

Welcome to the Car Price Prediction Project repository. This project contains a comprehensive data preparation, exploratory analysis, and predictive modelling pipeline for an automotive dataset, structured across two Jupyter Notebooks.

## Dataset Content

*   **Dataset:** The dataset originates from a car price assignment dataset, sourced from [Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data) and stored locally as `CarPrice_Assignment.csv`.
*   **Size:** The raw dataset contains **205 observations** and **26 original columns**.
*   **Features:** The attributes cover a wide range of automobile specifications, grouped into:
    *   **Identification:** `car_ID`, `symboling`, `CarName`.
    *   **Body & Dimensions:** `carbody`, `drivewheel`, `wheelbase`, `carlength`, `carwidth`, `carheight`, `curbweight`, etc.
    *   **Engine Specs:** `enginetype`, `cylindernumber`, `enginesize`, `boreratio`, `horsepower`, etc.
    *   **Fuel & Performance:** `fueltype`, `aspiration`, `fuelsystem`, `citympg`, `highwaympg`.
*   **Target:** The primary target variable for the modelling stage is `price` (a continuous numeric variable in USD).

## Business Requirements

The primary business requirement is to build a robust machine learning model capable of accurately predicting car prices based on their specifications. To achieve this, the project must deliver on the following:

1.  **A Clean and Standardised Dataset:** The raw data must be cleaned of typos, inconsistencies, and formatting errors to ensure data integrity.
2.  **Reduced Feature Sparsity:** High-cardinality features, particularly `CarName`, must be engineered into higher-level, more generalisable features to prevent model overfitting.
3.  **A Documented Data Transformation Pipeline:** The ETL process must be clearly documented, allowing for the transparent and reproducible preparation of the analysis-ready dataset.
4.  **Actionable Data Insights:** An exploratory data analysis must be conducted to provide actionable insights into the key drivers of car pricing, guiding feature selection for modelling.
5.  **A Trained and Evaluated Predictive Model:** Several regression models must be trained and evaluated to identify the best-performing algorithm for predicting `price`, providing a benchmark for future model iterations.

## Hypothesis and How to Validate

The analysis was guided by the following hypotheses, which are explored in the EDA notebook:

*   **Hypothesis 1:** Car price is strongly correlated with engine performance and vehicle size. We expect to see a positive correlation between `price` and features such as `enginesize`, `horsepower`, and `curbweight`. This is validated in the EDA notebook through scatter plots and regression plots, which visualise the relationship between these continuous variables and the target `price`.
*   **Hypothesis 2:** Brand perception and market segment influence price. We hypothesize that `manufacturer` is a significant predictor of `price`, with luxury brands (e.g., Jaguar, Porsche) having higher median prices than economy brands (e.g., Chevrolet, Honda). This is validated by extracting the `manufacturer` feature and comparing price distributions across brands in the analysis notebook.
*   **Hypothesis 3:** Engine configuration impacts price. We expect that engine characteristics such as `enginetype` and `fueltype` will show distinct price distributions. This is validated by using box plots to compare price across categories such as `enginetype` and `fueltype`.

## Project Plan

The project followed a two-stage pipeline, executed within two Jupyter Notebooks.

1.  **Stage 1: ETL and Data Cleaning (`Car_Price_Data_Understanding_ETL.ipynb`)**
    *   **Data Loading:** Loaded the raw `CarPrice_Assignment.csv`.
    *   **Data Cleaning:** Corrected brand spelling errors (e.g., `vokswagen` → `volkswagen`) and trimmed whitespace. Mapped string representations of numerical features (e.g., `"two"` → `2`) to integers.
    *   **Feature Engineering:**
        *   Extracted a new **`manufacturer`** column to reduce the cardinality of the `CarName` feature.
        *   Created a **`CarModel_Standardised`** column, leveraging a custom AI-generated cross-reference file (`Car_Name_Corrections.xlsx`) to standardise model names, correct typos, and consolidate redundant trim levels, significantly reducing feature sparsity.
    *   **Schema Design:** Reorganised the DataFrame columns into a logical order (Identification, Body Specs, Engine Specs, Fuel/Performance, Target) for clarity.
    *   **Output:** Saved the clean, structured DataFrame to `Car_Price_Cleaned.csv`.

2.  **Stage 2: Exploratory Data Analysis & Modelling (`Car_Price_EDA_and_Stats.ipynb`)**
    *   **Data Loading:** Loaded the cleaned `Car_Price_Cleaned.csv`.
    *   **Descriptive Statistics:** Generated summaries (`describe()`, `info()`) to understand the central tendency, dispersion, and data types of all features.
    *   **Univariate Analysis:** Created histograms and box plots for all numerical variables to assess their distributions, skewness, and identify potential outliers.
    *   **Bivariate & Multivariate Analysis:** Generated targeted visualisations:
        *   **Box Plots:** Used to compare price distributions across key categorical features (`carbody`, `enginetype`).
        *   **Scatter/Regression Plots:** Used to explore the relationships between continuous features (`enginesize`, `boreratio`, `peakrpm`) and `price`.
        *   **Feature Interaction:** Created an ad-hoc `car_volume` feature from dimensions and plotted it against price to explore a combined feature's predictive power.
    *   **Interactive Dashboarding:** Built a four-view interactive Tableau dashboard to consolidate the key EDA findings and enable segment-level exploration of price drivers.

3.  **Stage 3: Predictive Modelling (`Car_Price_Prediction_ML.ipynb`)**
    *   **Feature Preprocessing:** Categorical features were encoded using One-Hot Encoding, and numerical features were scaled using `StandardScaler` to ensure all predictors contributed equally to the distance and penalty calculations of the models.
    *   **Feature Selection:** Redundant and highly correlated predictors (identified via Pearson's correlation and VIF analysis in Stage 2) were removed to reduce model complexity and improve generalisation.
    *   **Model Training & Comparison:** Several regression models were trained on the prepared dataset to establish a predictive benchmark for `price`:
        *   **Linear Regression:** Served as the interpretable baseline model, providing a reference point for the direct linear relationship between the selected predictors and price.
        *   **Principal Components Regression (PCR):** Addressed residual multicollinearity by transforming the predictors into a set of uncorrelated principal components prior to regression.
        *   **Ridge Regression:** Applied L2 regularisation to penalise large coefficients, reducing model variance and improving generalisation on unseen data.
    *   **Model Evaluation:** Each model was assessed using standard regression metrics (R², RMSE, and MAE) to compare predictive accuracy and select the best-performing algorithm for the final benchmark.

## The Rationale to Map the Business Requirements to the Data Visualisations

*   **To Validate the Need for Cleaning (Business Req #1 & #2):** The fuzzy string matching analysis on `CarName` visually demonstrates the severe data quality issue, with many near-identical entries. This directly justifies the subsequent cleaning and feature engineering steps.
*   **To Explore Price Drivers (Business Req #4):** Scatter plots (`enginesize` vs. `price`) and box plots (`carbody` vs. `price`) directly test our hypotheses about what drives price. A strong positive slope in a regression plot validates the hypothesis that larger engines command higher prices, providing clear, data-driven insights.
*   **To Understand Data Distributions (Business Req #3 & #5):** Histograms of variables like `price` and `horsepower` reveal right-skewed distributions. This is a critical insight, as many regression models assume normally distributed variables, indicating that a log transformation may be necessary for future modelling. Correlation heatmaps and the modelling step directly build on this to select the most impactful predictors.

## Analysis Techniques Used

### Data Cleaning
The raw dataset required a multi-step cleaning process to handle inconsistencies:
*   **String Normalisation:** All text fields were standardised (lowercasing, whitespace stripping).
*   **Fuzzy Matching (`difflib.SequenceMatcher`):** Used to programmatically identify likely spelling variants in car names (e.g., "toyota" vs. "toyouta").
*   **AI-Assisted Standardisation:** A custom-curated Excel file, generated with an AI "Car Market Expert" gem, was used to standardise high-cardinality model names, correct typos, and consolidate redundant model/trim designations into a clean `CarModel_Standardised` feature. This was a key step in reducing sparsity.

### Feature Engineering
*   **`manufacturer`:** Created by splitting the first token of `CarName`. This reduced cardinality from 147 unique model names to 22 distinct brands, a more robust feature for modelling.
*   **`CarModel_Standardised`:** Created to consolidate model names with typos and different trim levels under a single, clean identifier, dramatically improving data quality and reducing feature noise.
*   **`car_volume`:** Created as an ad-hoc feature during EDA to explore the combined impact of vehicle dimensions on price.

### Visualisations
A range of plot types were used for specific analytical purposes:
*   **Histograms & Box Plots (Univariate):** To assess the distribution, skewness, and outliers of numerical features.
*   **Count Plots:** To visualise the frequency distribution of low-cardinality categorical features (e.g., `drivewheel`).
*   **Box Plots (Bivariate):** To compare the distribution of `price` across categories like `carbody` and `enginetype`.
*   **Scatter & Regression Plots (Bivariate):** To examine the relationship and linearity between continuous predictors and the `price` target.

#### Interactive Tableau Dashboard

In addition to the static plots generated in the Jupyter Notebooks, an interactive Tableau dashboard was built to provide a consolidated, exploration-friendly view of the key relationships between vehicle characteristics and price. The dashboard is composed of four linked views: a scatter matrix of `Price` against core numerical drivers (`Enginesize`, `Curbweight`, `Citympg`); a hierarchical bar chart of average price by `Drivewheel` → `Carbody` → `Enginetype`; a paired bar chart illustrating the trade-off between fuel efficiency (`Citympg`) and power (`Horsepower`); and a multi-panel scatter plot visualising the drivers of `Horsepower`. Together, these views reveal the strongest price determinants — engine size, curb weight, drivetrain, and engine configuration — and make the classic efficiency-versus-power trade-off immediately apparent.

### Stats and Modelling
The project's analytical and modelling stages involved:
*   **Correlation Analysis:** Used to quantify the strength of linear relationships between numerical features and the target `price`, and to identify multicollinearity among predictors (e.g., between `enginesize` and `horsepower`).
*   **Normality Assessment:** The analysis of histogram shapes informed the need for potential data transformations (e.g., `np.log()`) on skewed features before applying regression models.
*   **Regression Modelling:** Several regression models were trained and evaluated to establish a predictive benchmark and compare their performance:
    *   **Linear Regression:** As a baseline model to assess the direct linear relationship between predictors and price.
    *   **Principal Components Regression (PCR):** To address potential multicollinearity by transforming predictors into uncorrelated principal components before regression.
    *   **Ridge Regression:** A regularisation technique (L2 penalty) to handle multicollinearity and reduce model complexity, improving generalisation.
*   **Feature Selection:** The EDA insights and correlation analysis were used to guide the selection of the most relevant features for these models, removing redundant or highly correlated predictors.

## Use of Generative AI

This project leveraged a novel collaborative workflow between a human expert and multiple, specialised AI tools to achieve a high-quality outcome.

*   **Car Market Expert Gem (by Google Gemini):** As per the user's instructions, a specialised AI assistant was configured with domain-specific knowledge of the automotive market. This gem was used to generate a structured taxonomy (`Car_Name_Corrections.xlsx`) that provided market context for vehicle model hierarchies, trim lineages, and specifications, which was essential for the accurate standardisation of the `CarModel_Standardised` feature.
*   **Code and Analysis Assistant (this AI):** My role was to act as a coding and data science assistant. I generated the Python code for the ETL pipeline, including the complex data transformations, string cleaning, and feature engineering logic. I also provided the code for generating the visualisations and the mathematical and statistical rationale for their use, explaining why different plots were selected to answer specific analytical questions. Furthermore, I assisted in the implementation and explanation of the regression models used for price prediction.

## Unfixed Bugs

There are currently no known bugs in the project code.

## Development Roadmap

The next stages of the project are:
1.  **Advanced Model Optimisation:** Apply hyperparameter tuning techniques (e.g., GridSearchCV, RandomizedSearchCV) to the best-performing models (Linear, PCR, Ridge) to further improve their predictive accuracy.
2.  **Explore Alternative Algorithms:** Expand the model comparison to include more advanced algorithms such as tree-based models (Random Forest, Gradient Boosting, XGBoost) and Support Vector Regression to determine if they outperform the linear models.
3.  **Cross-Validation and Robust Evaluation:** Implement k-fold cross-validation to ensure the model's performance is robust and not overly dependent on a single train-test split. Use a wider range of evaluation metrics (e.g., RMSE, MAE, R²) for a more complete comparison.
4.  **Deployment Preparation:** Package the final, best-performing model and its preprocessing pipeline (e.g., using `joblib` or `pickle`) for eventual deployment into a simple web application or API.

## Main Data Analysis Libraries

*   **Pandas:** For data loading, cleaning, manipulation, and aggregation in DataFrames.
*   **NumPy:** For efficient numerical operations, especially on arrays and matrices.
*   **Matplotlib:** For creating foundational and customisable plots.
*   **Seaborn:** For generating high-level, aesthetically pleasing, and informative statistical graphics.
*   **SciPy:** Used primarily via its `scipy.stats` module for statistical hypothesis testing, including **Pearson's correlation coefficient** to quantify linear relationships and **one-way ANOVA** to compare group means across categorical features.
*   **Statsmodels:** Used via `statsmodels.stats.outliers_influence.variance_inflation_factor` (VIF) to detect and quantify **multicollinearity** among predictor variables, informing feature selection prior to regression modelling.
*   **Scikit-learn:** For the implementation of machine learning models (LinearRegression, Ridge, PCA) and preprocessing tools (StandardScaler).
*   **OpenPyXL:** For reading the `Car_Name_Corrections.xlsx` file used during data cleaning.
*   **Difflib:** For using the `SequenceMatcher` class to identify spelling inconsistencies in car names.
*   **Re (Regular Expression):** For pattern-based text cleaning and standardisation.

## Credits

### Content

*   The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data).
*   The project structure and objectives were inspired by coursework from the **Code Institute**.
*   The detailed model standardisation taxonomy (`Car_Name_Corrections.xlsx`) was generated using a user-created, specialised AI assistant ("Car Market Expert Gem"), which provided automotive domain knowledge.

### Media

*   The Code Institute logo was used as per the project template.

### Acknowledgements

This project is a testament to a collaborative, human-in-the-loop workflow that seamlessly blended multiple forms of intelligence and expertise:
*   The **user's domain knowledge** was the foundational driving force, particularly in guiding the strategic approach to feature engineering and model standardisation.
*   The **user's "Car Market Expert Gem"** provided the specialised, industry-specific data needed for high-quality model curation.
*   The **Code Institute's** educational materials provided the overall project framework and best practices.
*   The user collaborated with  **code and data science AI assistants (Gemini Notebook, Deepseek, Chat GPT 6)** to translate the combined human and AI-driven requirements into robust, efficient code and to provide the technical and theoretical explanations for the analytical techniques employed.

Last but not least, thanks to Phil for providing his unique expert insight into spotting car spelling mistakes.