# Statistical Analysis of U.S. Certified Organic Livestock (2008 vs. 2011)

An empirical statistical evaluation of U.S. state level certified organic livestock data. This project investigates temporal shifts across a 3-year period (2008 vs. 2011) and compares regional headcounts between Western and Southern states using parametric hypothesis testing in Google Sheets.

---

## Executive Summary

* **Temporal Comparison (2008 vs. 2011):** A paired two sample $t$ test evaluated nationwide state level organic livestock totals ($n = 50$). The test yielded $p = 0.7152$, showing **no statistically significant change** in national organic livestock counts over time.
* **Regional Comparison (West vs. South in 2011):** Welch's independent two sample $t$ test ($df \approx 22.23$) compared Western ($n_1 = 12$) and Southern ($n_2 = 14$) states. Despite higher sample means in the West ($\bar{X} = 13,412$) versus the South ($\bar{X} = 6,329$), the difference was **not statistically significant** ($p = 0.4128$) due to extreme state level variance and small sample sizes.

---

## Hypothesis Testing Summary

| Parameter | National Paired Test (2008 vs. 2011) | Regional Independent Test (West vs. South, 2011) |
| :--- | :--- | :--- |
| **Test Type** | Paired Two-Sample $t$ Test | Welch's Independent $t$ Test (Unequal Variance) |
| **Null Hypothesis ($H_0$)** | $\mu_{2008} = \mu_{2011}$ | $\mu_{\text{West}} = \mu_{\text{South}}$ |
| **Sample Size ($n$)** | $n = 50$ states | $n_{\text{West}} = 12$, $n_{\text{South}} = 14$ |
| **Degrees of Freedom ($df$)** | $49$ | $\approx 22.23$ |
| **Calculated $t$-Statistic** | $0.3670$ | $0.8346$ |
| **Critical Value ($\alpha = 0.05$)**| $2.0096$ | $2.0739$ |
| **$p$-Value** | $0.7152$ | $0.4128$ |
| **Statistical Decision** | **Fail to Reject $H_0$** | **Fail to Reject $H_0$** |

---

## Technical Implementation & Formulas

* **Data Cleaning:** Non numeric characters and missing records were filtered using dynamic arrays (`=FILTER()`) to compile contiguous ranges for subgroup testing.
* **Paired $t$ Test Execution:**
  * Difference calculation: `=N9:N58 - H9:H58`
  * Test $p$ value: `=T.TEST(H9:H58, N9:N58, 2, 1)`
* **Welch's Two-Sample $t$-Test Execution:**
  * West 2011 filter: `=FILTER(N9:N58, B9:B58 = "West")`
  * South 2011 filter: `=FILTER(N9:N58, B9:B58 = "South")`
  * Test $p$-value: `=T.TEST(P9:P58, Q9:Q58, 2, 3)`
  * Calculated $t$-statistic: `=(AVERAGE(P9:P58) - AVERAGE(Q9:Q58)) / SQRT((VAR.S(P9:P58)/COUNT(P9:P58)) + (VAR.S(Q9:Q58)/COUNT(Q9:Q58)))`

---

## Risk & Error Analysis

* **Type I Error Risk (False Positive):** In the 2008 vs. 2011 national test, a Type I error would mean incorrectly concluding that nationwide organic livestock production changed when it had not. Because we failed to reject $H_0$, a Type I error was avoided.
* **Type II Error Risk (False Negative):** In the regional test, high variance ($s^2 > 400\text{M}$) combined with small sample sizes ($12$ vs. $14$) reduced the statistical power of the test. A Type II error may have occurred if a true regional difference exists but was obscured by state-level noise (e.g., Texas skewing regional totals).

---

## Future Recommendations

Because state-level livestock distributions exhibit heavy right-skewness and non-normality, parametric $t$-tests are sensitive to extreme outliers. Future analyses should apply non-parametric methods—specifically the **Mann-Whitney U Test (Wilcoxon Rank-Sum)**—to compare regional median ranks without assuming normally distributed population data.

```
This project was completed as part of the ALX Africa Data Analytics Program to analyze state level trends and statistical shifts in U.S. Certified Organic Livestock (COL) data between 2008 and 2011. Using parametric hypothesis testing in Google Sheets, the project evaluates nationwide temporal growth through paired t tests, assesses regional disparities between Western and Southern states using Welch's independent t tests, and addresses key methodological considerations such as data skewness, sample size constraints, and statistical power.
```
