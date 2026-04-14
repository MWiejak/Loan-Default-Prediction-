## **Problem Definition**

### **The Context:**

Retail banks rely heavily on home equity loans as a stable source of interest-based income. However, loan defaults and severe delinquencies result in non-performing assets (NPAs), which directly impact profitability, capital adequacy, and risk exposure. Beyond financial losses, high default rates also increase regulatory scrutiny and operational costs associated with recovery and collections.
While traditional loan underwriting relies on manual assessment of an applicant’s financial and credit profile, such processes are resource-intensive and often inconsistent across applicants. More importantly, manual decision-making may fail to scale efficiently with growing application volumes and can lead to suboptimal capital allocation — either by approving high-risk applicants or by rejecting creditworthy customers due to conservative judgment.
From a business perspective, there is a strong need for a data-driven, standardized, and interpretable credit risk assessment framework that can proactively identify high-risk applicants before loan approval, reduce default-related losses, and support fair and consistent lending decisions in compliance with regulatory guidelines.

### **The objective:**

The objective of this project is to develop a classification model that predicts the likelihood of a loan applicant defaulting on a home equity loan using historical underwriting and loan performance data.

From a business perspective, the model is intended to identify applicants who are likely to default before loan approval, thereby supporting proactive credit risk screening and reducing future non-performing assets.

In addition to predictive performance, the model aims to:
* Provide interpretable and transparent decision support for credit underwriting
* Identify the most influential factors driving loan default risk
* Enable the bank to make consistent, fair, and data-driven loan approval decisions


### **The key questions:**

The analysis seeks to answer the following key questions:
* Which applicant attributes and credit-related factors are most indicative of loan default risk?
* Can a predictive model effectively identify potential defaulters while minimizing costly missed defaults?
* How do different modeling techniques (logistic regression, decision trees, and random forests) compare in terms of predictive performance, interpretability, and practical deployment feasibility?
* Which variables remain consistently important across different modeling approaches?
* What modeling approach provides the best balance between business risk mitigation and regulatory interpretability?


### **The problem formulation**:

This problem is formulated as a supervised binary classification task, where the goal is to predict whether a loan applicant will default on a home equity loan based on information available at the time of loan approval.
* Target variable:
`BAD`
    * 1 → Applicant defaulted or became severely delinquent
    * 0 → Loan was successfully repaid

* Input variables:

Financial attributes, credit history indicators, employment-related details, and loan characteristics recorded during the underwriting process.
The output of the model is a predicted probability of default that can be used to support loan approval decisions. From a business perspective, the cost of approving a high-risk applicant (false negative) is substantially higher than rejecting a low-risk applicant (false positive), making sensitivity to default risk a key operational concern.

Accordingly, **ROC–AUC is used as the primary metric for model comparison and selection**, as it provides a threshold-independent measure of how well models rank applicants by default risk under class imbalance. **Recall for defaulters (BAD = 1)** is reported at the default classification threshold to illustrate operational behavior and to reflect the higher cost of approving a borrower who later defaults, rather than to optimize a specific approval cutoff.

## **Data Description:**

The dataset used in this analysis is the Home Equity (HMEQ) dataset, which contains historical information on applicants who applied for home equity loans. The data was collected during the loan underwriting process and includes both applicant characteristics and loan-related attributes available at the time of loan approval. Additionally, the dataset records subsequent loan performance, making it suitable for building predictive credit risk models.
The dataset consists of 5,960 loan records and 13 variables, where each row represents a unique loan applicant. Out of these variables, 12 are predictor variables and one is the target variable (BAD), which indicates whether the applicant ultimately defaulted or became severely delinquent on the loan.
The variables in the dataset capture a combination of:

Loan-related financial information

Property valuation details

Applicant employment characteristics

Credit history indicators

Variable Description

* `BAD` - Binary target variable indicating loan performance
    * Values: 
        * 1 → Applicant defaulted or became severely delinquent
        * 0 → Loan was successfully repaid
* `LOAN` - Amount of the loan approved by the bank
* `MORTDUE` - Amount due on the applicant’s existing mortgage
* `VALUE` - Current market value of the property securing the loan
* `REASON` - Purpose of the loan
    * Values:
        * HomeImp → Home improvement
        * DebtCon → Debt consolidation
* `JOB` - Type of job held by the applicant (e.g., managerial, self-employed, office worker)
* `YOJ` - Number of years the applicant has been employed at their current job
* `DEROG` - Number of major derogatory credit reports, indicating serious delinquencies or late payments
* `DELINQ` - Number of delinquent credit lines, where payments were overdue by 30 to 60 days
* `CLAGE` - Age of the oldest credit line in months
* `NINQ` - Number of recent credit inquiries made by the applicant
* `CLNO`- Total number of existing credit lines
* `DEBTINC` - Debt-to-income ratio, calculated as total monthly debt payments divided by gross monthly income
