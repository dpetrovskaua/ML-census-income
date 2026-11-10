# ML-census-income
ED Mentorship Program: ML Engineering

1. ### **Project summary:**
The task was to predict whether a person earns more than 50K per year from census-style attributes (the Adult dataset), 
based on features of every person (some of which were missing). 
The data is the Adult dataset (OpenML name adult, version 2), with 48,842 rows, 14 features and a binary target (<=50K / >50K).

2. ### **How to run. Python version and the random seed.**
   1. `git clone https://github.com/dpetrovskaua/ML-census-income.git`
   2. `cd ML-census-income`
   3. `python -m venv .venv`
   4. `Windows: .venv\Scripts\activate`  /  `macOS/Linux: source .venv/bin/activate`
   5. `pip install -r requirements.txt`
   6. `jupyter notebook`

Requires Python 3.10+
(My ver: 3.13)

Seed: 42

3. ### **Results: Model comparison and recommendation of best-performance model**
| Model                                 | Accuracy | Precision | Recall | F1    | ROC AUC |
|---------------------------------------|----------|-----------|--------|-------|-------|
| Dummy                                 | 0.761    | 0.000     | 0.000  | 0.000 | 0.500 |
| Logic regression                      | 0.852    | 0.741     | 0.589  | 0.656 | 0.904 |
| RandomForest                          | 0.860    | 0.743     | 0.636  | 0.685 | 0.904 |
| HistGradientBoosting                  | 0.875    | 0.787     | 0.655  | 0.715 | 0.929 |
| PyTorch MLP                           | 0.859    | 0.748     | 0.619  | 0.677 | 0.912 |
| Neural network (MLP): mean of 5 seeds | 0.858    | 0.746     | 0.619  | 0.676 | 0.912 |


I recommend HistGradientBoostingClassifier as a model of choice for this kind of project,
since it achieves the highest metrics, while handling tabular feature interactions effectively.

4. ### **Key findings:**
    1. Baseline: 76.1% of people earn <=50K, so always predicting that class gives 76.1% accuracy. Accuracy alone is a weak metric here, which is why precision, recall, F1 and ROC AUC are also taken into account.
    2. Workclass (2,799), occupation (2,809) and native-country (857) were missing. They are stored as NaN (no ? strings were found) and are imputed inside the pipeline.
    3. Useful features: Hours-per-week: the target is the share per group: 7% for 1-20 hours, 19% for 21-40, 40% for 41-60 and 36% for 61-99. So working more than 40 hours is linked to a higher chance of earning >50K. 
   Capital-gain: 61.7% earn >50K when capital-gain > 0, against 20.5% otherwise. Worth or mention: capital-gain max is 99999, which looks like a top-coded value, to assure individuals of confidentiality.
    4. Categories with the most weight were marital-status (drop 0.094), capital-gain (0.062), age (0.045) and education-num (0.032) which met the expectations. What surprised me, is that hours-per-week feature did not have that much weight as i expected it too

5. ### **Limitations and ethics:**
The data is a 1994 US census sample, so it does not describe incomes today. Recall for high earners is only 0.66, so about one third of them are missed.
The data contains sex, race, marital-status and native-country. The share earning >50K is 30.4% for men and 10.9% for women, and 25.4% for White against 12.1% for Black people. 
A model trained on this data learns these gaps and could reproduce them, for example in a loan or hiring decision, which would be discrimination. 
Dropping the sensitive columns would not fully remove the risk, because other features (such as marital status and occupation) are correlated with them.

What to check before real use:
* Data Age: Because the dataset is from 1994, it does not reflect modern economic conditions and societal morals. 
The model would need to be retrained on up-to-date census data before any deployment.   
* Per-group metrics: Evaluate the model's performance (such as precision, recall, and false positive rates) separately for different demographic groups to ensure fairness. 
This ensures the model does not misclassify or harm specific populations based on features like race or sex. 

6. ### **What I learned and what was hard:**
    The hardest part was not the new libraries, materials on which where easy to find online, but new format of a task and new field overall. My previous assignments in UNI had much more simple structure, without the analysis of results.
One of other difficulties were independent learning of libraries and functions without use of AI. Not using it on this task was a challenge, but I understand that using it does not give me the skils I need.

Learned new Jupiter environment that was much easier to use than i expected, due to negative experience in past (browser version suuuckksss).

### After-Feedback
Explanation for "copied from tg" lines: The task brief for First Assignment contained Tips for beginners, from which these lines were taken from