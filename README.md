### License

Copyright (c) 2021 - 2025 Patrick Hall (jphall@gwu.edu), Hanna Courtot (Hanna.Courtot@gwu.edu), Elias Makanganise (eliasm@gwu.edu), Jabari Rose (Jabari.rose@gwmail.gwu.edu) and Pratyush Singhal (pratyush.singhal@gwu.edu)

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

DISCLAIMER: This notebook is not legal or compliance advice.

# Predicting High Priced Loans Model Card

### Basic Information - STARTED

- **Person or organization developing model**: Patrick Hall (jphall@gwu.edu), Hanna Courtot (Hanna.Courtot@gwu.edu), Elias Makanganise (eliasm@gwu.edu), Jabari Rose (Jabari.rose@gwmail.gwu.edu) and Pratyush Singhal (pratyush.singhal@gwu.edu)
- **Model creation date**: August, 2021
- **Model modification date**: April, 2025
- **Model version**: 1.0
- **License**: MIT
- **Model implementation code**: [DNSC_6301_Example_Project.ipynb](https://github.com/jphall663/GWU_DNSC_6301_project/blob/main/DNSC_6301_Example_Project.ipynb)

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
  | Column | description |
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

NOTE: UPDATE WITH Data dictionary is in assignment 1 

- **Data dictionary**:

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

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

NOTE: Use Validation and test AUC from bottom assignment 5!
NOTE: Take average of all 5 AUC from assignment 5!
NOTE: Might need to run code for training AUC – run extra code to get this – Run “EVM perf” on the training instead of the validation, Test AUC is the average, take each fold AUC is the average of the 5, Assignment 3 full validation results!

| Train AUC | Validation AUC | Test AUC |
| ------ | ------- | -------- |
| 0.7494 | 0.7891  | 0.7687* |

Table 1. AUC values across data partitions. 

| Group | Validation AIR |
|-------|-----|
| Black vs. White | 0.8345 |
| Hispanic vs. White | 0.8765 |
| Asian vs. White | 1.098 |
| Female vs. Male | 1.245 |

Table 2. Validation AIR values for race and sex groups. 

- **Provide at least one plot or table from each weekly assignment for a total of at least six plots, that must include the global variable importance and partial dependence of your group’s best remediated model.**:

- ![image](https://github.com/user-attachments/assets/76115d4c-9a4f-4629-ad40-ed22d3583015)
  Fig 2 – Partial dependence of standardized property value on EBM predictions.
  
- ![image](https://github.com/user-attachments/assets/9f30165c-a525-42fc-8df1-2a63da0b25c8)
  Fig 4 – Global variable importance for H2O Random Forest model, highlighting income and intro rate period as top predictors.
- 
- ![image](https://github.com/user-attachments/assets/63e0dde2-606d-4eb6-ab0e-8ccddaa8dd03)



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

The EBM model can behave unpredictably when exposed to data far from its training distribution, especially at extreme values. This may lead to inaccurate risk scores that unfairly penalize applicants.

The model doesn’t naturally follow expected relationships like “higher income → lower risk.” In some income ranges, this causes misleading predictions that can disadvantage qualified borrowers.

▪ Uncertainties:

Model results vary depending on data splits, initialization, and random seed—retraining the same configuration can yield noticeably different AUC scores.

Fairness interventions like data rebalancing may introduce unintended bias. This raises uncertainty about how well the model will generalize to new or diverse populations.

▪ Unexpected Results:

A log-loss residual check revealed 21 records with unusually high errors. Removing them helped stabilize training but also highlighted sensitivity to anomalies.

When tested under simulated recession conditions, the model’s AUC dropped from 0.7484 to 0.6045, showing that its reliability decreases sharply under stress.


