# Waze User Churn Analysis — Hypothesis Testing by Device Type

**Course context:** Google Advanced Data Analytics — Course 3: *The Power of Statistics*  
**Tools:** Python, pandas, NumPy, SciPy, Jupyter Notebook  
**Project type:** Descriptive statistics and two-sample hypothesis test

## Project overview
This notebook investigates whether average monthly driving activity, measured by the number of drives, differs between Waze users on iPhone and Android. It uses descriptive statistics to frame the comparison and Welch's independent two-sample t-test to assess whether the observed difference is statistically significant.

## Data source and acquisition
The notebook loads `waze_dataset.csv` with `pandas.read_csv()`. The course lab indicates that the file is supplied in the Coursera environment. The notebook does not identify a public download URL or show independent data collection, so the dataset should be described as **course-provided Waze user data**.

The dataset contains 14,999 records and includes `drives`, `device`, and `label` among its variables. There are 700 missing values in `label`; the device comparison uses the drive counts for each device group.

## Analysis workflow
1. Imported pandas, NumPy, and `scipy.stats`.
2. Loaded the dataset and inspected descriptive information.
3. Mapped the categorical device values to numeric codes in an additional `device_type` column (`iPhone` = 1, `Android` = 2) for group-based comparison.
4. Calculated mean drives for each device group.
5. Set up a two-sided hypothesis test:
   - **Null hypothesis (H₀):** The population mean number of drives is equal for iPhone and Android users.
   - **Alternative hypothesis (H₁):** The population mean number of drives differs between the two groups.
6. Used a significance level of **α = 0.05**.
7. Ran an independent two-sample t-test with `equal_var=False`, i.e. Welch's t-test, which does not assume equal population variances.

## Results
- Mean drives for iPhone users: **67.86**.
- Mean drives for Android users: **66.23**.
- Test statistic: approximately **1.464**.
- p-value: approximately **0.1434**.
- Because p > 0.05, the analysis **fails to reject the null hypothesis**. The observed difference is not statistically significant at the 5% level.

## Interpretation
The sample average is slightly higher for iPhone users, but the test does not provide sufficient evidence to conclude that the population mean number of drives differs between iPhone and Android users. This result does **not** prove the means are identical; it means the observed evidence is insufficient to establish a difference at the chosen significance level.

## Business implications
Device type alone should not be treated as a demonstrated driver of driving frequency based on this test. Further analysis could consider activity days, driving days, onboarding tenure, and other behavioral features. Additional tests should be planned with clear hypotheses and attention to multiple comparisons where relevant.

## Limitations
- The analysis tests a difference in mean drive counts; it does not directly test whether device type affects churn.
- Statistical significance does not establish causality or business importance.
- The dataset is course-provided, and its public provenance is not documented in the notebook.
- Missing churn labels are relevant to churn-specific analyses, though the device-group drive comparison is based on `drives` and `device`.
- The test result depends on the dataset and assumptions; it should not be generalized beyond the analyzed sample without considering representativeness.

## Reproducibility
Expected input: `waze_dataset.csv` in the working directory. Required libraries: `pandas`, `numpy`, and `scipy`.

## Attribution and sharing note
This README is a high-level project description, not a replacement for course assessment material. Check the applicable Coursera sharing rules before publishing the original notebook, starter code, prompts, or restricted assessment answers.
