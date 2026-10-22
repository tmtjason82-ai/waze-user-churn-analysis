# Waze User Churn Analysis — Data Inspection & Preparation

**Course context:** Google Advanced Data Analytics — Course 1: *Foundations of Data Science*  
**Tools:** Python, pandas, NumPy, Jupyter Notebook  
**Project type:** Guided learning project / exploratory data preparation

## Project overview
This notebook performs an initial inspection of Waze user activity data to understand its structure, assess data quality, and prepare the dataset for subsequent exploratory and statistical analysis. The business context is user churn: identifying patterns that may help the team understand which users stop using the app.

## Data source and acquisition
The notebook loads `waze_dataset.csv` using `pandas.read_csv()`. The notebook instructions state that the CSV is automatically made available in the Coursera lab environment. The notebook itself does not document a public download URL or an independent collection process; therefore, the dataset should be described as **course-provided Waze user data**, not as data personally collected or scraped.

The dataset contains **14,999 rows and 13 original columns**. Variables include a user ID, churn/retention label, session and drive counts, total sessions, days since onboarding, favorite-navigation counts, distance and duration driven, activity days, driving days, and device type.

## Data inspection and preparation
1. Imported `pandas` and `NumPy`.
2. Loaded the CSV into a DataFrame.
3. Inspected sample rows with `head()` and structure/types/non-null counts with `info()`.
4. Compared records with missing `label` values against records with a known label.
5. Counted missing labels by device to check whether missingness was disproportionately associated with one device group.
6. Summarized churned versus retained users using counts, percentages, medians, and device composition.
7. Created derived metrics to examine behavior:
   - `km_per_drive`: driven kilometers divided by drives.
   - `km_per_driving_day`: driven kilometers divided by driving days.
   - `drives_per_driving_day`: drives divided by driving days.

### Data quality notes
- **700 of 14,999 rows (about 4.7%) have a missing `label`.** The other 14,299 records have a known label.
- Among the 700 rows with missing labels, 447 are iPhone users and 253 are Android users. This is broadly similar to the overall device mix, so the notebook does not establish a strong device-specific missingness problem.
- The missing target labels are not automatically equivalent to churn. They should be treated as unknown labels unless further documentation establishes otherwise.
- Derived ratios can be undefined when their denominator is zero. Such cases need explicit handling before those metrics are used for modeling or interpretation.

## Key findings
- Of the records with known labels, **2,536 were marked churned and 11,763 retained**. That is approximately **17.7% churn** and **82.3% retained**, calculated on the labeled records.
- The median number of drives is lower for churned users than retained users (50 versus 59 in the notebook's summary).
- The derived metrics show behavioral differences worth exploring, but ratios involving driving days can be distorted by zero denominators and should be interpreted carefully.
- Device mix is broadly similar across churned and retained groups; this initial inspection does not establish device type as a strong explanation of churn.

## Limitations
This is an initial data-understanding exercise, not a causal study or a validated churn-prediction model. The notebook uses a course-provided dataset whose public provenance is not specified in the notebook. Missing labels limit analyses that depend on the churn outcome, and derived ratios require careful treatment of zero denominators and extreme values.

## Suggested next steps
- Continue with EDA to inspect distributions, outliers, and relationships between user activity and churn.
- Decide explicitly how to handle rows with missing target labels.
- Validate ratio features and avoid dividing by zero.
- Investigate behavioral and lifecycle features before making product or retention recommendations.

## Reproducibility
The notebook expects `waze_dataset.csv` to be available in the working directory. Required libraries: `pandas` and `numpy` (plus a Jupyter environment).

## Attribution and sharing note
This is a portfolio-oriented summary of a guided course exercise. Before publishing the original notebook or any course-provided materials, check the applicable Coursera course terms and assessment-sharing rules. Do not include restricted prompts, answer keys, starter files, or course-owned materials without permission.
