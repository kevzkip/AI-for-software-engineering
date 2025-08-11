# AI Development Workflow Assignment

## Part 1: Short Answer Questions (30 points)

### 1. Problem Definition (6 points)
**Hypothetical Problem**: Predicting student dropout rates in online education platforms

**Objectives**:
1. Identify at-risk students 3 months before potential dropout
2. Recommend personalized interventions
3. Reduce dropout rates by 15% within one academic year

**Stakeholders**:
1. University administrators
2. Student success counselors

**KPI**: Precision@K (Top 100 predictions) - Measures how many of our top predictions actually drop out

### 2. Data Collection & Preprocessing (8 points)
**Data Sources**:
1. Learning Management System (LMS) interaction logs
2. Student demographic and academic history

**Potential Bias**: Underrepresentation of non-traditional students in training data

**Preprocessing Steps**:
1. Handle missing grades using multiple imputation
2. Normalize engagement metrics (clicks, time spent) across courses
3. Temporal feature engineering (create rolling 30-day activity windows)

### 3. Model Development (8 points)
**Chosen Model**: Gradient Boosted Decision Trees (XGBoost)

**Justification**:
- Handles mixed data types well
- Provides feature importance
- Robust to outliers

**Data Splitting**:
- 60% training (chronological first 60% of academic terms)
- 20% validation (next 20%)
- 20% test (most recent 20%)

**Hyperparameters to Tune**:
1. `max_depth`: Controls model complexity to prevent overfitting
2. `learning_rate`: Balances training speed and performance

### 4. Evaluation & Deployment (8 points)
**Evaluation Metrics**:
1. Recall: Critical to identify most at-risk students (false negatives costly)
2. Precision-Recall AUC: Better than ROC for imbalanced data

**Concept Drift Monitoring**:
- Track feature distribution shifts monthly using Kolmogorov-Smirnov tests
- Monitor prediction stability via weekly inference on held-out samples

**Deployment Challenge**: Real-time feature generation from LMS logs requires streaming pipeline

## Part 2: Case Study Application (40 points)

### Problem Scope (5 points)
**Problem**: Predict 30-day readmission risk for cardiac patients  
**Objectives**:
1. Flag high-risk patients before discharge
2. Reduce readmissions by 20%
3. Prioritize resource allocation

**Stakeholders**:
1. Hospital administrators
2. Care coordination teams
3. Insurance providers

### Data Strategy (10 points)
**Data Sources**:
1. Electronic Health Records (EHRs)
2. Socioeconomic data from public health databases

**Ethical Concerns**:
1. Privacy: PHI handling requires HIPAA-compliant pipelines
2. Fairness: Potential bias against underserved populations

**Preprocessing Pipeline**:
```mermaid
graph TD
    A[Raw EHR] --> B[De-identification]
    B --> C[Feature Extraction]
    C --> D[Impute Missing Labs]
    D --> E[Create Temporal Features]
    E --> F[Normalize Clinical Values]
