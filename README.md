# HR-Analytics-at-ScaleneWorks
HR Analytics at ScaleneWorks

# HR Analytics at ScaleneWorks — Predicting Candidate Renege

## 📌 Project Overview

This project analyzes the **HR Analytics at ScaleneWorks** case study and uses Machine Learning to predict whether a candidate who has accepted a job offer will eventually **join the organization or renege on the offer**.

The project follows an end-to-end Machine Learning workflow, including data cleaning, exploratory data analysis, preprocessing, classification model building, model evaluation, feature importance analysis, and business recommendations.

The objective is not only to build an accurate predictive model but also to understand the **key factors influencing candidate joining behaviour** and translate the findings into actionable HR strategies.

---

## 🎯 Business Problem

ScaleneWorks faces a major recruitment challenge: candidates may accept an offer but later decide not to join the organization.

This creates:

* Additional recruitment costs
* Wasted HR and management effort
* Delays in workforce planning
* Difficulty in meeting project staffing requirements
* Potential loss of quality talent

The case study highlights that for a client rolling out 12,000 offers annually, a 30% renege rate could result in approximately **3,600 candidates not joining** and around **54,000 man-hours of recruitment effort being wasted**.

Therefore, the key business question is:

> **Which candidates are likely to not join the company after accepting an offer, and what factors drive that decision?**

---

## 📊 Dataset

The dataset contains **12,333 candidate records and 17 columns** before cleaning.

Each record represents a candidate who received and accepted a job offer, along with information about the candidate, compensation, recruitment process, and final joining status.

### Important Variables

| Variable                  | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| DOJ Extended              | Whether the joining date was extended                 |
| Duration to Accept Offer  | Number of days taken to accept the offer              |
| Notice Period             | Notice period at the candidate's current organization |
| Offered Band              | Job grade/band offered                                |
| % Hike Expected           | Salary hike expected by the candidate                 |
| % Hike Offered            | Salary hike offered by the company                    |
| % Difference CTC          | Difference between expected and offered hike          |
| Joining Bonus             | Whether a joining bonus was offered                   |
| Candidate Relocate Actual | Whether relocation was required                       |
| Gender                    | Candidate gender                                      |
| Candidate Source          | Direct, Agency, or Employee Referral                  |
| REX in Years              | Relevant work experience                              |
| LOB                       | Line of Business                                      |
| Location                  | Job location                                          |
| Age                       | Candidate age                                         |
| Status                    | Target variable — Joined / Not Joined                 |

The `Candidate Ref` column was removed because it is only a unique identifier and does not provide predictive value.

---

## 🔎 Project Workflow

```text
Case Study
     ↓
Data Loading
     ↓
Data Cleaning
     ↓
Exploratory Data Analysis
     ↓
Data Preprocessing
     ↓
Train-Test Split
     ↓
Model Building
     ↓
Model Evaluation
     ↓
Feature Importance
     ↓
Business Insights
     ↓
HR Recommendations
```

---

## 🧹 Data Cleaning

The dataset was checked for missing values and duplicate records.

Missing values were found primarily in:

* Duration to accept offer
* % Hike Expected in CTC
* % Hike Offered in CTC
* % Difference CTC

### Treatment

* Numerical missing values → **Mean imputation**
* Categorical missing values → **Mode imputation**
* Duplicate records → **No duplicate records found**
* Candidate Ref → **Dropped before modelling**

After cleaning, the dataset contained **zero missing values**.

---

## 📈 Exploratory Data Analysis

Several aspects of the dataset were explored to understand candidate behaviour.

### Target Distribution

* **Joined:** 8,725 candidates — 70.75%
* **Not Joined:** 3,608 candidates — 29.25%

This means that almost **3 out of every 10 candidates who accepted an offer did not eventually join**.

### Candidate Source

* Direct: 7,075 candidates
* Agency: 3,170 candidates
* Employee Referral: 2,088 candidates

### Other EDA Areas

The analysis also examined:

* Gender distribution
* Joining-date extensions
* Joining bonuses
* Notice period
* Age distribution
* Correlation between numerical variables
* Relationship between candidate characteristics and joining status

---

## ⚙️ Data Preprocessing

Categorical variables were converted into numerical values using **Label Encoding**.

The target variable was defined as:

```text
0 → Joined
1 → Not Joined
```

The dataset was divided into:

```text
80% → Training Data
20% → Testing Data
```

With:

* Training records: **9,866**
* Testing records: **2,467**
* Random state: **42**

---

## 🤖 Machine Learning Models

Three classification algorithms were implemented and compared.

### 1. Logistic Regression

Used as the baseline classification model.

**Accuracy:** 74.83%

The model performed well in identifying candidates who joined but had relatively poor recall for candidates who did not join.

---

### 2. Decision Tree

A non-linear classification model capable of capturing interactions between different variables.

**Accuracy:** 78.03%

The Decision Tree significantly improved the recall of the **Not Joined** class compared with Logistic Regression.

---

### 3. Random Forest

An ensemble model consisting of multiple decision trees.

**Accuracy:** 83.66%

Random Forest produced the strongest overall performance among the three models.

---

## 🏆 Model Comparison

| Model               |   Accuracy | F1-Score — Not Joined |
| ------------------- | ---------: | --------------------: |
| Logistic Regression |     74.83% |                  0.45 |
| Decision Tree       |     78.03% |                  0.63 |
| **Random Forest**   | **83.66%** |              **0.67** |

### Final Model

**Random Forest** was selected as the final model because it achieved the highest accuracy and provided a better overall balance between identifying candidates who join and candidates who renege.

For the **Not Joined** class, Random Forest achieved:

* Precision: **0.83**
* Recall: **0.56**
* F1-score: **0.67**

---

## 🔑 Key Drivers of Candidate Renege

The Random Forest feature importance analysis identified the following major drivers:

| Rank | Feature                  | Importance |
| ---: | ------------------------ | ---------: |
|    1 | Duration to Accept Offer |     19.22% |
|    2 | % Difference CTC         |     11.94% |
|    3 | % Hike Offered in CTC    |     10.54% |
|    4 | % Hike Expected in CTC   |      9.81% |
|    5 | Notice Period            |      7.16% |
|    6 | Age                      |      6.69% |
|    7 | REX in Years             |      6.51% |
|    8 | Candidate Relocation     |      6.22% |

The strongest individual predictor was **Duration to Accept Offer**.

Salary-related variables were also highly influential, with expected hike, offered hike, and CTC difference collectively accounting for a substantial portion of feature importance.

---

## 💡 Business Insights

### 1. Slow offer acceptance is a warning signal

Candidates who take longer to accept an offer may be more likely to reconsider the opportunity or explore alternatives.

### 2. Compensation alignment matters

The gap between what candidates expect and what the organization offers is an important factor influencing joining behaviour.

### 3. Notice period can increase risk

Candidates with longer notice periods have more time to receive counter-offers or reconsider their decision.

### 4. Joining bonus alone has limited influence

The model indicates that joining bonus has relatively low feature importance compared with factors such as offer acceptance time and compensation.

### 5. Predictive analytics can improve HR intervention

Instead of treating every accepted offer equally, HR teams can prioritize candidates with higher predicted renege risk.

---

## 🎯 Recommendations

Based on the analysis, the following actions can be considered:

1. **Flag candidates with unusually long offer acceptance times** for proactive HR engagement.

2. **Improve compensation alignment** by comparing candidate expectations with the proposed CTC.

3. **Maintain structured communication** with candidates serving longer notice periods.

4. **Use the Random Forest risk prediction** to prioritize retention and follow-up efforts.

5. **Reevaluate joining bonuses** as a standalone retention strategy because of their relatively low predictive importance.

---

## 🚀 Future Scope

The project can be further improved by:

* Applying **SMOTE** or class-weight balancing to improve minority-class recall.
* Performing **hyperparameter tuning** using GridSearchCV or RandomizedSearchCV.
* Testing advanced models such as **XGBoost**.
* Adding additional features such as counter-offer history and communication frequency.
* Developing a dashboard for HR teams to monitor candidate risk.
* Deploying the model as an HR decision-support application.

---

## 🛠️ Tools & Technologies

### Programming

* Python

### Data Analysis

* pandas
* NumPy

### Data Visualization

* Matplotlib
* Seaborn

### Machine Learning

* Scikit-learn

### Algorithms

* Logistic Regression
* Decision Tree
* Random Forest

### Evaluation

* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix
* Feature Importance

---

## 📚 Case Study Reference

**HR Analytics at ScaleneWorks — Behavioral Modeling to Predict Renege**

Case: **IMB551**

Indian Institute of Management Bangalore



## ⭐ Key Takeaway

The project demonstrates how Machine Learning can transform a recruitment problem into a **data-driven HR decision-support system**.

The Random Forest model achieved **83.66% accuracy**, while the feature analysis highlighted **offer acceptance duration and compensation-related factors** as the most important predictors of candidate joining behaviour.

The overall objective is to help HR teams identify high-risk candidates earlier and take targeted actions to reduce offer reneges and improve recruitment efficiency.
