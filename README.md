# Wind-Turbine-EDA_Project
Wind Turbine Failure EDA
Exploratory Data Analysis to understand patterns, trends, and failure drivers in wind turbine SCADA data, with visual analytics, outlier detection, discretization, auto-EDA, and feature scaling workflows

KEY OBJECTIVES
Inspect structure, quality, and distributions of operational variables.
Visualize relationships affecting power output and failure status.
Prepare data via imputation, winsorization, discretization, and encoding for downstream modeling.

OPEN IN COLAB
A Colab badge is embedded in the notebook to run everything in the cloud environment.

DATASET
Wind turbine operational data with columns such as date, Wind_speed, Power, Generator_speed, ambient/nacelle/bearing temperatures, Wind_direction, and Failure_status. The notebook expects a CSV at /content/Wind_Turbine_2025.csv in Colab.

PROJECT STRUCTURE
Wind_Turbine_Project.ipynb — main EDA notebook with visualizations and preprocessing.
Outputs written by the notebook:
wind_turbine_clearedNV.csv — median-imputed numeric features.
wind_turbine_cleaned.csv — post-imputation cleaned frame.
wind_turbine_discretized.csv — adds categorical bins for speed, temperature, direction.
wind_turbine_standardized.csv — standardized numeric features.
wind_turbine_normalized.csv — min–max scaled numeric features.
Wind_Turbine_Profile_Report.html — full ydata-profiling report.

PREREQUISITES 
Python 3.8+ (Colab default works).
Libraries: pandas, numpy, matplotlib, seaborn, plotly, bokeh, scipy, scikit-learn, feature_engine, dtale, ydata-profiling.

Quick start (Colab)
Upload Wind_Turbine_2025.csv to /content in Colab.
Run the notebook cells top-to-bottom; pip installs are included for dtale, ydata-profiling, and feature_engine.
Generated reports and CSVs are saved in the working directory and can be downloaded.
Installation notes
ydata-profiling (formerly pandas-profiling) installs via: pip install -U ydata-profiling; widget support may require ydata-profiling[notebook] and enabling ipywidgets. Kernel restart may be needed in Colab.
D-Tale runs a local Flask server; in managed environments it can open a dynamic port or the specified host/port. Use dtale.show(df, host='localhost', port=8000) as shown in the notebook.

What the notebook does
1) Setup and data load
Imports pandas, numpy, plotting libraries (matplotlib, seaborn, plotly, bokeh), and utility packages.
Loads /content/Wind_Turbine_2025.csv, parses date to datetime, and derives Year.
Splits columns into numerical and categorical lists for targeted analysis.

2) Initial exploration
df.info(), head(), tail(), describe(), dtypes to check schema and summary stats.
Missing values summary and a heatmap to visualize sparsity patterns.

3) Univariate analysis
Business moments per numeric feature: mean, median, mode, variance, standard deviation, range, skewness, kurtosis.
Histograms grid with KDE for distribution shape.
Boxplots grid and IQR-based outlier detection printouts.
Count plots for categorical columns.

4) Class balance and label view
Plotly donut pie of Failure_status.
Bokeh bar chart showing class imbalance with an interactive toolbar.

5) Bivariate and multivariate
Scatter: Wind_speed vs Power, static and interactive (colored by Failure_status).
Boxplot and violin plots contrasting Failure_status with Generator_speed and Power distributions.
Pairplot for numeric features and correlation heatmap for linear relations.

6) Time series views
Plotly lines for Power and Wind_speed over time; seaborn line colored by Failure_status.
Faceted line grids: each numeric feature over time by Failure_status.
Year-over-year overlays by day-of-year to compare seasonal dynamics.
Lag plot for Power to inspect autocorrelation patterns.

7) Aggregations
groupby(Failure_status).mean() for quick class-level numeric summaries.

8) Auto-EDA
D-Tale interactive dataframe explorer (dtale.show) for quick grid, filters, charts, and code export.
ydata-profiling report generation and HTML export with explorative=True.

9) Data quality and cleaning
Duplicate check via df.duplicated() and count.
Numeric missing value imputation with median; save cleaned CSVs.
Winsorization using feature_engine Winsorizer with IQR capping on both tails; visualize post-winsorization boxplots.

10) Feature engineering
Discretization:
Wind_speed into Very Low/Low/Medium/High.
Ambient, Bearing, Nacelle, Hub, and Gearbox inlet temperatures into Very Cold/Cold/Moderate/Hot bins.
Wind_direction into quadrant-like sectors.
Encoding:
pd.get_dummies to dense integer columns.
OneHotEncoder(sparse_output=False) with explicit feature names.
Normality aid:
Q–Q plot for Power; Yeo-Johnson transformer scaffold for distribution correction.

11) Scaling
Standardization via StandardScaler; output saved.
Min–max normalization via MinMaxScaler; output saved.
