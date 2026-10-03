&#x20;**Impact of Missing Clinical Data and Median Imputation on a Diabetes Prediction Model**



&#x20;**Project Overview**



Healthcare data are often incomplete. Clinical measurements may be missing because a test was not performed, documentation was incomplete, information was unavailable at the time of data collection, or data were not entered into a health information system. Missing information can create challenges when clinical data are used for statistical analysis or predictive modelling.



This project explores the effect of missing clinical data and median imputation on the performance of a diabetes prediction model. It uses a dataset containing 583 adult records with demographic, lifestyle, cardiovascular, laboratory, and diabetes outcome variables.



The project first examines the dataset through exploratory data analysis and statistical comparisons. A logistic regression model is then trained and evaluated using the complete dataset to establish baseline performance.



A controlled missing-data experiment is subsequently performed. Approximately 10% of values are randomly removed from five selected clinical variables: BMI, glucose, HbA1c, systolic blood pressure, and diastolic blood pressure. Median imputation is then used to replace the missing values before fitting the same type of logistic regression model.



Performance of the clean-data model and the missing-data/imputation model is compared using accuracy, sensitivity, specificity, positive predictive value (PPV), negative predictive value (NPV), and ROC-AUC.



The purpose of the project is not to develop or validate a clinical diagnostic system. Instead, it is an educational health data science project demonstrating how data quality, missing values, preprocessing decisions, and choice of evaluation metrics can influence the interpretation of predictive models.





&#x20;**Research Question**



*How does introducing approximately 10% random missingness in selected clinical variables and applying median imputation affect the performance of a logistic regression model for diabetes prediction?*



&#x20;**Project Objectives**



The project was designed to:



1\. Inspect and explore a clinical-style dataset containing demographic, lifestyle, cardiovascular, and laboratory variables.



2\. Examine the distribution of the diabetes outcome.



3\. Compare selected characteristics between records classified as diabetes and non-diabetes.



4\. Perform statistical comparisons of glucose and HbA1c between the two outcome groups.



5\. Develop a baseline logistic regression model using complete data.



6\. Evaluate the model using multiple classification metrics rather than relying only on overall accuracy.



7\. Simulate a controlled data-quality problem by introducing missing values into selected clinical variables.



8\. Apply median imputation using a modelling pipeline designed to prevent data leakage.



9\. Train and evaluate the logistic regression model under the missing-data condition.



10\. Compare performance before and after the missing-data experiment.



11\. Demonstrate the importance of careful interpretation of model performance in healthcare-related data analysis.



**Dataset**

&#x20;Dataset Size



The dataset contains:



\- 583 adult records

\- 15 variables



The variables represent a combination of demographic characteristics, health conditions, lifestyle factors, laboratory measurements, cardiovascular measurements, and diabetes outcome.



The dataset was prepared for this educational project and does not contain identifiable patient information.



The exact original source and the complete procedure used to generate or modify the final dataset are not fully documented. Therefore, the dataset should be treated as a demonstration dataset rather than as a representative clinical population.



This is an important limitation of the project. Associations observed within the dataset should not automatically be interpreted as estimates of associations in real patients.



&#x20;**Variables**



The dataset contains the following variables:



&#x20;**Demographic Variables**



\- Age

\- Sex



&#x20;**Anthropometric Variable**



\- Body Mass Index (BMI)



&#x20;**Medical History Variables**



\- Hypertension

\- Heart disease



&#x20;**Lifestyle Variables**



\- Smoking

\- Physical activity



&#x20;**Glycemic Variables**



\- Glucose

\- HbA1c



&#x20;**Blood Pressure Variables**



\- Systolic blood pressure

\- Diastolic blood pressure



&#x20;**Lipid Variables**



\- HDL cholesterol

\- LDL cholesterol

\- Triglycerides



&#x20;**Outcome Variable**



\- Diabetes status



The diabetes variable is used as the target outcome for the logistic regression model.





&#x20;**Analysis Workflow**



The project follows the workflow below:



Data loading and inspection

↓

Exploratory data analysis

↓

Group comparisons

↓

Statistical testing

↓

80/20 stratified train-test split

↓

Feature standardization

↓

Baseline logistic regression model

↓

Baseline model evaluation

↓

Random introduction of missing values

↓

Median imputation

↓

Feature standardization

↓

Logistic regression using the missing-data condition

↓

Model evaluation

↓

Comparison of clean and missing-data model performance



1\. Data Loading and Initial Inspection



The dataset was loaded into Google Colab using Python and pandas.



Initial inspection was performed to understand the structure of the data before modelling.



The inspection included:



\- Number of records

\- Number of variables

\- Column names

\- Data types

\- Example observations

\- Diabetes outcome counts



The dataset contained **583 rows and 15 columns**.



Inspecting the data before analysis is an important step because it helps identify the available variables and understand the structure of the dataset before statistical testing or predictive modelling.



2\. Exploratory Data Analysis



Exploratory data analysis was performed before model development.



The analysis examined the distribution of diabetes status and selected clinical characteristics within the dataset.



The diabetes outcome distribution showed that the dataset contained approximately:



\- 502 records without diabetes

\- 81 records with diabetes



This indicates that the outcome classes were not evenly distributed.



The diabetes class represented a smaller proportion of the dataset than the non-diabetes class.



This imbalance is important when interpreting model accuracy. A model can achieve relatively high overall accuracy when the majority class is much larger while still performing less effectively at identifying the smaller positive class.



For this reason, the project later evaluates sensitivity, specificity, PPV, NPV, and ROC-AUC in addition to accuracy.



&#x20;**Diabetes Distribution Visualization**



A bar chart was generated to visualize the number of records in the two outcome groups:



\- No Diabetes

\- Diabetes



The figure is saved as:



`diabetes\_distribution.png`



This provides a simple visual representation of the imbalance between the two outcome classes.



&#x20;3. Comparison of Selected Clinical Characteristics



Selected variables were summarized separately for the diabetes and non-diabetes groups.



Mean values were examined for:



\- Age

\- BMI

\- Glucose

\- HbA1c



The purpose of this step was to explore whether these variables showed different patterns across the two outcome groups within the project dataset.



A separate bar chart was also generated to compare mean glucose between diabetes and non-diabetes records.



Because the exact generation or modification process of the dataset is not fully documented, these differences should be interpreted only as characteristics of this project dataset.



They should not be interpreted as estimates of clinical effects or population-level relationships.



4\. Statistical Analysis



Statistical comparisons were performed for two glycemic variables:



\- Glucose

\- HbA1c



Welch's independent-samples t-test was used to compare values between the diabetes and non-diabetes groups.



Welch's version of the independent t-test was used so that equal variance between the two groups did not have to be assumed.



&#x20;**Glucose Comparison**



The statistical comparison for glucose produced:



\- t-statistic: -10.303

\- p-value: approximately 1.54 × 10⁻¹⁷



This indicates a substantial difference in glucose values between the two outcome groups within this dataset.



&#x20;**HbA1c Comparison**



The statistical comparison for HbA1c produced:



\- t-statistic: -11.755

\- p-value:approximately 6.49 × 10⁻²¹



This also indicates a substantial difference between the two groups within this dataset.



However, these p-values should be interpreted cautiously.



Because the dataset preparation and outcome-generation mechanism are not fully documented, these tests demonstrate statistical comparison within the project dataset rather than providing evidence about a real clinical population.



&#x20;5. Train-Test Split



Before predictive modelling, the outcome variable was separated from the predictor variables.



The data were then divided into training and testing sets using an:



**80% training / 20% testing split**



The split produced:



\- 466 training records

\- 117 testing records



A **stratified train-test** split was used.



Stratification helps preserve the proportion of diabetes and non-diabetes outcomes in both the training and test sets.



A fixed:



`random\_state = 42`



was used to improve reproducibility.



The test set was kept separate from model training so that performance could be evaluated on observations not used to fit the model.



&#x20;6. Baseline Logistic Regression Model



Logistic regression was selected as the prediction model.



Logistic regression provides a relatively simple and interpretable baseline approach for binary classification and is suitable for demonstrating the effect of preprocessing and missing-data handling.



Before fitting the model, predictor variables were standardized using:



`StandardScaler`



The baseline modelling pipeline therefore followed:



**StandardScaler → Logistic Regression**



The logistic regression model used:



`max\_iter = 1000`



The model was fitted using the training data and evaluated using the held-out test data.



&#x20;7. Why Multiple Evaluation Metrics Were Used



Model performance was not evaluated using accuracy alone.



The following metrics were calculated:



\- Accuracy

\- Sensitivity

\- Specificity

\- Positive Predictive Value (PPV)

\- Negative Predictive Value (NPV)

\- ROC-AUC



Each metric describes a different aspect of model performance.



&#x20;Accuracy



Accuracy represents the proportion of all test observations that were classified correctly.



However, accuracy can be misleading when outcome classes are imbalanced.



Because the dataset contains considerably more non-diabetes than diabetes records, accuracy alone would not show how well the model identifies diabetes cases.



&#x20;Sensitivity



Sensitivity measures the proportion of actual diabetes cases correctly identified by the model.



It is calculated as:



**TP / (TP + FN)**



where:



\- TP = true positives

\- FN = false negatives



Sensitivity is particularly useful for understanding performance on the positive diabetes class.



&#x20;Specificity



Specificity measures the proportion of non-diabetes cases correctly identified.



It is calculated as:



**TN / (TN + FP)**



where:



\- TN = true negatives

\- FP = false positives



&#x20;Positive Predictive Value



Positive Predictive Value (PPV), also called precision, represents the proportion of positive model predictions that are true positives.



It is calculated as:



**TP / (TP + FP)**



&#x20;Negative Predictive Value



Negative Predictive Value (NPV) represents the proportion of negative model predictions that are true negatives.



It is calculated as:



**TN / (TN + FN)**



&#x20;ROC-AUC



The Receiver Operating Characteristic Area Under the Curve (ROC-AUC) evaluates the model's ability to distinguish between the two outcome classes across different classification thresholds.



Unlike metrics calculated at one classification threshold, ROC-AUC provides a broader measure of discrimination.



&#x20;8. Clean-Data Model Results



The baseline logistic regression model was evaluated on the clean test dataset.



The confusion matrix was:



\[97, 4],

&#x20;\[ 7, 9]



This corresponds to:



\- True negatives:97

\- False positives: 4

\- False negatives: 7

\- True positives: 9



The model therefore correctly classified most non-diabetes cases but missed several diabetes cases.



&#x20;**Clean-Data Performance**



The clean-data model achieved:



| Metric | Performance |

|

| Accuracy | 90.60% |

| Sensitivity | 56.25% |

| Specificity | 96.04% |

| PPV | 69.23% |

| NPV | 93.27% |

| ROC-AUC | 0.893 |



The overall accuracy was high at 90.60%.



However, sensitivity was only 56.25%.



This demonstrates why examining accuracy alone would provide an incomplete interpretation of the model.



The model performed much better at identifying non-diabetes cases, reflected by a specificity of 96.04%, than at identifying diabetes cases.



&#x20;9. ROC Curve



Predicted probabilities from the clean-data logistic regression model were used to generate a Receiver Operating Characteristic curve.



The clean model achieved:



**ROC-AUC = 0.893**



The ROC curve is saved as:



`roc\_curve.png`



The ROC curve provides a visual representation of the trade-off between true-positive rate and false-positive rate across different classification thresholds.



&#x20;10. Missing-Data Experiment



After establishing baseline performance, a controlled missing-data experiment was performed.



Missing values were introduced into five selected clinical variables:



1\. BMI

2\. Glucose

3\. HbA1c

4\. Systolic blood pressure

5\. Diastolic blood pressure



These variables were selected to simulate incomplete clinical measurements.



Approximately **10% of values in each selected variable** were randomly changed to missing values.



A fixed random seed was used:



`np.random.seed(42)`



This makes the random missingness experiment reproducible.



&#x20;**Missingness in the Training Data**



The training dataset contained 466 observations.



For each selected variable, **46 values** were randomly set to missing.



Therefore, missing values were introduced separately into:



\- BMI: 46 missing values

\- Glucose: 46 missing values

\- HbA1c: 46 missing values

\- Systolic blood pressure: 46 missing values

\- Diastolic blood pressure: 46 missing values



This corresponds to approximately 10% missingness in each selected training variable.



\---



&#x20;**Missingness in the Test Data**



The test dataset contained 117 observations.



For each selected variable, **11 values** were randomly set to missing.



Therefore:



\- BMI: 11 missing values

\- Glucose: 11 missing values

\- HbA1c: 11 missing values

\- Systolic blood pressure: 11 missing values

\- Diastolic blood pressure: 11 missing values



Again, this represents approximately 10% missingness.



&#x20;**Why Missingness Was Introduced Separately**



Missing values were introduced separately into copies of the training and test predictor sets.



The original train-test split was preserved.



This allowed the comparison to use the same underlying training and test observations while changing the data-quality condition.



The experiment therefore compared:



**Complete data**



versus



**Approximately 10% random missingness + median imputation**



&#x20;11. Missing-Data Assumption



The missing values were introduced randomly by the analysis code.



Therefore, this experiment represents a simplified random missingness scenario.



Real healthcare data can have more complicated missingness mechanisms.



For example, whether a clinical measurement is available may depend on:



\- Clinical condition

\- Testing decisions

\- Healthcare access

\- Documentation practices

\- Facility workflow

\- Patient characteristics



This project does not attempt to reproduce these more complex mechanisms.



Instead, random missingness was used to create a controlled educational experiment.



&#x20;12. Median Imputation



Machine-learning models such as the implementation of logistic regression used in this project cannot directly train on these missing values.



Median imputation was therefore used to replace the missing observations.



The imputation method was:



`SimpleImputer(strategy="median")`



For each affected predictor, missing observations were replaced using the median learned from the training data.



Median imputation was selected as a simple and commonly understandable approach for demonstrating missing-data handling.



The project does not claim that median imputation is the optimal method for every clinical dataset.



&#x20;13. Prevention of Data Leakage



A particularly important part of the workflow was ensuring that preprocessing did not use information from the test dataset during model training.



The missing-data model was created using a scikit-learn pipeline:



**Median Imputation → Standardization → Logistic Regression**



Conceptually:

text

Training Data

&#x20;     ↓

Median Imputer

&#x20;     ↓

StandardScaler

&#x20;     ↓

Logistic Regression





The imputer and scaler were fitted using the **training data only**.



The fitted transformations were then applied to the test data.



This prevents the test data from influencing the calculation of training medians or scaling parameters.



Using information from the test set during preprocessing could produce **data leakage** and lead to an overly optimistic estimate of model performance.



Using a pipeline helps keep preprocessing and model fitting together and reduces this risk.



&#x20;14. Missing-Data Model



After introducing missing values, the second model used the following pipeline:



SimpleImputer(strategy="median")

&#x20;       ↓

StandardScaler

&#x20;       ↓

LogisticRegression(max\_iter=1000)





The logistic regression modelling approach remained comparable with the baseline condition.



The main additional preprocessing step was median imputation.



This allowed the project to examine model performance under the simulated missing-data condition.



&#x20;15. Missing Data + Median Imputation Results



The confusion matrix for the missing-data model was:



\[97, 4],

&#x20;\[ 6, 10]



This corresponds to:



\- True negatives: 97

\- False positives: 4

\- False negatives: 6

\- True positives: 10



Compared with the clean-data model, the missing-data model produced one fewer false negative and one additional true positive in this particular test set.



&#x20;**Missing-Data Model Performance**



| Metric | Performance |

|---|---:|

| Accuracy | 91.45% |

| Sensitivity | 62.50% |

| Specificity | 96.04% |

| PPV | 71.43% |

| NPV | 94.17% |

| ROC-AUC | 0.881 |



&#x20;16. Clean vs Missing-Data Model Comparison



The final comparison was:



| Metric | Clean Data | Missing Data + Median Imputation | Direction of Change |

| Accuracy | 90.60% | 91.45% | Slight increase |

| Sensitivity | 56.25% | 62.50% | Increase |

| Specificity | 96.04% | 96.04% | No change |

| PPV | 69.23% | 71.43% | Slight increase |

| NPV | 93.27% | 94.17% | Slight increase |

| ROC-AUC | 0.893 | 0.881 | Slight decrease |



The comparison was also visualized in:



`model\_performance\_comparison.png`



&#x20;17. Interpretation of the Results



The missing-data experiment did **not** produce the same direction of change across every performance metric.



After approximately 10% random missingness and median imputation:



\- Accuracy increased slightly.

\- Sensitivity increased.

\- Specificity remained unchanged.

\- PPV increased slightly.

\- NPV increased slightly.

\- ROC-AUC decreased.



At first glance, the increase in several metrics could appear to suggest that the model improved after missingness was introduced.



That conclusion would be inappropriate.



The experiment does **not** demonstrate that missing data improve prediction.



There are several reasons for caution.



&#x20;**Sensitivity Changed Because of One Prediction**



The clean-data confusion matrix was:



\[97, 4],

&#x20;\[ 7, 9]



The missing-data model produced:



\[97, 4],

&#x20;\[ 6, 10]





There were only **16 diabetes cases in the test set.**



For the clean model:



9 / 16 = 56.25% sensitivity



For the missing-data model:



10 / 16 = 62.50% sensitivity



Therefore, the increase in sensitivity resulted from only **one additional diabetes case being correctly classified**.



This demonstrates how performance metrics can change noticeably when the number of positive cases in a test sample is small.



&#x20;**ROC-AUC Moved in the Opposite Direction**



While several threshold-based metrics increased, ROC-AUC decreased:



0.893 → 0.881



Accuracy, sensitivity, specificity, PPV, and NPV depend on predictions at a selected classification threshold.



ROC-AUC instead evaluates discrimination across a range of thresholds.



Therefore, the results show why conclusions should not be based on a single performance metric.



The model's threshold-based classifications happened to improve slightly in this particular experimental run, while its overall ranking/discrimination measured by ROC-AUC became slightly lower.



&#x20;18. Main Findings



The main observations from this project are:



&#x20;1. High accuracy did not mean equally high sensitivity



The clean model achieved **90.60% accuracy**, but sensitivity was only **56.25%**.



This illustrates why accuracy alone can hide weaker performance on the smaller positive class.



&#x20;2. Missingness and imputation changed model performance



Introducing approximately 10% random missingness followed by median imputation changed several evaluation metrics.



&#x20;3. Different metrics gave different impressions



Several threshold-based metrics increased slightly, while ROC-AUC decreased.



Therefore, the effect of preprocessing cannot be summarized accurately using only one metric.



&#x20;4. Small test samples can produce unstable-looking changes



Only 16 diabetes cases were present in the test set.



One additional correct prediction changed sensitivity by more than six percentage points.



&#x20;5. Data preprocessing should be separated between training and test data



The imputer and scaler were fitted only using training data, demonstrating a basic method for avoiding data leakage.



&#x20;19. Key Learning from the Project



This project provided practical experience across several stages of a health data science workflow.



&#x20;**Data Inspection**



The project involved loading a structured dataset, checking its dimensions and variables, examining data types, and reviewing outcome distributions.



&#x20;**Exploratory Data Analysis**



Group-level summaries and visualizations were used to understand characteristics of the dataset before modelling.



&#x20;**Statistical Testing**



Welch's independent-samples t-tests were used to compare glucose and HbA1c between outcome groups.



&#x20;**Predictive Modelling**



A logistic regression model was developed as a baseline binary classifier.



&#x20;**Data Preprocessing**



Feature standardization was incorporated into the modelling workflow.



&#x20;**Missing-Data Simulation**



A controlled data-quality problem was created by randomly introducing missing values into selected clinical measurements.



&#x20;**Missing-Data Handling**



Median imputation was implemented using SimpleImputer.



&#x20;**Pipeline Construction**



scikit-learn pipelines were used to combine preprocessing and modelling steps.



&#x20;**Data Leakage Prevention**



The imputer and scaler were fitted using training data rather than the full dataset.



&#x20;**Model Evaluation**



Performance was assessed using accuracy, sensitivity, specificity, PPV, NPV, confusion matrices, and ROC-AUC.



&#x20;**Interpretation**



The project demonstrated that a change in one model metric should not automatically be interpreted as an overall improvement or deterioration.



&#x20;20. Relevance to Health Data Science



Healthcare analytics involves more than fitting predictive models.



The quality and completeness of the underlying information can affect:



\- Statistical analysis

\- Model development

\- Model evaluation

\- Interpretation of results

\- Reliability of data-driven decisions



Missing clinical information is therefore an important data-quality issue.



This project provides a small controlled demonstration of how a missing-data problem can be introduced, handled, and evaluated systematically.



It also emphasizes that technical preprocessing choices should be documented because they form part of the analytical methodology rather than being treated as invisible steps.



&#x20;21. Limitations



This project has several important limitations.



&#x20;**Dataset provenance**



The dataset was prepared for an educational project, but its exact original source and complete generation or modification process are not fully documented.



Therefore, results should not be interpreted as findings from a representative clinical population.



&#x20;**Dataset size**



The dataset contains only 583 records.



A larger dataset would provide a stronger basis for evaluating model stability.



&#x20;**Outcome imbalance**



The dataset contains substantially fewer diabetes records than non-diabetes records.



This affects interpretation of overall accuracy and contributes to the importance of examining sensitivity and other metrics.



&#x20;**Small number of positive test cases**



Only 16 diabetes cases were present in the test set.



This means that changing the classification of a very small number of records can noticeably change sensitivity.



&#x20;**Single train-test split**



The project uses one 80/20 train-test split.



Performance may differ with another split.



&#x20;**Single missingness simulation**



Only one randomly generated missingness pattern was evaluated.



A different random seed could produce different missing observations and potentially different performance results.



&#x20;**Simplified missingness mechanism**



Missing values were introduced randomly.



Real clinical missingness can be systematic and may depend on patient characteristics, clinical decisions, healthcare access, workflow, or disease status.



&#x20;**One level of missingness**



Only approximately 10% missingness was examined.



The project does not evaluate whether performance changes differently at higher or lower levels of missingness.



&#x20;**One imputation method**



Only median imputation was evaluated.



Other approaches could include more advanced imputation methods, but comparison of imputation algorithms was outside the scope of this project.



&#x20;**One modelling algorithm**



Only logistic regression was evaluated.



The project therefore does not compare the effect of missing data across different machine-learning algorithms.



&#x20;**Statistical interpretation**



Because the dataset generation mechanism is not fully documented, statistical differences between outcome groups should be treated as characteristics of the project dataset rather than clinical evidence.



&#x20;**No external validation**



The model was not evaluated using an independent external dataset.



&#x20;**No clinical validation**



The model has not been clinically validated and is not intended for diagnosis, screening, treatment decisions, or patient care.



&#x20;22. Tools and Technologies



The analysis was performed in Google Colab using Python.



Main libraries included:

&#x20;pandas



Used for:



\- Loading the dataset

\- Inspecting records

\- Selecting variables

\- Grouping observations

\- Calculating descriptive summaries



&#x20;**NumPy**



Used for:



\- Random selection of observations

\- Introducing missing values

\- Reproducible random operations



&#x20;**SciPy**



Used for:



\- Welch's independent-samples t-tests



&#x20;**scikit-learn**



Used for:



\- Train-test splitting

\- Stratification

\- Median imputation

\- Feature standardization

\- Logistic regression

\- Modelling pipelines

\- Predictions

\- Predicted probabilities

\- Confusion matrices

\- Accuracy

\- Sensitivity

\- Precision/PPV

\- ROC-AUC

\- ROC curves



&#x20;**Matplotlib**



Used to generate:



\- Diabetes distribution visualization

\- Mean glucose visualization

\- ROC curve

\- Model performance comparison



&#x20;23. Main Python Components



Important components used in the notebook include:



python

pandas

numpy

matplotlib

scipy.stats.ttest\_ind



sklearn.model\_selection.train\_test\_split

sklearn.pipeline.make\_pipeline

sklearn.preprocessing.StandardScaler

sklearn.impute.SimpleImputer

sklearn.linear\_model.LogisticRegression



sklearn.metrics.accuracy\_score

sklearn.metrics.confusion\_matrix

sklearn.metrics.precision\_score

sklearn.metrics.recall\_score

sklearn.metrics.roc\_auc\_score

sklearn.metrics.roc\_curve



&#x20;24. Generated Visualizations



The project generates several figures.



&#x20;**Diabetes Distribution**



`diabetes\_distribution.png`



Shows the number of diabetes and non-diabetes records in the dataset.



&#x20;**Mean Glucose by Diabetes Status**



Displays mean glucose values for the two outcome groups during exploratory analysis.



&#x20;**ROC Curve**



`roc\_curve.png`



Shows the ROC curve for the clean-data logistic regression model.



&#x20;**Model Performance Comparison**



`model\_performance\_comparison.png`



Compares:



\- Accuracy

\- Sensitivity

\- Specificity

\- PPV

\- NPV

\- ROC-AUC



between the clean-data model and the missing-data + median-imputation model.



&#x20;25. Project Structure





Diabetes\_Data\_Quality\_Project/

│

├── Diabetes\_Data\_Quality\_Project.ipynb

│

├── README.md

│

├── data/

│   └── diabetes\_data\_quality\_synthetic\_583.csv

│

└── figures/

&#x20;   ├── diabetes\_distribution.png

&#x20;   ├── roc\_curve.png

&#x20;   └── model\_performance\_comparison.png



&#x20;Impact of Missing Clinical Data and Median Imputation on a Diabetes Prediction Model



&#x20;**Project Overview**



Clinical datasets often contain missing information because measurements may not be recorded, tests may not be performed, or documentation may be incomplete. Missing data can affect statistical analysis, model development, and the interpretation of predictive performance.



This project explores how missing clinical data and median imputation affect the performance of a logistic regression model for diabetes prediction. The analysis uses a dataset containing 583 adult records with demographic, lifestyle, cardiovascular, laboratory, and diabetes outcome variables.



The project first examines the dataset through exploratory data analysis and statistical comparisons. A logistic regression model is then trained and evaluated using the complete dataset to establish baseline performance.



A controlled missing-data experiment is subsequently performed. Approximately 10% of values are randomly removed from five selected clinical variables: BMI, glucose, HbA1c, systolic blood pressure, and diastolic blood pressure. Median imputation is then applied before fitting and evaluating the logistic regression model under the missing-data condition.



Performance of the clean-data model and the missing-data model is compared using accuracy, sensitivity, specificity, positive predictive value (PPV), negative predictive value (NPV), and ROC-AUC.



The purpose of this project is not to develop a clinical diagnostic tool. It is an educational health data science project demonstrating how data quality, missing values, preprocessing decisions, and evaluation metrics can influence the interpretation of predictive models.



&#x20;**Research Question**



How does introducing approximately 10% random missingness in selected clinical variables and applying median imputation affect the performance of a logistic regression model for diabetes prediction?



&#x20;**Project Objectives**



The objectives of this project were to:



\- Inspect and explore a clinical-style dataset.

\- Examine the distribution of diabetes status.

\- Compare selected characteristics between diabetes and non-diabetes groups.

\- Perform statistical comparisons of glucose and HbA1c.

\- Develop a baseline logistic regression model using complete data.

\- Evaluate the model using multiple classification metrics.

\- Simulate a data-quality problem by introducing missing values into selected clinical variables.

\- Apply median imputation while preventing data leakage.

\- Evaluate the logistic regression model after missing-data handling.

\- Compare model performance before and after the missing-data experiment.



&#x20;**Dataset**



The dataset contains 583 adult records and 15 variables.



The variables include:



\- Age

\- Sex

\- Body Mass Index (BMI)

\- Hypertension

\- Heart disease

\- Smoking

\- Physical activity

\- Glucose

\- HbA1c

\- Systolic blood pressure

\- Diastolic blood pressure

\- HDL cholesterol

\- LDL cholesterol

\- Triglycerides

\- Diabetes outcome



The dataset was prepared for this educational project and does not contain identifiable patient information.



The exact original source and complete procedure used to generate or modify the final dataset are not fully documented. Therefore, the dataset should be treated as a demonstration dataset rather than as a representative clinical population. Relationships observed within the dataset should not be interpreted as population-level clinical evidence.



&#x20;**Analysis Workflow**



The project followed these main stages:



1\. Data loading and initial inspection

2\. Exploratory data analysis

3\. Comparison of selected clinical variables

4\. Statistical testing

5\. Stratified train-test split

6\. Baseline logistic regression modelling

7\. Evaluation of the clean-data model

8\. Introduction of random missing values

9\. Median imputation

10\. Logistic regression modelling under the missing-data condition

11\. Comparison of model performance



**Data Loading and Initial Inspection**



The dataset was loaded into Google Colab using Python and pandas.



Initial inspection was performed to examine the number of records, number of variables, column names, data types, example observations, and diabetes outcome distribution.



The dataset contained 583 rows and 15 columns.



Inspecting the dataset before analysis helped establish its structure and identify the variables available for exploratory analysis and predictive modelling.



&#x20;**Exploratory Data Analysis**



Exploratory data analysis was performed before model development.



The diabetes outcome distribution showed approximately:



\- 502 records without diabetes

\- 81 records with diabetes



The dataset therefore contained considerably fewer diabetes records than non-diabetes records.



This class imbalance is important when interpreting model accuracy. A model may achieve high overall accuracy because most observations belong to the majority class while still performing less effectively at identifying diabetes cases.



For this reason, the final model evaluation included sensitivity, specificity, PPV, NPV, and ROC-AUC in addition to accuracy.



A bar chart was generated to visualize the diabetes outcome distribution and saved as:



diabetes\_distribution.png



&#x20;**Comparison of Selected Clinical Characteristics**



Selected clinical characteristics were summarized separately for the diabetes and non-diabetes groups.



Mean values were examined for:



\- Age

\- BMI

\- Glucose

\- HbA1c



Mean glucose was also visualized by diabetes status.



These comparisons were used to explore patterns within the project dataset before predictive modelling.



Because the exact generation or modification process of the dataset is not fully documented, these differences should be interpreted only as characteristics of this dataset rather than evidence of clinical relationships in a real population.



&#x20;**Statistical Analysis**



Glucose and HbA1c were compared between diabetes and non-diabetes groups using Welch's independent-samples t-test.



Welch's t-test was used so that equal variance between the two groups did not have to be assumed.



For glucose, the analysis produced:



\- t-statistic: -10.303

\- p-value: approximately 1.54 × 10⁻¹⁷



For HbA1c, the analysis produced:



\- t-statistic: -11.755

\- p-value: approximately 6.49 × 10⁻²¹



These results indicate substantial differences between the two outcome groups within this dataset.



However, because the dataset preparation and outcome-generation process are not fully documented, these results should be interpreted as statistical comparisons within the project dataset rather than population-level clinical findings.



&#x20;**Train-Test Split**



The diabetes outcome was separated from the predictor variables before model development.



The dataset was divided using an 80/20 train-test split:



\- Training set: 466 records

\- Test set: 117 records



A stratified split was used to preserve the proportion of diabetes and non-diabetes cases across the training and test sets.



A random state of 42 was used for reproducibility.



The test set was kept separate from model training so that performance could be evaluated on observations that were not used to fit the model.



&#x20;**Baseline Logistic Regression Model**



Logistic regression was selected as the baseline binary classification model.



Before model fitting, predictor variables were standardized using StandardScaler.



The clean-data modelling pipeline consisted of:



Standardization → Logistic Regression



The logistic regression model used a maximum of 1,000 iterations.



The model was trained on the training set and evaluated on the held-out test set.



&#x20;**Model Evaluation**



Model performance was evaluated using several metrics rather than accuracy alone.



Accuracy measures the proportion of all test observations classified correctly.



Sensitivity measures the proportion of actual diabetes cases correctly identified by the model.



Specificity measures the proportion of non-diabetes cases correctly identified.



Positive Predictive Value (PPV) measures the proportion of positive model predictions that are true positives.



Negative Predictive Value (NPV) measures the proportion of negative model predictions that are true negatives.



ROC-AUC evaluates the model's ability to distinguish between the two outcome classes across different classification thresholds.



Using several metrics was particularly important because the dataset contained fewer diabetes cases than non-diabetes cases.



&#x20;**Clean-Data Model Results**



The clean-data model produced the following confusion matrix:



&#x20;\[97, 4],

&#x20;\[ 7, 9]



This corresponds to:



\- True negatives: 97

\- False positives: 4

\- False negatives: 7

\- True positives: 9



The model achieved:



| Metric | Clean-Data Model |



| Accuracy | 90.60% |

| Sensitivity | 56.25% |

| Specificity | 96.04% |

| PPV | 69.23% |

| NPV | 93.27% |

| ROC-AUC | 0.893 |



Although overall accuracy was 90.60%, sensitivity was 56.25%. This demonstrates why accuracy alone would provide an incomplete picture of model performance.



The model performed considerably better at identifying non-diabetes cases than diabetes cases.



&#x20;**ROC Curve**



Predicted probabilities from the clean-data logistic regression model were used to generate a Receiver Operating Characteristic curve.



The clean model achieved a ROC-AUC of 0.893.



The ROC curve was saved as:



roc\_curve.png



The curve represents the relationship between the true-positive rate and false-positive rate across different classification thresholds.



&#x20;**Missing-Data Experiment**



After establishing baseline performance, a controlled missing-data experiment was performed.



Missing values were introduced into five selected variables:



\- BMI

\- Glucose

\- HbA1c

\- Systolic blood pressure

\- Diastolic blood pressure



Approximately 10% of observations in each selected variable were randomly changed to missing values.



A NumPy random seed of 42 was used to make the missingness simulation reproducible.



Missing values were introduced separately into copies of the training and test predictor sets.



In the training set, 46 values were set to missing in each of the five selected variables.



In the test set, 11 values were set to missing in each selected variable.



This corresponds to approximately 10% missingness in each selected variable.



The original train-test split was preserved so that the clean-data and missing-data experiments used the same underlying training and test observations.



&#x20;**Missing-Data Assumption**



The missing values in this project were introduced randomly by the analysis code.



This represents a simplified random missingness scenario.



Real clinical data may have more complicated missingness patterns. Whether a measurement is available may depend on factors such as clinical condition, testing decisions, healthcare access, documentation practices, patient characteristics, or facility workflow.



The experiment therefore does not attempt to reproduce every type of missingness that may occur in real healthcare data. Random missingness was used to create a controlled educational experiment.



&#x20;**Median Imputation**



Median imputation was used to handle missing values.



The imputation method was:



SimpleImputer(strategy="median")



Missing observations were replaced using median values learned from the training data.



Median imputation was selected as a simple method for demonstrating missing-data handling. The project does not assume that median imputation is the optimal approach for every clinical dataset.



&#x20;**Prevention of Data Leakage**



An important part of the modelling workflow was preventing information from the test dataset from influencing preprocessing during training.



The missing-data model used the following pipeline:



Median Imputation → Standardization → Logistic Regression



The imputer and scaler were fitted using the training data only. The transformations learned from the training data were then applied to the test data.



This prevents test-set information from influencing the calculation of imputation values or scaling parameters.



Using information from the test set during model preprocessing could introduce data leakage and produce an overly optimistic estimate of performance.



Using a scikit-learn pipeline helped keep preprocessing and model fitting together and reduced this risk.



&#x20;**Missing-Data Model Results**



After approximately 10% random missingness and median imputation, the model produced the following confusion matrix:



&#x20;\[97, 4],

&#x20;\[ 6, 10]



This corresponds to:



\- True negatives: 97

\- False positives: 4

\- False negatives: 6

\- True positives: 10



The missing-data model achieved:



| Metric | Missing Data + Median Imputation |

| Accuracy | 91.45% |

| Sensitivity | 62.50% |

| Specificity | 96.04% |

| PPV | 71.43% |

| NPV | 94.17% |

| ROC-AUC | 0.881 |



&#x20;**Model Performance Comparison**



The final comparison between the two experimental conditions was:



| Metric | Clean Data | Missing Data + Median Imputation |

| Accuracy | 90.60% | 91.45% |

| Sensitivity | 56.25% | 62.50% |

| Specificity | 96.04% | 96.04% |

| PPV | 69.23% | 71.43% |

| NPV | 93.27% | 94.17% |

| ROC-AUC | 0.893 | 0.881 |



The comparison was also visualized and saved as:



model\_performance\_comparison.png



&#x20;**Interpretation of Results**



The missing-data experiment did not produce the same direction of change across all performance metrics.



After approximately 10% random missingness followed by median imputation:



\- Accuracy increased from 90.60% to 91.45%.

\- Sensitivity increased from 56.25% to 62.50%.

\- Specificity remained unchanged at 96.04%.

\- PPV increased from 69.23% to 71.43%.

\- NPV increased from 93.27% to 94.17%.

\- ROC-AUC decreased from 0.893 to 0.881.



These results should not be interpreted as evidence that missing data improve prediction.



The clean-data confusion matrix contained 9 true positives and 7 false negatives. The missing-data model contained 10 true positives and 6 false negatives.



There were only 16 diabetes cases in the test set.



For the clean model:



Sensitivity = 9 / 16 = 56.25%



For the missing-data model:



Sensitivity = 10 / 16 = 62.50%



Therefore, the increase in sensitivity resulted from only one additional diabetes case being classified correctly.



This demonstrates how model metrics can change noticeably when the number of positive cases in a test sample is small.



ROC-AUC also moved in the opposite direction from several threshold-based metrics. While accuracy, sensitivity, PPV, and NPV increased slightly, ROC-AUC decreased from 0.893 to 0.881.



This illustrates why the effect of a preprocessing or data-quality intervention should be evaluated using multiple metrics rather than a single performance measure.



&#x20;**Main Findings**



The project produced several useful observations.



First, high overall accuracy did not mean that the model performed equally well on both outcome classes. The clean-data model achieved 90.60% accuracy but only 56.25% sensitivity.



Second, introducing missing values and applying median imputation changed model performance, but the direction of change depended on the metric being examined.



Third, several threshold-based metrics increased slightly while ROC-AUC decreased.



Fourth, the relatively small number of diabetes cases in the test set meant that one additional correct prediction produced a noticeable change in sensitivity.



Finally, the project demonstrated the importance of fitting preprocessing steps only on training data to avoid data leakage.



&#x20;**Key Learning**



This project provided practical experience with several stages of a health data science workflow.



It involved:



\- Loading and inspecting structured health-related data

\- Exploratory data analysis

\- Group-level comparisons

\- Statistical testing

\- Stratified train-test splitting

\- Feature standardization

\- Logistic regression

\- Missing-data simulation

\- Median imputation

\- scikit-learn pipelines

\- Prevention of data leakage

\- Confusion-matrix interpretation

\- Calculation of sensitivity and specificity

\- Calculation of PPV and NPV

\- ROC-AUC evaluation

\- Data visualization

\- Comparison of model performance

\- Interpretation of model results and limitations



One of the main lessons from the project is that accuracy alone does not provide a complete picture of classification performance.



Another important lesson is that preprocessing decisions form part of the analytical methodology. Missing-data handling should therefore be documented and evaluated rather than treated as an invisible technical step.



&#x20;***Relevance to Health Data Science***



Healthcare data analysis depends not only on modelling methods but also on the quality and completeness of the underlying information.



Incomplete clinical data can affect statistical analysis, predictive modelling, model evaluation, and the interpretation of results.



This project provides a small controlled demonstration of how a missing-data problem can be introduced, handled, and evaluated.



It also demonstrates why health data science workflows should document preprocessing decisions and examine several measures of model performance.



&#x20;**Limitations**



This project has several limitations.



\- The exact original source and complete generation or modification process of the dataset are not fully documented.

\- The dataset should therefore be treated as a demonstration dataset rather than a representative clinical population.

\- The dataset contains only 583 records.

\- The outcome classes are imbalanced.

\- Only 16 diabetes cases were present in the test set.

\- Only one 80/20 train-test split was evaluated.

\- Only one random missingness simulation was tested.

\- A different random seed could produce a different missingness pattern and different model results.

\- Missing values were introduced randomly and therefore represent only one simplified missing-data scenario.

\- Real clinical missingness may depend on patient characteristics, disease status, clinical decisions, healthcare access, or documentation practices.

\- Only approximately 10% missingness was investigated.

\- Median imputation was the only imputation method evaluated.

\- Logistic regression was the only prediction model evaluated.

\- No external validation dataset was used.

\- Statistical comparisons should not be interpreted as population-level clinical evidence.

\- The model has not been clinically validated.

\- The model should not be used for medical diagnosis or clinical decision-making.



&#x20;**Tools and Libraries**



The project was completed in Google Colab using Python.



The main libraries were:



\- pandas

\- NumPy

\- SciPy

\- scikit-learn

\- Matplotlib



pandas was used for loading, inspecting, selecting, grouping, and summarizing data.



NumPy was used for random selection and the controlled introduction of missing values.



SciPy was used for Welch's independent-samples t-tests.



scikit-learn was used for train-test splitting, median imputation, standardization, logistic regression, pipelines, predictions, confusion matrices, and model evaluation.



Matplotlib was used for data and model-performance visualizations.



&#x20;**Main Python Components**



Important Python components used in the project include:



&#x20;   pandas

&#x20;   numpy

&#x20;   matplotlib

&#x20;   scipy.stats.ttest\_ind

&#x20;   sklearn.model\_selection.train\_test\_split

&#x20;   sklearn.pipeline.make\_pipeline

&#x20;   sklearn.preprocessing.StandardScaler

&#x20;   sklearn.impute.SimpleImputer

&#x20;   sklearn.linear\_model.LogisticRegression

&#x20;   sklearn.metrics.accuracy\_score

&#x20;   sklearn.metrics.confusion\_matrix

&#x20;   sklearn.metrics.precision\_score

&#x20;   sklearn.metrics.recall\_score

&#x20;   sklearn.metrics.roc\_auc\_score

&#x20;   sklearn.metrics.roc\_curve



&#x20;**Visualizations**



The project includes the following visualizations:



1\. Diabetes outcome distribution

2\. Mean glucose by diabetes status

3\. ROC curve for the clean-data logistic regression model

4\. Model performance comparison between the clean-data and missing-data conditions



The main saved figure files are:



\- diabetes\_distribution.png

\- roc\_curve.png

\- model\_performance\_comparison.png



&#x20;**Project Structure**



&#x20;   Diabetes\_Data\_Quality\_Project/

&#x20;

&#x20;   ├── Diabetes\_Data\_Quality\_Project.ipynb

&#x20;   ├── README.md

&#x20;   │

&#x20;   ├── data

&#x20;   │   └── diabetes\_data\_quality\_synthetic\_583.csv

&#x20;   │

&#x20;   └── figures

&#x20;       ├── diabetes\_distribution.png

&#x20;       ├── roc\_curve.png

&#x20;       └── model\_performance\_comparison.png



&#x20;**Reproducibility**



Fixed random values were used where appropriate.



The train-test split used:



&#x20;   random\_state=42



The missingness simulation used:



&#x20;   np.random.seed(42)



These settings allow the same train-test split and missingness pattern to be reproduced when the analysis is rerun under the same conditions.



&#x20;**How to Run the Project**



1\. Open Diabetes\_Data\_Quality\_Project.ipynb in Google Colab or Jupyter Notebook.

2\. Upload diabetes\_data\_quality\_synthetic\_583.csv if using a new Colab session.

3\. Confirm that the file path in the data-loading cell matches the dataset location.

4\. Run the notebook cells from top to bottom.

5\. Review the exploratory analysis and statistical comparisons.

6\. Review the clean-data logistic regression results.

7\. Run the missing-data experiment and median-imputation model.

8\. Review the final model comparison and visualizations.



&#x20;**Possible Future Improvements**



This project was intentionally limited to a simple controlled experiment. Future work could improve the analysis by:



\- Repeating the missingness experiment using multiple random seeds

\- Using cross-validation

\- Evaluating several levels of missingness

\- Comparing different imputation methods

\- Investigating different missingness mechanisms

\- Comparing additional prediction algorithms

\- Examining model calibration

\- Using a larger and fully documented dataset

\- Performing external validation

\- Evaluating performance across relevant subgroups



These extensions could provide a more robust understanding of how missing data and preprocessing affect predictive performance.



&#x20;**Disclaimer**



This project is intended for educational and portfolio purposes.



The model has not been clinically validated and should not be used to diagnose diabetes, estimate an individual's clinical risk, make treatment decisions, replace clinical assessment, or guide patient care.



&#x20;**Conclusion**



This project investigated how a controlled missing-data problem and median imputation affected the performance of a logistic regression model for diabetes prediction.



The clean-data model achieved 90.60% accuracy, 56.25% sensitivity, 96.04% specificity, 69.23% PPV, 93.27% NPV, and a ROC-AUC of 0.893.



After approximately 10% random missingness was introduced into BMI, glucose, HbA1c, systolic blood pressure, and diastolic blood pressure and handled using median imputation, the model achieved 91.45% accuracy, 62.50% sensitivity, 96.04% specificity, 71.43% PPV, 94.17% NPV, and a ROC-AUC of 0.881.



Several threshold-based metrics increased slightly, while ROC-AUC decreased. These results do not demonstrate that missing data improve model performance. Instead, they illustrate that the observed effect of a data-quality intervention can vary depending on the evaluation metric and the particular experimental sample.



The increase in sensitivity resulted from only one additional correctly classified diabetes case, demonstrating the importance of considering sample size and confusion-matrix counts when interpreting changes in percentages.



Overall, the project demonstrates an introductory health data science workflow involving data inspection, exploratory analysis, statistical testing, train-test splitting, standardization, logistic regression, missing-data simulation, median imputation, prevention of data leakage, model evaluation, visualization, and cautious interpretation.



The main lesson is that data quality and preprocessing are important parts of health data analysis and that predictive models should be evaluated using multiple performance metrics rather than accuracy alone.

