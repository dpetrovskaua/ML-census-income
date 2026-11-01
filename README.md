# ML-census-income
ED Mentorship Program: ML Engineering

1. ### **Project summary: one paragraph on the problem and the dataset.**
The task was to predict whether a person earns more than 50K per year from census-style attributes (the Adult dataset), 
based on features of every person (some of which were missing). 
The data is the Adult dataset (OpenML name adult, version 2), with 48,842 rows, 14 features and a binary target (<=50K / >50K).

2. ### **How to run: exact commands to create the environment, install dependencies and run the notebooks, plus the Python version and the random seed.**
   1. `git clone https://github.com/dpetrovskaua/ML-census-income.git`
   2. `cd ML-census-income`
   3. `python -m venv .venv`
   4. `Windows: .venv\Scripts\activate`  /  `macOS/Linux: source .venv/bin/activate`
   5. `pip install -r requirements.txt`
   6. `jupyter notebook`

Python version: 3.13

Seed: 42

3. ### **Results: the final comparison table (all models, the same metrics) and a one-sentence recommendation of which model you would use and why.**
![img_1.png](img_1.png)
![img.png](img.png)
![learning_curves.png](learning_curves.png)
![img_4.png](img_4.png)
![img_2.png](img_2.png)
I would use tuned gradient boosting for it's efficiency, intuitively easy concept for beginners in the field.

4. ### **Key findings: three to five short points from your exploration and error analysis.**
    1. Baseline: 76.1% of people earn <=50K, so always predicting that class gives 76.1% accuracy. Accuracy alone is a weak metric here, which is why precision, recall, F1 and ROC AUC are also taken into account.
    2. Workclass (2,799), occupation (2,809) and native-country (857) were missing. They are stored as NaN (no ? strings were found) and are imputed inside the pipeline.
    3. Useful features: marital status (44.6% of married-civ-spouse people earn >50K against 4.5% of never-married), education, and capital gain (61.7% earn >50K when it is non-zero against 20.5% when zero, although 91.7% of values are zero).
    4. Categories with the most weight were marital-status (drop 0.094), capital-gain (0.062), age (0.045) and education-num (0.032) which met the expectations. What surprised me, is that hours-per-week feature did not have that much weight as i expected it too

5. ### **Limitations and ethics: what the model cannot be trusted for, which risks the sensitive attributes create, and what you would check before using it for any real decision.**
The data is a 1994 US census sample, so it does not describe incomes today. Recall for high earners is only 0.66, so about one third of them are missed.
The data contains sex, race, marital-status and native-country. The share earning >50K is 30.4% for men and 10.9% for women, and 25.4% for White against 12.1% for Black people. 
A model trained on this data learns these gaps and could reproduce them, for example in a loan or hiring decision, which would be discrimination. 
Dropping the sensitive columns would not fully remove the risk, because other features (such as marital status and occupation) are correlated with them.

6. ### **What I learned and what was hard:**
    The hardest part was not the new libraries, materials on which where easy to find online, but new format of a task and new field overall. My previous assignments in UNI had much more simple structure, without the analysis of results.
One of other difficulties were independent learning of libraries and functions without use of AI. Not using it on this task was a challenge, but I understand that using it does not give me the skils I need.

Learned new Jupiter environment that was much easier to use than i expected, due to negative experience in past (browser version suuuckksss).

