# Plant Growth Before and After Compost

Mini project: paired t-test using Python

Name: NUKALA JASHWANT SAI

PRN: B25CE1177

**Note:** The dataset is simulated. I did not have real plant measurements, so I made up 10 realistic values to show how the method works. The results only describe this sample data.

## Overview
This project checks whether the mean height of 10 plants is different after adding compost. Each plant is measured twice (before and after), so the data is paired and a two-tailed paired t-test is used.

## Objectives
- Create a simulated dataset of 10 paired height measurements (in cm)
- Find the mean, sample standard deviation (`ddof=1`), and the growth of each plant
- Do a paired t-test at the 5% significance level
- Draw a histogram, a box plot and a paired comparison chart
- Explain the result and its limits

## Dataset
Heights in cm. The values are typed directly in the notebook (no random generator), so the results are the same every time.

| Plant | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| Before | 12.5 | 14.0 | 11.8 | 13.2 | 15.1 | 12.9 | 13.6 | 14.4 | 11.5 | 13.9 |
| After | 15.8 | 17.1 | 14.2 | 16.9 | 18.0 | 15.4 | 16.1 | 18.3 | 14.6 | 16.5 |
| Growth | 3.3 | 3.1 | 2.4 | 3.7 | 2.9 | 2.5 | 2.5 | 3.9 | 3.1 | 2.6 |

## Software and Libraries
- Python 3.9 or above (Google Colab or Jupyter Notebook)
- `numpy` for arrays, mean and standard deviation
- `scipy` (`scipy.stats`) for `ttest_rel`, `shapiro` and the t-distribution
- `matplotlib` (`pyplot`) for the graphs (version 3.9 or newer, because `boxplot` uses `tick_labels`)

To install locally: `pip install numpy scipy matplotlib jupyter`

## Methodology
1. Enter the simulated before and after heights.
2. Find the growth of each plant: d = After - Before.
3. Calculate the mean and sample standard deviation.
4. Check normality of the differences with the Shapiro-Wilk test.
5. Do the paired t-test by hand using the formula and check it with `scipy.stats.ttest_rel`.
6. Draw the three graphs.
7. Write the interpretation and limitations.

## Hypotheses
- H0: mu_d = 0 (compost makes no difference to the mean height)
- H1: mu_d is not equal to 0 (mean height is different after compost, two-tailed)
- Significance level: alpha = 0.05. Reject H0 if p < 0.05.

## Formulas
- Mean growth: d_bar = (sum of d) / n
- Sample standard deviation: s_d = sqrt( sum of (d - d_bar)^2 / (n - 1) )
- Test statistic: t = d_bar / (s_d / sqrt(n))
- Degrees of freedom: df = n - 1

## How to Run
**Google Colab:** go to <https://colab.research.google.com/>, click File > Upload notebook, choose `Plant_Growth_Before_After_Compost.ipynb`, then click Runtime > Run all.

**Jupyter:** run `jupyter notebook`, open the `.ipynb` file, then click Kernel > Restart & Run All.

## Results (from the notebook output)
| Quantity | Value |
|---|---|
| Mean before (SD) | 13.29 cm (1.14) |
| Mean after (SD) | 16.29 cm (1.35) |
| Average growth (SD) | 3.00 cm (0.52) |
| t-statistic, df | 18.22, 9 |
| p-value (two-tailed) | 2.06e-08 |
| Critical t (+/-) | 2.262 |
| 95% CI for mean growth | [2.63, 3.37] cm |
| Decision | Reject H0 |

## Interpretation
In this simulated sample, the mean height after compost is significantly different from (and higher than) the height before, at the 5% level. All 10 plants show positive growth and the confidence interval does not contain 0.

Limitations: the data is made up, so the strong result only comes from how the values were written. There is also no control group, so even with real data this test would not prove that compost caused the growth, because normal growth over time, watering, weather or sunlight could also explain it. A sample of 10 is small too.

## References
- SciPy, `scipy.stats.ttest_rel`: https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_rel.html
- SciPy, `scipy.stats.shapiro`: https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.shapiro.html
- NumPy, `numpy.std`: https://numpy.org/doc/stable/reference/generated/numpy.std.html
- Matplotlib, `pyplot.boxplot`: https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html
- Wikipedia, Student's t-test: https://en.wikipedia.org/wiki/Student%27s_t-test
