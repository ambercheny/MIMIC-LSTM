# MIMIC-LSTM
Topic: An LSTM prediction on ICU stay length based on patient glycemic control
Database: https://physionet.org/content/glucose-management-mimic/1.0.1/ (1)

### Aim of the final report
To predict ICU stay days based on patient demographics, glucose readings and insulin treatments.

### Database and preprocessing
For full code of data preprocessing, see Python Notebook, Preprocess.ipynb.

MIMIC-III is a freely accessible critical care database, comprised of clinical data from patients admitted to Beth Israel Deaconess Medical Center in Boston, Massachusetts. Adult patients (aged 16 years or above) admitted to critical care units between 2001 and 2012 and neonates admitted between 2001 and 2008 were included (2)

For this project, database Curated Data for Describing Blood Glucose Management in the Intensive Care Unit was used. The inclusion criteria for data curation process was published in February 2021 (1). The resulting database is uploaded online on Physionet (https://physionet.org/content/glucose-management- mimic/1.0.1/). Patients with glucose readings and insulin treatments were included. The final dataset glucose_insulin_pair.csv is used for this final project. Additionally, other attributes (ADMISSIONS_TYPE, GENDER, DOB, ICD9_CODE) are obtained from linking with MIMIC-III v.1.4 database directly (2, 3, 4).

### Exploratory data analysis
For full code of exploratory data analysis, see Python Notebook, EDA.ipynb.

### Model development and testing
For full code of model development and training, see Python Notebook, DNN.ipynb.

### Result interpretation
For Model2, data with Repeated variable and dummy-variable transformation of categorical variables outperformed all the other models. Although this is compatible to the expectation since Repeated indicates the relationship between glucose readings and insulin treatments. However, the difference is not significant (AUROC 0.973 for with repeat, AUROC 0.969 for without repeat). Feature importance or statistical models are needed to explain the result.

For Model2-adult and Model2-elderly, both models performed worse than Model2, implying that despite sample size, age could be a significant factor contributing to the length of ICU stay. Furthermore, Model2- elderly performed slightly worse than Model2-adult.

Specificity in all model was better than sensitivity. This is possibly due to the imbalance of data (positive outcome represents about 40% of the entire sample) (Table 3). However, stratification was used for train, validation and test set splitting. Model adjustment may be needed to address sensitivity improvement.

### Future direction
1. Apply statistical model s (e.g. logistic regression) to 1) obtain covariate estimates, 2) compare with the
deep learning model.
2. Implement SHAP value to explain the importance of each variable. (I have tried and googled many
documents regarding SHAP implementation. However, since the model used LSTM and masking, in my
knowledge, current SHAP package does not support this model structure.)
3. Include more variables (information), such as clinical assessment score (e.g SOFA score), comorbidities,
and other medications.
4. Current epoch number is only 50. More epochs training may lead to better models.

### Reference
1. Robles Arevalo A, Maley JH, Baker L, da Silva Vieira SM, da Costa Sousa JM, Finkelstein S, et al. Data-driven curation process for describing the blood glucose management in the intensive care unit. Sci Data. 2021;8(1):80.
2. Johnson AE, Pollard TJ, Shen L, Lehman LW, Feng M, Ghassemi M, et al. MIMIC-III, a freely accessible critical care database. Sci Data. 2016;3:160035.
3. Johnson, A., Pollard, T., & Mark, R. (2019). MIMIC-III Clinical Database Demo (version 1.4). PhysioNet. https://doi.org/10.13026/C2HM2Q.
4. Goldberger A, Amaral L, Glass L, Hausdorff J, Ivanov PC, Mark R, Mietus JE, Moody GB, Peng CK, Stanley HE. PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals. Circulation [Online]. 101 (23), pp. e215–e220.