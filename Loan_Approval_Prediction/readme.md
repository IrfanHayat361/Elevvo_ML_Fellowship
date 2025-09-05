# Loan Approval Prediction

A machine learning project that predicts whether someone applying for a loan will get approved or denied. Built this to understand how different factors like income, credit history, and personal details influence loan decisions.

## What's in this project

- [What I built](#what-i-built)
- [The data](#the-data)
- [How to run it](#how-to-run-it)
- [Results](#results)
- [What I learned](#what-i-learned)
- [Tech stack](#tech-stack)

## What I built

This project tackles loan approval prediction using several machine learning models. The tricky part wasn't just building the models - it was dealing with imbalanced data where most loans get approved, making it easy for a model to just predict "approved" every time and look good.

I used SMOTE to balance the classes and focused on metrics like precision and recall instead of just accuracy, since getting loan predictions wrong has real consequences.

## The data

I worked with 1,000 loan application records. Here's what each record contains:

- **Personal info**: Gender, marital status, number of dependents
- **Education & employment**: Education level, self-employed status  
- **Financial details**: Applicant income, co-applicant income, loan amount, loan term
- **Credit & property**: Credit history, property area type
- **Target**: Whether the loan was approved (Y/N)

The data had some missing values (about 5% across different fields) which I filled in using the most common values for categories and median for numbers. Originally, about 70% of loans were approved and 30% denied, but after using SMOTE to balance things out, I had equal numbers of both classes.

## How to run it

You'll need Python 3.7+ and these libraries:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
```

Then just open the Jupyter notebook and run all the cells:
```bash
jupyter notebook Loan_Approval_Prediction.ipynb
```

The notebook walks through everything step by step - data cleaning, handling missing values, encoding categorical variables, scaling features, balancing the classes with SMOTE, and finally training and comparing the models.

## Results

I tested four different models and here's how they performed:

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| **Random Forest** | **74%** | **0.74** | **0.74** | **0.74** |
| Decision Tree | 67% | 0.67 | 0.67 | 0.67 |
| SVM | 68% | 0.68 | 0.68 | 0.68 |
| Logistic Regression | 54% | 0.54 | 0.54 | 0.54 |

Random Forest came out on top. I was a bit surprised that logistic regression didn't do better - I thought it would at least give a decent baseline, but it really struggled with the balanced dataset after SMOTE. The decision tree was okay but showed signs of overfitting, and SVM was solid but not exceptional.

## Tech stack

- Python 3.12
- Pandas for data manipulation
- NumPy for numerical operations
- Scikit-learn for machine learning
- Imbalanced-learn for SMOTE
- Matplotlib & Seaborn for visualizations
- Jupyter Notebook for development

## What I learned

The biggest challenge was definitely the imbalanced data. At first glance, 70% approved vs 30% denied doesn't seem terrible, but it's enough to make a model just predict "approved" every time and still look pretty good on accuracy.

I tried a few different approaches for handling missing values - mode for categorical variables and median for numerical ones seemed to work well. For encoding, I went with label encoding instead of one-hot encoding to keep the feature space manageable.

Feature scaling was crucial too. Income values were way higher than other features, so without standardization, the models would have been biased toward income just because of the scale.

SMOTE was a game changer. It created synthetic examples for the minority class (denied loans) without just duplicating existing data. This helped the models actually learn patterns for both classes instead of ignoring the denied loans.

The random forest result makes sense in hindsight - it's good at handling mixed data types and doesn't overfit as much as a single decision tree. Plus, you can actually see which features matter most, which is useful for understanding what drives loan decisions.
