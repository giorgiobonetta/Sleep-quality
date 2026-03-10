# Sleep-quality
Dottor Bonetta, ti preparo un **README.md professionale per GitHub** per il progetto che hai caricato (LMDD – Linear Models for Dependent Data). È scritto in stile **accademico / data science portfolio**, perfetto per GitHub o CV.

---

# Modeling Sleep Quality Using Mixed Models for Ordinal Dependent Data

## Project Overview

This project investigates how **lifestyle factors and demographic characteristics influence sleep quality**, using statistical models designed for **clustered and ordinal data**.

The analysis focuses on a dataset where the response variable **Quality of Sleep** is measured on an **ordinal scale** and observations are grouped by **occupation**. Because individuals within the same profession share similar working conditions and lifestyle constraints, the data exhibit **intra-group dependence**, which violates the independence assumptions of standard regression models.

To address this issue, we compare several modeling strategies:

* Linear Regression (baseline)
* Linear Mixed Models (random intercept and random slope)
* Cumulative Link Mixed Model (CLMM) for ordinal outcomes

The project highlights the **importance of hierarchical modeling when analyzing grouped observational data**. 

---

# Authors

* Giorgio Bonetta
* Maximilian Brunner
* Simon Derleth

Course: **Linear Models for Dependent Data**
Program: MSc in Statistics
Institution: **University of Geneva – Geneva School of Economics and Management**
Lecturer: Romain Pic
Semester: Fall 2025 

---

# Research Question

The project investigates:

> How do lifestyle behaviours (sleep duration, physical activity, daily steps, stress level) influence sleep quality compared to demographic factors (gender, age), and how does the effect of stress vary across occupational groups?

The analysis accounts for:

* **Clustered data structure** (occupation groups)
* **Ordinal response variable**
* **Heterogeneity across professions**

---

# Dataset

The study uses the **Sleep Health and Lifestyle dataset**, a synthetic dataset designed to reflect realistic relationships between sleep behavior and health indicators.

### Dataset characteristics

* **374 individuals**
* **13 variables**

### Main variables

| Variable                | Type        | Description                   |
| ----------------------- | ----------- | ----------------------------- |
| Gender                  | Categorical | Male / Female                 |
| Age                     | Continuous  | Centered and scaled           |
| Occupation              | Categorical | 11 occupational groups        |
| Sleep Duration          | Continuous  | Hours of sleep                |
| Physical Activity Level | Continuous  | Activity score                |
| Stress Level            | Continuous  | Self-reported stress          |
| Daily Steps             | Continuous  | Steps per day                 |
| Heart Rate              | Continuous  | Resting heart rate            |
| BMI Category            | Categorical | Weight categories             |
| Sleep Disorder          | Categorical | None / Apnea                  |
| Quality of Sleep        | Ordinal     | Response variable (4–9 scale) |

The **cluster variable is occupation**, which introduces dependence between observations within the same professional group. 

---

# Methodology

The analysis follows a **progressive modeling framework** to illustrate the limitations of standard models and the advantages of hierarchical approaches.

## 1. Linear Regression Model

A standard multiple regression model is first estimated:

[
QualityOfSleep_i = \beta_0 + \beta_1 Gender_i + \beta_2 Age_i + \dots + \epsilon_i
]

However, this model suffers from several issues:

* residual non-normality
* violation of homoskedasticity
* ignored occupational clustering
* discretization due to ordinal outcome

These limitations motivate the use of **mixed-effects models**.

---

## 2. Linear Mixed Model (Random Intercept)

To account for the hierarchical structure, we estimate:

[
QualityOfSleep_{ij} = \beta X_{ij} + u_{0j} + \epsilon_{ij}
]

Where:

* ( i ) = individuals
* ( j ) = occupation groups
* ( u_{0j} ) = occupation-level random intercept

This model captures **baseline differences in sleep quality across professions**.

---

## 3. Linear Mixed Model (Random Slope)

The model is extended to allow **stress effects to vary by occupation**:

[
QualityOfSleep_{ij} = \beta X_{ij} + u_{0j} + u_{1j} Stress_{ij} + \epsilon_{ij}
]

This specification allows the relationship between stress and sleep quality to differ across occupations.

The results show:

* reduced residual variance
* improved model diagnostics
* substantial heterogeneity in stress sensitivity across professions.

---

## 4. Cumulative Link Mixed Model (CLMM)

Because the response variable is ordinal, we estimate a **Cumulative Link Mixed Model**, which:

* respects the ordered nature of the response
* accounts for group-level effects

However, the model may experience **convergence issues in finite samples**, especially with unbalanced group sizes.

---

## 5. Monte Carlo Simulation

A Monte Carlo study evaluates:

* model robustness
* convergence properties
* reliability of parameter estimates

This analysis shows that:

* mixed models significantly improve model performance
* CLMM is theoretically correct but may fail to converge under certain data conditions.

---

# Key Findings

The main empirical results are:

* **Stress level** is the strongest negative predictor of sleep quality.
* **Physical activity**, **age**, and **gender** show positive associations.
* Ignoring clustering leads to **biased standard errors and misleading significance**.
* Mixed models successfully capture **occupation-level heterogeneity**.
* Random slope models reveal **substantial variation in stress sensitivity across professions**.

---

# Technologies Used

* **R**
* lme4
* ordinal
* ggplot2
* dplyr
* RMarkdown
  
---

# Key Statistical Concepts

This project illustrates several advanced statistical topics:

* Hierarchical modeling
* Mixed-effects models
* Random intercept vs random slope
* Ordinal regression
* Clustered data structures
* Monte Carlo simulation
* Diagnostic analysis

---

# References

* Laird & Ware (1982) – Random Effects Models
* Gelman & Hill (2007) – Data Analysis Using Regression and Multilevel Models
* Halekoh & Højsgaard (2014) – Parametric bootstrap for mixed models
* Fox & Monette (1992) – Generalized Variance Inflation Factor
