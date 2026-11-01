# Project Explanation Guide
**Plant Growth Before and After Compost**
Student: NUKALA JASHWANT SAI (PRN: B25CE1177)

This guide is for explaining the project to someone (a teacher, examiner or friend) when you know nothing about statistics yet. Read it once from top to bottom, then use the speaking script and the question-answer section to practice.

---

## 1. The project in one line

> "I checked whether plants grew taller after adding compost, by measuring the same 10 plants before and after and using a paired t-test in Python. The data is simulated, so this demonstrates the method and does not prove anything about real compost."

If you forget everything else, remember this sentence.

---

## 2. The big idea in simple words

Imagine you have 10 plants. You measure how tall each one is. Then you add compost, wait some time, and measure the same 10 plants again.

Every plant will probably be a bit taller, because plants grow anyway. So the real question is:

**Is the average increase big enough that it is unlikely to be just luck or random variation?**

A t-test is a tool that answers this question with a number. It tells us how surprising our result would be if compost actually did nothing.

---

## 3. Why is the data "simulated"?

I did not have real plants to measure, so I made up 10 realistic height values and typed them into the notebook. This is allowed as long as it is clearly stated, and I have written "simulated" in the notebook, the graphs and the README.

Because the data is made up:
- the method (the steps and the code) is real and works for any real data
- the result (the numbers) only describes my made-up data

If someone gave me real measurements, I could replace the two lists in the code and everything else would run the same way.

---

## 4. Words you must understand

Learn these in plain language. You do not need textbook definitions.

| Term | Simple meaning |
|---|---|
| **Mean (average)** | Add all values and divide by how many there are. |
| **Standard deviation (SD)** | How spread out the values are around the mean. Small SD means values are close together. Large SD means they are far apart. |
| **Sample** | A small group (here 10 plants) used to learn about a bigger group. |
| **Sample SD, `ddof=1`** | Divide by n - 1 instead of n. We do this because we are using a sample, and dividing by n - 1 gives a better estimate. |
| **Paired data** | Two measurements on the same item (same plant before and after). Each "before" belongs to one "after". |
| **Growth (d)** | After minus Before for each plant. |
| **Hypothesis** | A claim that we test with data. |
| **Null hypothesis (H0)** | The "nothing happened" claim: average growth is 0, so compost has no effect. |
| **Alternative hypothesis (H1)** | The "something happened" claim: average growth is not 0. |
| **Two-tailed test** | We check for a change in either direction (taller or shorter), not only taller. |
| **Significance level (alpha = 0.05)** | Our cut-off for being convinced. 0.05 means 5%. It is the standard choice used in most courses. |
| **t-statistic** | How many "standard errors" the average growth is away from 0. A big t means the result is far from "no change". |
| **Degrees of freedom (df)** | n - 1. Here 10 - 1 = 9. It decides which t-distribution is used. |
| **p-value** | If compost really did nothing, this is the chance of seeing a growth as big as ours (or bigger) just by luck. Small p-value means our result is hard to explain by luck. |
| **Confidence interval (CI)** | A range in which the true average growth probably lies. |
| **Causation** | One thing actually causing another. A t-test alone cannot prove this. |

### The decision rule (very important)
- If **p < 0.05**, reject H0. The result is "statistically significant".
- If **p >= 0.05**, fail to reject H0. We do not have enough evidence of a difference.

Note: we say "reject" or "fail to reject" H0. We never say "we proved H0".

---

## 5. Step-by-step: what the notebook does

Follow the notebook sections in this order while presenting.

**Section 1 to 2: Aim, hypotheses and formulas**
Explain the goal and state H0 and H1. Show the formula for t:

t = (average growth) / (SD of growth / square root of n)

In words: the average growth divided by how much we expect the average to wobble by chance.

**Section 3: Import libraries**
- `numpy` handles the numbers (mean, standard deviation, arrays)
- `scipy.stats` does the statistics (t-test, normality test)
- `matplotlib.pyplot` draws the graphs

**Section 4: Dataset**
Two lists of 10 numbers, `before` and `after`, and `growth = after - before`. Heights are in cm. Mention again that it is simulated.

**Section 5: Descriptive statistics**
Finds the mean and SD for before, after and growth. This just describes the data.

**Section 6: Normality check (Shapiro-Wilk)**
The t-test works best when the growth values are roughly bell-shaped (normal). We check this. Our p-value is 0.3366, which is above 0.05, so there is no sign of a problem. With only 10 values this check is a rough guide, not a guarantee.

**Section 7: The paired t-test**
Done twice on purpose:
1. by hand, using the formula
2. with `stats.ttest_rel(after, before)`

Both give the same answer and the code checks this with an `assert`. This shows that the library result matches the formula and is not a black box.

**Section 8: Three graphs** (explained in Section 7 of this guide)

**Section 9 to 11: Summary, interpretation and conclusion**
Collects the final numbers, explains what they mean and states the limits.

---

## 6. The results in simple words

| Item | Value | What it means |
|---|---|---|
| Mean before | 13.29 cm (SD 1.14) | Average starting height |
| Mean after | 16.29 cm (SD 1.35) | Average height after compost |
| Average growth | 3.00 cm (SD 0.52) | On average each plant grew 3 cm, and the growth was similar for all plants |
| Standard error | 0.1647 | How much the average growth would wobble by chance |
| t-statistic | 18.22 | The average growth is about 18 standard errors away from 0 |
| Degrees of freedom | 9 | 10 pairs minus 1 |
| Critical t | 2.262 | If |t| is bigger than this, we reject H0 |
| p-value | 2.06 x 10^-8 (about 0.00000002) | Roughly 2 chances in 100 million that this would happen by luck if compost did nothing |
| 95% CI of growth | 2.63 to 3.37 cm | True average growth is probably in this range. It does not include 0. |
| Decision | Reject H0 | Because 0.00000002 is far smaller than 0.05 |

**How to say the conclusion:**
"In this simulated data, the average height after compost is significantly higher than before at the 5% level, so we reject the null hypothesis."

**Why is the result so strong?**
Because I made up the values, and I made the growth quite similar for every plant (all between 2.4 and 3.9 cm). Real plant data is usually messier, so real p-values are usually not this tiny. Say this honestly if asked.

---

## 7. The three graphs explained

**1. Histogram of growth differences**
Shows how many plants fall into each growth range. All bars are to the right of 0, meaning every plant grew. The red dashed line is the average growth (3.00 cm).

**2. Box plot (before vs after)**
Each box shows where the middle half of the heights lie. The line inside the box is the median and the green triangle is the mean. The "after" box sits higher than the "before" box, so heights increased overall.

**3. Paired before-and-after chart**
One grey line for each plant, joining its before height to its after height. All 10 lines go upward. The thick red line shows the average. This graph is the best one to show why paired data is useful, because you can see each plant individually.

---

## 8. Why a paired t-test (and not another test)?

Because the same 10 plants are measured twice. The before and after values are linked.

If we had used 10 plants without compost and a different 10 plants with compost, the groups would be independent and we would use an independent (two-sample) t-test instead.

Using the paired test is better here because it removes the difference between plants (a naturally tall plant is tall in both measurements) and focuses only on the change.

---

## 9. What this project does NOT prove

Be very clear about this. Examiners like it when you know the limits.

1. **The data is simulated.** The strong result is because of how the numbers were written, not because real plants behaved this way.
2. **No causation.** Even with real data, a significant t-test does not prove compost caused the growth. There is no control group (plants that got no compost). Plants grow over time anyway, and watering, sunlight and weather can also change the result.
3. **Small sample.** 10 plants is small.
4. **For a real study** we would need real measurements, a control group, the same conditions for all plants, and ideally random assignment.

---

## 10. Two-minute speaking script

You can say this almost word for word.

> "Good morning. My project is called Plant Growth Before and After Compost. The aim is to check whether the average height of plants changes after adding compost.
>
> Since I did not have real plants, I created a simulated dataset of 10 plants with their heights before and after compost. I have clearly marked it as simulated everywhere, so the project demonstrates the method and does not prove anything about real compost.
>
> Because the same plants are measured twice, I used a paired t-test. My null hypothesis is that the average growth is zero, meaning compost has no effect. The alternative hypothesis is that the average growth is not zero. I used a two-tailed test at the 5% significance level.
>
> I used Python with NumPy for calculations, SciPy for the statistical test, and Matplotlib for graphs. I calculated the t-test manually using the formula and also with SciPy, and both gave the same result.
>
> The average height went from 13.29 cm to 16.29 cm, so the average growth is 3.00 cm. The t-statistic is 18.22 with 9 degrees of freedom, and the p-value is about 2 times 10 to the power minus 8. Since this is less than 0.05, we reject the null hypothesis.
>
> I also made three graphs: a histogram of growth, a box plot, and a paired chart, and they all show that every plant is taller after compost in this data.
>
> Finally, because the data is simulated and there is no control group, I cannot claim that compost causes plants to grow. The project shows how to do the analysis, and real data would be needed for real conclusions. Thank you."

---

## 11. Questions you may be asked, with answers

**Q1. What is a t-test?**
A test that checks whether an average is really different from some value (here 0) or whether the difference could just be random chance.

**Q2. What is a paired t-test?**
A t-test for two measurements on the same subjects, like before and after. It works on the difference for each subject.

**Q3. What are your hypotheses?**
H0: average growth is 0 (no effect). H1: average growth is not 0 (two-tailed).

**Q4. What is a p-value?**
The chance of getting a result as extreme as ours if H0 were true. A small p-value means the result is hard to explain by chance alone. Mine is about 2 x 10^-8.

**Q5. What does "5% significance level" mean?**
It is our cut-off. If p is below 0.05 we reject H0. It also means we accept a 5% risk of wrongly rejecting H0 when it is actually true.

**Q6. Why two-tailed?**
Compost could in theory make plants taller or shorter, and we did not want to assume the direction beforehand. Two-tailed checks for a change in either direction.

**Q7. What are degrees of freedom?**
n - 1. With 10 pairs, df = 9.

**Q8. Why `ddof=1`?**
It divides by n - 1 instead of n, giving the sample standard deviation. We use it because our 10 plants are only a sample of all plants.

**Q9. Why did you do the t-test manually and also with SciPy?**
To confirm that I understand the formula and that the library gives the same answer. The code has an `assert` that checks they match.

**Q10. Is your data real?**
No, it is simulated, and I have said so clearly. I created it because real measurements were not available. The method is real, and real data can be put in the same code.

**Q11. Does your result prove compost helps plants grow?**
No. The data is simulated, and there is no control group. Even with real data, a t-test shows a statistical difference, not a cause.

**Q12. Why is your p-value so small?**
Because I made the simulated growth values very consistent. Real data is usually more varied, which gives larger p-values.

**Q13. What if the p-value was 0.08?**
Then p is greater than 0.05, so we would fail to reject H0. That means we do not have enough evidence of a difference. It does not prove there is no difference.

**Q14. What does the confidence interval tell us?**
The true average growth is probably between 2.63 and 3.37 cm. Since 0 is not in this range, it agrees with rejecting H0.

**Q15. What is the Shapiro-Wilk test for?**
To check whether the growth values look roughly normal, which the t-test assumes. My p-value was 0.3366, so there was no evidence against normality. With 10 values it is only a rough check.

**Q16. What does the box plot show?**
The spread of heights before and after. The "after" box is higher, so heights increased.

**Q17. What would you do to make this a real study?**
Measure real plants, add a control group without compost, keep sunlight and watering the same, and use more plants.

**Q18. Which libraries did you use and why?**
NumPy for arrays and basic calculations, SciPy (`scipy.stats`) for the t-test and normality test, and Matplotlib (`pyplot`) for the graphs.

**Q19. How do you run your project?**
Upload the `.ipynb` file to Google Colab and click Runtime, then Run all. It can also be run in Jupyter Notebook.

---

## 12. Quick cheat sheet (revise this before presenting)

- Data: 10 plants, simulated, heights in cm
- Test: two-tailed paired t-test, alpha = 0.05
- H0: mean growth = 0. H1: mean growth is not 0
- Mean before = 13.29 cm, mean after = 16.29 cm
- Average growth = 3.00 cm (SD 0.52)
- t = 18.22, df = 9, critical t = 2.262
- p = 2.06 x 10^-8, which is less than 0.05, so reject H0
- 95% CI of growth: 2.63 to 3.37 cm
- Three graphs: histogram, box plot, paired chart
- Limits: simulated data, no control group, small sample, no proof of causation

## 13. Presentation tips

- Start with the one-line summary, then go through the notebook top to bottom.
- Say "simulated" early and clearly. It shows honesty and examiners appreciate it.
- Do not say "compost proves" or "compost causes". Say "in this simulated data, the average height after compost is significantly higher".
- If you do not know an answer, say what you do know in simple words. For example: "The p-value tells us how likely this result is by chance if there is no real effect."
- Run the notebook once before the demo (Runtime, Run all) so the outputs and graphs are ready.
