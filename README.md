# Metabolic Syndrome Prediction

## Demo

🔗 Try it: [MetSync App](https://metabolic-screener.streamlit.app/)

&nbsp;

<img width="853" height="480" alt="Metabolic+Syndrome+2" src="https://github.com/user-attachments/assets/49426f07-f4a3-4a07-aa1a-098d179d5aff" />

## Problem Statement
Metabolic Syndrome affects nearly 28% of adults worldwide, yet remains one of the most underdiagnosed conditions. This project uses machine learning to identify individuals likely to have Metabolic Syndrome from clinical and socioeconomic data,supporting faster and more informed clinical decision-making

<img width="1360" height="1040" alt="metabolic_syndrome" src="https://github.com/user-attachments/assets/e42b5db5-2be8-463e-be73-4df21d7d06a6" />

## Data 
For this dataset, there were 2401 rows and 15 columns.

| Variable Name | Description |
|---|---|
| `seqn` | Unique respondent sequence number (ID) |
| `Age` | Age of the respondent in years |
| `Sex` | Biological sex (`Male` / `Female`) |
| `Marital` | Marital status (`Single`, `Married`, etc.) |
| `Income` | Annual income in USD |
| `Race` | Self-reported race/ethnicity (`White`, `Black`, `Asian`, etc.) |
| `WaistCirc` | Waist circumference in centimeters |
| `BMI` | Body Mass Index |
| `Albuminuria` | Degree of albumin in urine (`0` = Normal, `1` = Microalbuminuria, `2` = Macroalbuminuria) |
| `UrAlbCr` | Urine albumin-to-creatinine ratio (mg/g) |
| `UricAcid` | Serum uric acid level (mg/dL) |
| `BloodGlucose` | Fasting blood glucose level (mg/dL) |
| `HDL` | HDL cholesterol level (mg/dL)|
| `Triglycerides` | Fasting triglyceride level (mg/dL)|
| `MetabolicSyndrome` | **Target variable** — Metabolic Syndrome diagnosis (`MetSyn` / `No MetSyn`) |

**Data Source:** This dataset is based on the NCEP ATP III diagnostic criteria. Available on [data.world](https://data.world/informatics-edu/metabolic-syndrome-prediction).


## Explanatory Analysis

<img width="1190" height="690" alt="Blood sugar" src="https://github.com/user-attachments/assets/9d84ca1b-dc78-423e-b2bc-e1e813c430a5" /> <br>

*Once fasting blood sugar crosses 100 mg/dL, the risk of Metabolic Syndrome more than triples — jumping from 14% to over 52%. A routine blood test isn't just a number; it's a critical early warning sign.*



<img width="1190" height="690" alt="waist" src="https://github.com/user-attachments/assets/e8d056d8-828e-4a7d-9252-3f427cac2ae7" /><br>

*As waist circumference grows, so does the risk - climbing from 2.8% below 80 cm to 73% above 120 cm. A waist size over 100 cm is where risk begins to escalate sharply.*


## Data preparation

- Imputed WaistCirc & BMI using a custom GroupedMedianImputer (median per Sex, Race group).  
- Imputed Income using global median; Marital using a constant value ("Missing").  
- Applied OrdinalEncoder to Albuminuria and OneHotEncoder to Sex, Race, and Marital.  
- Scaled all numerical features using RobustScaler to handle significant outliers. 

## Modeling

### Feature Engineering

- TG_HDL_Ratio — TG to HDL ratio, a strong insulin resistance indicator.
- Metabolic_Risk_Score — a composite score (0–6) based on clinical thresholds for blood glucose, triglycerides, HDL, and waist circumference (sex-adjusted).

### Feature Selection
- Applied RFECV to identify the most predictive features.

### Model

- Trained a voting ensemble (XGBoost + Random Forest) with threshold tuning.
- Achieved 88% accuracy and 90% recall on the target class (Metabolic Syndrome)
