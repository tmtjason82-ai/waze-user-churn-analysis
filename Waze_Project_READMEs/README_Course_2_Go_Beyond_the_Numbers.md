# Waze User Churn Analysis — Exploratory Data Analysis

**Course context:** Google Advanced Data Analytics — Course 2: *Go Beyond the Numbers: Translate Data into Insights*  
**Tools:** Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook  
**Project type:** Exploratory data analysis (EDA) and visualization

## Project overview
This notebook explores Waze user activity and churn patterns using summary statistics and visualizations. The goal is to identify behavioral signals and questions that could guide deeper analysis of user retention.

## Data source and acquisition
The notebook reads `waze_dataset.csv` using `pandas.read_csv()`. The course lab says the dataset is made available in the Coursera environment. It does not provide a public URL or document independent collection by the student. The appropriate provenance description is **course-provided Waze user data**.

The dataset has **14,999 observations and 13 original columns**. The churn label has 700 missing values, leaving 14,299 records with known labels.

## Workflow: inspection, cleaning, and analysis
1. Imported pandas, NumPy, Seaborn, and Matplotlib.
2. Loaded the CSV and reviewed the first rows, dataset dimensions, data types, and descriptive statistics.
3. Examined distributions of activity-related variables such as sessions, drives, total sessions, driving duration, activity days, and driving days.
4. Used box plots and histograms to inspect skewness and potential outliers; used categorical charts to inspect device and churn-label distributions.
5. Compared driving days with activity days, and examined retention by device.
6. Created `km_per_driving_day` by dividing driven kilometers by driving days.
7. Replaced positive and negative infinite values in that derived metric with zero to handle zero-denominator cases, then inspected the resulting distribution.
8. Examined churn proportions by driving-day count and calculated the percentage of a user's total sessions occurring in the last month.
9. Applied 95th-percentile capping to selected highly skewed numeric variables (`sessions`, `drives`, `total_sessions`, `driven_km_drives`, and `duration_minutes_drives`) to reduce the influence of extreme values in the prepared analysis data.

## Key findings
- Overall churn is approximately **17.7%** among records with known labels; retained users account for approximately 82.3%.
- The notebook's initial comparisons show a broadly similar churn/retention mix for iPhone and Android users. Device alone does not appear to explain the overall churn pattern.
- User activity varies widely, and several numeric variables are right-skewed with high-end values. Distribution plots help show why averages alone may not describe typical user behavior well.
- Driving-day frequency is a useful dimension for further churn investigation. Users with very few driving days warrant closer examination, although the visualization alone does not prove that low activity causes churn.
- The derived `km_per_driving_day` variable originally produced infinite values for zero driving days. These were replaced with zero in the notebook; this is a practical computational fix but can conflate “no driving days” with a true zero-distance-per-day value. A more explicit missing/undefined category may be preferable in a production analysis.

## Business implications
A useful follow-up is to examine early signs of disengagement, such as fewer active days or a drop in recent sessions, and test whether those signals predict future churn. Any retention intervention should be evaluated rather than assumed effective from descriptive charts alone.

## Limitations
This notebook is descriptive. It does not establish causality and does not build or validate a predictive model. The 95th-percentile capping changes extreme observations and should be documented when interpreting results. Missing churn labels should not be imputed without a defensible strategy. The dataset's public source is not specified in the notebook.

## Reproducibility
Expected input: `waze_dataset.csv` in the working directory. Required libraries: `pandas`, `numpy`, `matplotlib`, and `seaborn`.

## Attribution and sharing note
This README summarizes the analysis at a high level. Confirm the course-specific rules before publishing the original Coursera notebook, its prompts, starter code, or assessment answers. Use only content you are permitted to share.
