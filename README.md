# Credit_Line_Increase Model Card
DNSC_6301

### Basic Information

*  **Authors : Students at the George Washington University School of Business**: Group 17 : Tivon Johnson `tivonj`, Harsharan Gorli `Harsh-5`, Andrew Levy `Arl34`, Yingying Liu `Yingying0201`
* **Model date**: August, 2021
* **Model version**: 0.22.2.post1
* **License**: Apache 2.0 License
* **Model implementation code**: [Credit_Line_Increase.ipynb](Credit_Line_Increase.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Professors, Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: This model is for educational purposes and not intended to evaluate real-world credit worthiness.

### Training Data

* Data dictionary: 

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

* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model Details
* **Columns used as inputs in the final model:** Limit_BAL,PAY_0, PAY_2, PAY_3, PAY_4, PAY_5, PAY_6,BILL_AMT1, BILL_AMT2, BILL_AMT3, BILL_AMT4, BILL_AMT5, BILL_AMT6,PAY_AMT1, PAY_AMT2, PAY_AMT3, PAY_AMT4, PAY_AMT5, PAY_AMT6
* **Column(s) used as target(s) in the final model:** DELINQ_NEXT
* **Type of model:** Decision Tree
* **Software used to implement the model:** Python 3.6+, Google Colab
* **Version of the modeling software:** v0.2.5.
* **Hyperparameters or other settings of your model:** max_depth = 12

### Quantitative analysis:
* **Metrics used to evaluate the model and final figures: 
  * Training AUC: 0.78
  * Validation AUC: 0.75
  * Test AUC: 0.74
  * Asian-to-White AIR: 1.00
  * Black-to-White AIR: 0.85
  * Female-to-Male AIR: 1.02
  * Hispanic-to-White AIR: 0.83
* **Iteration Plot of the final model (inclusive of Training AUC, Validation AUC and Hispanic-to-White AIR: ![image](https://user-images.githubusercontent.com/12841463/131274193-1f068b6a-2d40-4776-884e-1c44e79dfc1b.png)


### Ethical considerations:
* **Potential negative impacts of the model:
  * The model can lead to descrimination.  While the model may be accurate, accuracy does not always imply the model is unbiased.  Numerous factors that can lead to delinquency unfortunately can potentially be linked to race or gender.  Bias testing was implemented in order to mitigate any potential descrimination.
  *  According to variable importance chart, the most recent payment is the primary factor the decision tree splits on.  As we have seen in the pandemic, the people that are affected most by economic disruptions are lower income individuals, who would be most in need of potential increased credit lines.
* **Potential uncertainties relating to the impact of using the model:
  * One uncertainty could the off-label use of the model.  While it is the intention of the group to use the model specifically for extending a credit line, there is the potential of others to use it where it has not been tested.
  * Another uncertainty can be the accuracy of the data itself.  Over time, the data itself can become dated, leading to inaccurate results.
* **Other unexpected results:
  * The model still has bias and hard to fix it based on the dataset.

