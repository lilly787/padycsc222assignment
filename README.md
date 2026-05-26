# EduSafe: Student Dropout Prediction & Intervention System

[![Streamlit App](https://img.shields.io/badge/Streamlit-App-FF4B4B?style=for-the-badge&logo=streamlit)](https://edusafe-a-atl7rvyerbdxmqgwct2pfo.streamlit.app/)
[![YouTube Demo](https://img.shields.io/badge/YouTube-Demo-FF0000?style=for-the-badge&logo=youtube)](https://youtube.com/shorts/BzfoCSF6pk8?si=liGhBuDTDICmbgAL)

---

## 🎓 Academic Submission Details
* **Course Title:** CSC 322 / CSC 222 (Systems Analysis & Machine Learning Assignment)
* **Project Title:** EduSafe: Student Dropout Prediction & Intervention System
* **Submitted By:** [Your Name] 
* **Matriculation Number:** [Your Matric Number]
* **Department:** Computer Science
* **Submitted To:** [Lecturer's Name]
* **Date:** May 2026

---

## 📌 Project Overview
EduSafe is an end-to-end Machine Learning-powered system designed to predict student dropout rates and provide explainable risk indicators. By identifying at-risk students early in their academic journey, institutions can deploy timely interventions (counseling, financial aid, or academic tutoring) to improve student retention and graduation rates.

This repository contains the data analysis, machine learning models, and the code for the interactive Streamlit web application.

* **Live Web App:** [EduSafe Streamlit Platform](https://edusafe-a-atl7rvyerbdxmqgwct2pfo.streamlit.app/)
* **Video Demonstration:** [YouTube Project Short](https://youtube.com/shorts/BzfoCSF6pk8?si=liGhBuDTDICmbgAL)

---

## 🛠️ Feature Engineering & Preprocessing
Using a real-world student dataset, the raw columns were preprocessed and transformed into highly informative features to capture academic performance and socioeconomic stability:

1. **Target Variable Binarization:** The dataset's original three-class target was converted into a binary classification target where:
   - `1` represents **Dropout** (High Risk)
   - `0` represents **Stayed** (Graduate/Enrolled)
2. **Academic GPA Index (`gpa`):** Calculated as the average grade of the 1st and 2nd semesters:
   $$\text{GPA} = \frac{\text{Curricular units 1st sem (grade)} + \text{Curricular units 2nd sem (grade)}}{2}$$
3. **Engagement Index (`engagement`):** Quantifies student academic participation by averaging enrolled and approved units across both semesters:
   $$\text{Engagement} = \frac{\text{Enrolled}_{\text{sem1}} + \text{Enrolled}_{\text{sem2}} + \text{Approved}_{\text{sem1}} + \text{Approved}_{\text{sem2}}}{4}$$
4. **Socio-Economic Income Proxy (`income_proxy`):** Derived from scholarship status and debtor status:
   $$\text{Income Proxy} = (\text{Scholarship holder} \times 2) + (1 - \text{Debtor})$$
5. **Risk Flags:**
   - **Low GPA Flag:** Active if GPA falls below 5.
   - **Low Engagement Flag:** Active if Course Engagement falls below 3.
   - **Risk Score:** Combined sum of both flags (Scale of 0 to 2) representing the compound academic risk.

---

## 📊 Machine Learning Models & Performance
We trained and evaluated three classification models on a stratified 80-20 train-test split (3,539 training samples, 885 testing samples). 

### Model Comparison Table

| Machine Learning Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Logistic Regression** | 83.62% | 83.25% | 61.27% | 70.59% | 0.8763 |
| **Random Forest** (Selected) | 82.03% | 77.53% | 61.97% | 68.88% | **0.8765** |
| **XGBoost** | 81.24% | 74.18% | 63.73% | 68.56% | 0.8486 |

* **Selected Model:** **Random Forest Classifier** was selected due to its superior ROC-AUC score (**0.8765**) and stable recall, ensuring that non-linear relationships and interactions between socioeconomic factors and academic performance are captured effectively.

---

## 🔍 Model Interpretability (LIME Integration)
To move beyond black-box predictions, EduSafe incorporates **LIME (Local Interpretable Model-agnostic Explanations)**. This allows academic advisors to see exactly *why* a specific student is flagged as high-risk.

For example, for a student predicted to drop out with a **62.0% probability**, LIME decomposes the decision into specific contributing weights:
* **gpa <= 10.92** (Strongly pushes towards dropout) ❌
* **engagement <= 4.00** (Pushes towards dropout) ❌
* **income_proxy <= 1.00** (Pushes towards dropout) ❌
* **Age at enrollment <= 19.00** (Pushes away from dropout) ✅

---

## 💻 Streamlit Web Application
The deployed Streamlit app provides an intuitive dashboard for administrators and lecturers to input student metrics and receive instant risk classifications.

### Key Features:
- **Interactive Sliders:** For GPA, Age, Unemployment Rate, and Engagement.
- **Toggles:** For Gender, Daytime/Evening Attendance, Scholarship Holder, and Debtor status.
- **Real-Time Predictions:** Instant feedback with probability meters showing the likelihood of dropout vs. graduation.
- **Hosted Cloud Link:** [EduSafe Web App](https://edusafe-a-atl7rvyerbdxmqgwct2pfo.streamlit.app/)

---

## 🚀 How to Run Locally

### 1. Clone the Repository
```bash
git clone https://github.com/lilly787/padycsc222assignment.git
cd padycsc222assignment
```

### 2. Install Dependencies
Ensure you have Python 3.8+ installed. Run:
```bash
pip install pandas numpy scikit-learn xgboost lime streamlit matplotlib seaborn
```

### 3. Run the Jupyter Notebook (Model Development)
To view the EDA, feature engineering, model training, and LIME explanation code:
```bash
jupyter notebook assignment.ipynb
```

### 4. Launch the Streamlit App
If you have the `app.py` script locally:
```bash
streamlit run app.py
```
*(If the repository only contains notebooks, the web application runs directly from the Streamlit Cloud deployment linked above).*
