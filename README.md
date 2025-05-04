# Predicting High Priced Loans Model Card

### Basic Information

- **Person or organization developing model**: Copyright (c) 2021 - 2025 Patrick Hall (jphall@gwu.edu), Hanna Courtot (Hanna.Courtot@gwu.edu), Elias Makanganise (eliasm@gwu.edu), Jabari Rose (Jabari.rose@gwmail.gwu.edu) and Pratyush Singhal (pratyush.singhal@gwu.edu)
- **Model creation date**: May, 2021
- **Model modification date**: May, 2025
- **Model version**: 2.0
- **License**: Apache License, Version 2.0; you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0. Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License. DISCLAIMER: These notebooks are not legal or compliance advice.
- **Model implementation code**: [Assignment 1.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_1/assign_1_template.ipynb), [Assignment 2.ipynb](
https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_2/assign_2_template.ipynb), [Assignment 3.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_3/assign_3_template.ipynb), [Assignment 4.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_4/assign_4_template.ipynb), [Assignment 5.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_5/assign_5_template.ipynb) and [Assignment 6.ipynb](https://github.com/jphall663/GWU_DNSC_6301_project)

### Intended Use
 
- **Describe the business value of your group’s best remediated model**: This model is not intended to generate any value for commercial/business purposes.
- **Describe how your group’s best remediated model is designed to be used**: This model is designed solely for educational purposes.
- **Describe the intended users for your group’s best remediated model**: This model is designed for students and individuals interested in learning about bias in machine learning models.
- **State whether your group’s best remediated model can or cannot be used for any additional purposes**: Our model cannot be used for any additional purposes. Any use beyond an educational example is out-of-scope.

### Training Data

- **State the source of training data**: [GW DNSC 6330 Class Github Training Data Zip](https://github.com/jphall663/GWU_rml/tree/master/assignments/data), email `jphall@gwu.edu` for more information
- **State how training data was divided into training and validation data**: 70% training and 30% validation.
- **State the number of rows in training and validation data**: 112253 training rows and 48085 validation rows.
- **Define the meaning of all training data columns**:
  | **Feature** | **Description** |
  |--------| ------------|
  | **high priced**| Binary target, whether (1) or not (0) the annual percentage rate (APR) charged for a mortgage is 150 basis points (1.5%) or more above a survey-based estimate of similar mortgages.|
  |**conforming**| Binary numeric input, whether the mortgage conforms to normal standards (1), or whether the loan is different (0).|
  |**debt to income ratio std**|Numeric input, standardized debt-to-income ratio for mortgage applicants.|
  |**debt to income ratio missing**|Binary numeric input, missing marker (1) for debt to income ratio std.|
  |**income std**| Numeric input, standardized income for mortgage applicants.|
  |**loan amount std**|Numeric input, standardized amount of the mortgage for applicants.|
  |**intro rate period std**| Numeric input, standardized introductory rate period for mortgage applicants.|
  |**loan to value ratio std** |Numeric input, ratio of the mortgage size to the value of the property for mortgage applicants.|
  |**no intro rate period std**| Binary numeric input, whether or not a mortgage does not include an introductory rate period.|
  |**property value std**|Numeric input, value of the mortgaged property.|
  |**term 360**|Binary numeric input, whether the mortgage is a standard 360 month mortgage (1) or a different type of mortgage (0). |

Table 1. Description of training data columns. 

- **Define the meaning of all engineered columns**: no engineered features.

### Evaluation Data

- **State the source of evaluation (or “test”) data**: [GW DNSC 6330 Class Github Test Data Zip](https://github.com/jphall663/GWU_rml/tree/master/assignments/data), email `jphall@gwu.edu` for more information
- **State the number of rows in evaluation (or “test”) data**: 19831 rows
- **State any differences in columns between training and evaluation (or “test”) data**: The test data does not contain the y-column/target variable 'high_priced'.

### Model Details

- **State the columns used as inputs in your group’s best remediated model**: 'debt_to_income_ratio_missing', 'conforming', 'term_360', 'intro_rate_period_std', 'debt_to_income_ratio_std', 'income_std', 'loan_amount_std', 'no_intro_rate_period_std'
- **State the columns used as targets in your group’s best remediated model**: 'high_priced'
- **State the type of your group’s best remediated model**: Explainable Boosting Machine (EBM)
- **State the software used to implement your group’s best remediated model**: Python, Interpret
- **State the version of the modeling software for your group’s best remediated model**: 3.11.12, 0.6.10
- **State the hyperparameters or other settings of your group’s best remediated model**:

```
rem_params = {'max_bins': 512, 'max_interaction_bins': 64, 'interactions': 10,
              'outer_bags': 8, 'inner_bags': 4, 'learning_rate': 0.05,
              'validation_size': 0.25, 'min_samples_leaf': 5, 'max_leaves': 3,
              'n_jobs': 4, 'early_stopping_rounds': 100, 'random_state': 12345}
```

### Quantitative Analysis

- **State the metrics used to evaluate your group’s best remediated model**: Area Under the Curve (AUC) and Adverse Impact Ratio (AIR)
- **State the values of the metrics for training, validation, and evaluation (or “test”) data – evaluation (or “test”) metrics come from the most recent class full evaluation results, link under Assignment 1.**: 

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.7494 | 0.7553  | 0.7502* |

Table 2. AUC values across data partitions. 

| Group | Validation AIR |
|-------|-----|
| Black vs. White | 0.8345 |
| Hispanic vs. White | 0.8765 |
| Asian vs. White | 1.098 |
| Female vs. Male | 1.245 |

Table 3. Validation AIR values for race and sex groups. 

- **Provide at least one plot or table from each weekly assignment for a total of at least six plots, that must include the global variable importance and partial dependence of your group’s best remediated model.**:

![image](https://github.com/user-attachments/assets/561e527a-1fc5-4d3e-8410-c00613ddcd57)

Figure 1. Histograms for data exploration from assignment 1.

![image](https://github.com/user-attachments/assets/76115d4c-9a4f-4629-ad40-ed22d3583015)  

Figure 2. Partial dependence of standardized property value on EBM predictions from assignment 2.

![image](https://github.com/user-attachments/assets/2455ca29-cfc9-430c-ae7a-ba406e01cb4e)

Figure 3. Global Feature Importance Plots from Assignment 3 

![image](https://github.com/user-attachments/assets/ed63a494-f523-42ca-a534-3e3c8979d827)

Figure 4.  Plot of model performance vs model bias from assignment 3. 

![image](https://github.com/user-attachments/assets/9f30165c-a525-42fc-8df1-2a63da0b25c8)

Figure 5. Global variable importance for H2O random forest model, highlighting income and intro rate period as top predictors from assignment 4.

![image](https://github.com/user-attachments/assets/5f0a77a2-8046-482c-952e-d5e3eb69f380)

Figure 6. Outlier analysis from assignment 5.

- **Address other alternative models considered**: We tried using the general linear model (GLM) with elastic net, monotonic gradient boosting machines (GBM) and extreme gradient boosting (XGBoost). The models tried can be found in [assigment 1](https://github.com/HannaCourtot/DNSC-6330---Responsible-Machine-Learning/blob/main/Group_5_assign_1.ipynb). However, our EBM model demonstrated the highest AUC and maintained an AIR above the 0.9 threshold, making it the most suitable choice for further implementation.

(**HINT**: Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv)

#### Correlation Heatmap

![Correlation Heatmap](Correlation_Matrix_for_Input_Features.png)

Figure 7. Correlation matrix for input features. 

### Ethical Considerations

- **Describe potential negative impacts of using your group’s best remediated model:**

1. Unpredictable Behavior on Unseen Inputs. <br>
The EBM model tends to misbehave when it encounters inputs outside the range seen during training—particularly at extreme values. This can result in overconfident or underconfident risk predictions. In a real-world lending context, this could lead to unjust loan denials or unfavorable interest rates for certain applicants, especially those with unusual financial profiles.

2. Lack of Monotonic Relationship with Income. <br>
The model does not consistently learn logical trends like “higher income implies lower risk.” In fact, due to EBM’s binning approach, it can create splits where risk appears to increase with income in certain ranges. This can confuse stakeholders and produce unfair outcomes for high-income applicants who might be wrongly classified as risky.

- **Describe potential uncertainties relating to the impacts of using your group’s best remediated model:**

1. Model Instability Across Runs. <br>
Even when using the same model configuration, outcomes varied based on how the data was split or randomized. Key metrics like AUC showed noticeable fluctuations between runs. This makes it difficult to confidently assess whether a model version is truly more reliable or simply benefited from favorable randomness.

2. Risk of Bias from Remediation Steps. <br>
During fairness remediation, we adjusted feature distributions and sampling strategies to improve metrics like AIR. However, these interventions may have unintentionally distorted real-world data patterns. As a result, the model’s performance on new, unbalanced populations remains uncertain and potentially less fair than intended.

* **Describe any unexpected or results encountered during training**

1. Outliers in Log-Loss Residuals. <br>
 A residual analysis revealed 21 data points with extremely high log-loss values (>7), indicating poor model fit. We removed these outliers to smooth training, but their presence highlighted how a small number of anomalous records can heavily influence EBM’s performance. This suggests a need for robust anomaly detection.

3. Fragility Under Economic Stress. <br>
In a simulated recession scenario, where income and property values were adjusted downward, the model’s AUC dropped dramatically from 0.7484 to 0.6045. This sharp decline shows that the model is not resilient to major shifts in economic conditions and could produce unreliable predictions during financial downturns.

