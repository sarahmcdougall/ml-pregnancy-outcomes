# Predicting Adverse Pregnancy Outcomes with Machine Learning

## Project Overview
This project aims to predict 3 adverse pregnancy outcomes - **preeclampsia**, **preterm delivery**, and **obstretric hemorrhaging** - using **supervised machine learning models** trained on health and demographic data.

This repository contains the Jupyter Notebooks, external resources, and constructed dataframes used to construct machine learning models for prediction of adverse pregnancy outcomes using the [MIMIC-IV dataset](https://www.nature.com/articles/s41597-022-01899-x).

## Directory Structure
- `notebooks` - contains Jupyter Notebooks used for preprocessing, EDA, and model construction. Note that the notebooks have numbers appended to the end of their file names. The numbers represent the general order in which the notebooks should be run. While not all notebooks are dependent on the results of another, many of the notebooks do depend on the CSV output of previous notebooks.
- `final_dfs` - final dataframes used for model construction
- `resources` - external resources used for data pre-processing, filtering, and mapping

## Dataset and Sources
This project utilizes the open-source Multiparameter Intelligent Monitoring in Intensive Care (MIMIC)-IV dataset. The datset is a publicly available database sourced from the electronic health record (EHR) of the Beth Israel Deaconess Medical Center in Massachusetts.

The dataset contains data on a clinical cohort of patients that were admitted to the Emergency Department (ED) or an intensive care unit (ICU) between the years of 2008 and 2019. All patients are greater than 18 years of age and the patient records have been de-identified to abide by HIPAA regulations. The MIMIC-IV dataset takes on a relational structure and contains patient demographic data, health metrics, and mapping tables with the International Classification of Diseases (ICD) codes, Diagnosis Related Groups (DRGs), and the Healthcare Common Procedure Coding System (HCPCS).

## Methodology
### Data Extraction and Cleaning
- read data into Postgres
- filter data on pregnancy diagnosis and gender
- pre-process diagnosis, procedure, and medication codes - results in a truncated "root" representation of the original code
- handle outliers by measuring against clinically informed outlier values gathered in ["MIMIC-Extract: A Data Extraction, Preprocessing, and Representation Pipeline for MIMIC-III"](https://arxiv.org/pdf/1907.08322)

### Exploratory Data Analysis
- explore adverse outcomes by race, marital status, and other demographic factors
- explore common diagnoses and prescriptions for pregnant patients

### Model Selection and Training
For all classifiers:
- apply SMOTE to account for output imbalance
- apply stratified 5-fold cross-validation to ensure minority classes are represented
- evaluate via AUC and recall

Constructed models:
- AdaBoost
- Random Forest
- Long Short-Term Memory Network (LSTM)

## Results
- Binary LSTM model (predicting adverse outcome v. no adverse outcome) achieved **88.5%** AUC and **94%** recall.
- Multi-label LSTM model (predicts output labels for each adverse outcome) achieved **77%** AUC and **92%** recall.
- Binary AdaBoost model achieved **86%** recall and **88%** precision.
- The models tend to over-predict adverse outcomes (Type I error) compared to missing a diagnosis (Type II error).


## Relevant Resources
- [Physionet Page for MIMIC-IV v3.0](https://physionet.org/content/mimiciv/3.0/)
- [Nature article on MIMIC-IV](https://www.nature.com/articles/s41597-022-01899-x)
- [ICD-10 Diagnosis Repository](https://www.icd10data.com/ICD10CM/Codes)
- [ICD-9 Diagnosis Repository](https://www.cms.gov/medicare/coordination-benefits-recovery/overview/icd-code-lists)
- [NDC for Medications](https://www.fda.gov/drugs/drug-approvals-and-databases/national-drug-code-directory)
- [ICD-10 Procedure Code Repository](https://www.icd10data.com/ICD10PCS/Codes)
- [ICD-9-PCS to ICD-10-PCS Mapping Overview](https://www.nber.org/research/data/icd-9-cm-and-icd-10-cm-and-icd-10-pcs-crosswalk-or-general-equivalence-mappings)
- ["MIMIC-Extract: A Data Extraction, Preprocessing, and Representation Pipeline for MIMIC-III"](https://arxiv.org/pdf/1907.08322)
- ["An Extensive Data Processing Pipeline for MIMIC-IV"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9854277/)
- ["Patient Subtyping via Time-Aware LSTM Networks"](https://biometrics.cse.msu.edu/Publications/MachineLearning/Baytasetal_PatientSubtypingViaTimeAwareLSTMNetworks.pdf)
