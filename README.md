# Predicting High Priced Loans Model Card

### Basic Information - DONE

- **Person or organization developing model**: Copyright (c) 2021 - 2025 Patrick Hall (jphall@gwu.edu), Hanna Courtot (Hanna.Courtot@gwu.edu), Elias Makanganise (eliasm@gwu.edu), Jabari Rose (Jabari.rose@gwmail.gwu.edu) and Pratyush Singhal (pratyush.singhal@gwu.edu)
- **Model creation date**: May, 2021
- **Model modification date**: May, 2025
- **Model version**: 2.0
- **License**: Apache License, Version 2.0; you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0. Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License. DISCLAIMER: These notebooks are not legal or compliance advice.
- **Model implementation code**: [Assignment 1.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_1/assign_1_template.ipynb), [Assignment 2.ipynb][
https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_2/assign_2_template.ipynb), [Assignment 3.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_3/assign_3_template.ipynb), [Assignment 4.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_4/assign_4_template.ipynb), [Assignment 5.ipynb](https://github.com/jphall663/GWU_rml/blob/master/assignments/assignment_5/assign_5_template.ipynb) and [Assignment 6.ipynb](https://github.com/jphall663/GWU_DNSC_6301_project)

### Intended Use - DONE
 
- **Describe the business value of your group’s best remediated model**: This model is not intended to generate any value for commercial/business purposes.
- **Describe how your group’s best remediated model is designed to be used**: This model is designed solely for educational purposes.
- **Describe the intended users for your group’s best remediated model**: This model is designed for students and individuals interested in learning about bias in machine learning models.
- **State whether your group’s best remediated model can or cannot be used for any additional purposes**: Our model cannot be used for any additional purposes. Any use beyond an educational example is out-of-scope.

### Training Data - DONE

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

- **Define the meaning of all engineered columns**: no engineered features.

### Evaluation Data - DONE

- **State the source of evaluation (or “test”) data**: [GW DNSC 6330 Class Github Test Data Zip](https://github.com/jphall663/GWU_rml/tree/master/assignments/data), email `jphall@gwu.edu` for more information
- **State the number of rows in evaluation (or “test”) data**: 19831 rows
- **State any differences in columns between training and evaluation (or “test”) data**: The test data does not contain the y-column/target variable 'high_priced'.

### Model Details - DONE

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

### Quantitative Analysis - STARTED

NOTE: You should briefly address your other models as “alternative approaches” in the Quantitative analysis section, and point to why your main model is a better choice.

- **State the metrics used to evaluate your group’s best remediated model**: Area Under the Curve (AUC) and Adverse Impact Ratio (AIR)
- **State the values of the metrics for training, validation, and evaluation (or “test”) data – evaluation (or “test”) metrics come from the most recent class full evaluation results, link under Assignment 1.**: 

NOTE: Use Train and Validation AUC from bottom assignment 5!

NOTE: Take average of all 5 AUC from assignment 5!

NOTE: Might need to run code for training AUC – run extra code to get this – Run “EVM perf” on the training instead of the validation, Test AUC is the average, take each fold AUC is the average of the 5, Assignment 3 full validation results!

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.7494 | 0.7553  | 0.7502* |

Table 1. AUC values across data partitions. 

| Group | Validation AIR |
|-------|-----|
| Black vs. White | 0.8345 |
| Hispanic vs. White | 0.8765 |
| Asian vs. White | 1.098 |
| Female vs. Male | 1.245 |

Table 2. Validation AIR values for race and sex groups. 

- **Provide at least one plot or table from each weekly assignment for a total of at least six plots, that must include the global variable importance and partial dependence of your group’s best remediated model.**:

- - ![image](https://github.com/user-attachments/assets/561e527a-1fc5-4d3e-8410-c00613ddcd57)
Fig 1 - Data Exploration Plots from Assignment 1 

- ![image](https://github.com/user-attachments/assets/76115d4c-9a4f-4629-ad40-ed22d3583015)  
Fig 2 – Partial dependence of standardized property value on EBM predictions.


  ![image](https://github.com/user-attachments/assets/ed63a494-f523-42ca-a534-3e3c8979d827)
Fig 3 Pareto Plot of Model Performance vs Model Bias 


- ![image](https://github.com/user-attachments/assets/9f30165c-a525-42fc-8df1-2a63da0b25c8)
Fig 4 – Global variable importance for H2O Random Forest model, highlighting income and intro rate period as top predictors.


 - ![image](https://github.com/user-attachments/assets/5f0a77a2-8046-482c-952e-d5e3eb69f380)
Fig 5 - Outlier Analysis


- **Address other alternative models considered**: We tried using the general linear model (GLM) with elastic net, monotonic gradient boosting machines (GBM) and extreme gadient boosting (XGBoost). The models tried can be found in [assigment 1](https://github.com/HannaCourtot/DNSC-6330---Responsible-Machine-Learning/blob/main/Group_5_assign_1.ipynb).

(**HINT**: Test AUC taken from https://github.com/jphall663/GWU_rml/blob/master/assignments/model_eval_2023_06_21_12_52_47.csv)

NOTE: Add something other than a heat map, use something more interesting!

#### Correlation Heatmap - DONE

![Correlation Heatmap](Correlation_Matrix_for_Input_Features.png)




Figure 1. Correlation matrix for input features. 

### Ethical Considerations

NOTE: only place you write a short paragraph about bias, performance can drop during a recession

- **Describe potential negative impacts of using your group’s best remediated model:**
From a technical point of view, our model has two big weaknesses. First, it struggles to give reliable results when it sees something very different from what it saw during training—especially at the extreme ends of the scoring scale. This means it might be way too confident or not confident enough when predicting risk. Second, the tool we used (Interpret-EBM) doesn’t handle increasing or decreasing trends in income and risk very well. So, even though it makes sense to think that “higher income = lower risk,” that logic can fall apart in certain income ranges and lead to confusing or inaccurate results.

These issues matter most for people who are right on the edge of being approved or denied—especially those with lower incomes or from minority backgrounds. That’s because their data often falls near the model’s weak spots. If the model wrongly labels someone as “high risk,” they might get denied a mortgage or be offered one with a high interest rate, making things worse for them financially. And during tough economic times, like a recession, the model’s accuracy can drop a lot—from an AUC of 0.75 down to 0.60—which means its predictions get even less reliable. Finally, if these flawed predictions are used in automated pricing systems, it can make things even worse by applying those errors across thousands of people—especially hurting the ones who are already at a disadvantage.

- **Describe potential uncertainties relating to the impacts of using your group’s best remediated model:**
  There are still a bunch of unknowns when it comes to how the model works behind the scenes. How well it performs can change just based on how it’s set up—for example, things like how we split the data, how many models we combine, and even the random number it starts with.  Just rerunning the same setup could make the model’s score go up or down noticeably.

Also, when we cleaned and rebalanced the data to make things more even, we may have accidentally introduced some bias. That means the model might not do a great job when it’s faced with new or different data that it hasn’t seen before.

In the real world, conditions can change fast. Things like interest rates or how people handle debt can shift, and if they do, the model might rely on outdated patterns that no longer apply. On top of that, some groups of people weren’t well represented in the data we trained on, so we’re not totally sure how well the model will work for them—which could lead to unfair results.

* **Describe any unexpected or results encountered during training**
During training, we ran into three notable surprises. First, a log-loss residual analysis revealed a pocket of extreme outliers—just 21 records with residuals above 7—so we removed them to steady the model’s learning curve. Second, the model proved fragile in a recession stress test: when we simulated downturn conditions, its AUC tumbled from 0.7484 to 0.6045, underscoring how sharply performance can erode under major data shifts. Finally, our attempt to impose a “higher-income ⇒ lower-risk” monotonic constraint hit a roadblock because Interpret-EBM doesn’t yet support true monotonicity; we therefore had to perform a manual bin review to prevent counter-intuitive splits.

Negative Impacts:

1. Unpredictable Behavior on Unseen Inputs
The EBM model tends to misbehave when it encounters inputs outside the range seen during training—particularly at extreme values. This can result in overconfident or underconfident risk predictions. In a real-world lending context, this could lead to unjust loan denials or unfavorable interest rates for certain applicants, especially those with unusual financial profiles.

2. Lack of Monotonic Relationship with Income
The model does not consistently learn logical trends like “higher income implies lower risk.” In fact, due to EBM’s binning approach, it can create splits where risk appears to increase with income in certain ranges. This can confuse stakeholders and produce unfair outcomes for high-income applicants who might be wrongly classified as risky.

▪ Uncertainties:

1. Model Instability Across Runs
Even when using the same model configuration, outcomes varied based on how the data was split or randomized. Key metrics like AUC showed noticeable fluctuations between runs. This makes it difficult to confidently assess whether a model version is truly more reliable or simply benefited from favorable randomness.

2. Risk of Bias from Remediation Steps
During fairness remediation, we adjusted feature distributions and sampling strategies to improve metrics like AIR. However, these interventions may have unintentionally distorted real-world data patterns. As a result, the model’s performance on new, unbalanced populations remains uncertain and potentially less fair than intended.

▪ Unexpected Results:

1. Outliers in Log-Loss Residuals
A residual analysis revealed 21 data points with extremely high log-loss values (>7), indicating poor model fit. We removed these outliers to smooth training, but their presence highlighted how a small number of anomalous records can heavily influence EBM’s performance. This suggests a need for robust anomaly detection.

2. Fragility Under Economic Stress
In a simulated recession scenario, where income and property values were adjusted downward, the model’s AUC dropped dramatically from 0.7484 to 0.6045. This sharp decline shows that the model is not resilient to major shifts in economic conditions and could produce unreliable predictions during financial downturns.

