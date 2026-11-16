# Who Will Take Part, and When? Predicting Student Participation at RIT

**Team 9 · AI-Powered Data Insight Internship · Excelerate**

An end-to-end data analytics project on 8,558 student applications to 22 learning opportunities at the Rochester Institute of Technology (RIT). We cleaned the data, explored participation patterns, trained prediction models and turned the results into recommendations for program managers.

---

## The Problem

Program managers need to know **which learning opportunities attract and keep student participation**, **when demand peaks**, and **which applications are likely to end in participation**. The raw dataset could not answer this directly: it had text-formatted and day/month-swapped dates, corrupted characters, no learner ID and no ready-made participation label.

Our goals:

1. Understand and clean the dataset, and document its quality.
2. Find trends by quarter, category and signup cohort.
3. Build models that estimate the probability that an application ends in participation.
4. Recommend actions and KPIs based on evidence.

## The Dataset

- **8,558 application records** (one row per application, not per learner; there is no learner ID)
- **16 original columns**, extended to **36 columns** with 20 derived features in Week 2
- **22 opportunities** (23 IDs) in 5 categories: Internship, Course, Event, Competition, Engagement
- Apply dates: 5 Oct 2022 to 10 Apr 2024 · Signup dates: 5 Jan 2023 to 9 Apr 2024
- Students from 70 countries
- **Target label:** `Participated` = Started, Team Allocated or Rewards Award. `Not Participated` = Rejected, Dropped Out or Withdraw. Applied and Waitlisted records are unresolved.

> The dataset contains personal information (names, dates of birth, institutions), so it is **not included in this repository**.

## What We Did

| Week | Stage | What we did |
|---|---|---|
| 1 | **Understand** | Cleaned the data (fixed 16,150 day/month-swapped dates, restored 48 corrupted text cells, standardised text), wrote a data dictionary, ran quality and outlier checks, and analysed baseline participation. |
| 2 | **Explore** | Built 20 new features (quarter, month, weekday, weekend, lead time, age group and more), then ran quarterly trend, category, cohort, learner-profile and anomaly analysis with charts. Added indicative baseline forecasts. |
| 3 | **Predict** | Trained and compared three models (Logistic Regression, Random Forest, Gradient Boosting) with grouped cross-validation, produced participation probabilities and opportunity rankings, and built a quarterly forecast. |
| 4 | **Recommend** | Presented findings, recommendations, KPIs and business impact in the final presentation. |

## Key Findings

- **Demand is concentrated.** 2024 Q1 holds 4,785 applications (55.9% of the dataset). January–February applications grew from 62 in 2023 to 4,401 in 2024. With one full year of data, this cannot be confirmed as seasonal.
- **Two very different pathways.** Courses, events, competitions and engagement activities lead to participation in about 99% of resolved applications. Internships lead to participation in about 22%.
- **Internships are the bottleneck.** They are 63% of all applications and account for all 3,569 rejections and 613 of the 617 dropouts.
- **The overall fall in participation is mostly a mix effect.** Observed participation drops from 96% (2023 Q2) to 36% (2024 Q1) because internships grow from 5% to 73% of applications, not because learners lose interest.
- **One programme changed behaviour.** Health Care Management allocated about 80% of applicants in 2023 Q3–Q4, then none from early 2024.
- **Weak signals.** Country, gender, age and weekend effects are small or mostly explained by category mix.

## Models and Results

- **Validation:** 5-fold StratifiedGroupKFold, grouped by opportunity, so every fold is tested on opportunities the model has never seen.
- **Selected model: Random Forest**: F1 0.830, ROC-AUC 0.897, accuracy 85.1%.
- **What drives the prediction:** opportunity category. A simple category-only rule scores almost the same F1 (0.829), so the model's added value is in ranking and probabilities.
- **Limit:** within internships the model has little skill (ROC-AUC 0.65, recall 11%). Learner details alone cannot explain why one internship selects more applicants than another.
- **Forecast:** the next peak is expected in Q1, about 4,785 applications and about 1,861 expected participants (planning band 3,589 to 5,981). This is a planning range from one yearly cycle, not a validated forecast.

## Recommendations

1. Investigate why Health Care Management stopped allocating applicants in 2024.
2. Plan review capacity for the Q1 surge.
3. Clear the 214 pending applications (all 55 AI Ethics Challenge records are still "Applied").
4. Promote high-participation programmes with fast growth.
5. Collect richer data: seats, deadlines, selection rules and a stable learner ID.

## Deliverables

| File | Description |
|---|---|
| `Data_Understanding_Report.docx` | Week 1: data dictionary, cleaning, quality checks, descriptive statistics, outliers |
| `Cohort_Analysis_with_Visual_Insights.docx` | Week 2: feature engineering, quarterly, category and cohort analysis, anomalies |
| `Trained_Models_and_Prediction_Report.docx` | Week 3: models, evaluation, probabilities, ranking, forecast |
| `Final_Presentation___Program_Insights_Report.pptx` | Week 4: final presentation with recommendations, KPIs and impact |

## Tools

Python (pandas, NumPy, matplotlib, seaborn, scikit-learn), Excel and Google Sheets, Google Colab, Power BI, R (diagnostic charts), SQL.

**AI tools used:** Claude (data cleaning, report compilation, recomputing and checking figures), ChatGPT (coding help, troubleshooting, report wording) and Gemini (code refinement, table formatting). Every AI-assisted figure was checked against the data, and AI use is documented in each report.

## Limitations

- Rows are applications, not learners, so repeat behaviour cannot be tracked.
- The target is a status-based grouping, not a confirmed completion measure.
- The data covers one full year (2023) plus part of 2022 and 2024, so seasonality and forecasts cannot be validated.
- The Week 1 day/month date correction is inferred from the data and is not confirmed by the data owner.
- Seats, applicant counts and selection rules are unknown, so individual internship outcomes cannot be predicted well.
- Scores are for planning, not for decisions about individual learners.

## Other Contributors

Ghufran Khan, Victor Thompson, Khadija Kamal, Nour Ahmed, Kamoru Olayemi Raji, Oladosu Rophiat

---

*Built as part of the AI-Powered Data Insight Internship with Excelerate.*
