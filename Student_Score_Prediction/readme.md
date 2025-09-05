# Student Score Prediction

A simple linear regression project that predicts student exam scores based on study hours. I built this to see if there's really a direct relationship between how much students study and how well they perform on exams.

## What this project does

- [The question](#the-question)
- [The data](#the-data)
- [The approach](#the-approach)
- [What I found](#what-i-found)
- [The results](#the-results)
- [How to run it](#how-to-run-it)

## The question

I was curious about whether there's a straightforward relationship between study time and exam performance. It seems obvious that more studying should lead to better scores, but I wanted to see if the data actually supports this assumption and how strong that relationship really is.

The goal was to build a simple model that could predict exam scores based mainly on study hours, using linear regression to find the best-fit line through the data.

## The data

I used a dataset with 6,378 students that includes:
- **Hours_Studied**: How many hours each student studied
- **Exam_Score**: Their final exam score (0-100)
- Plus 18 other factors like attendance, parental involvement, sleep hours, etc.

The dataset was pretty clean - just had to remove duplicates and handle a few missing values. I focused on the study hours and exam scores since that's what I was most interested in exploring.

## The approach

I kept it simple and used linear regression, which tries to draw a straight line that best fits the data. The idea is that if there's a relationship between study hours and scores, we should be able to find a line that captures it.

The process was straightforward:
1. **Split the data** - 80% for training, 20% for testing
2. **Train the model** - Find the best-fit line through the training data
3. **Make predictions** - Use the line to predict scores for the test set
4. **Evaluate performance** - See how close the predictions were to actual scores

I used several metrics to measure how well the model worked:
- **MAE** (Mean Absolute Error): Average difference between predicted and actual scores
- **RMSE** (Root Mean Square Error): Penalizes larger errors more heavily
- **R²** (R-squared): How much of the variation in scores the model explains

## What I found

The results were interesting but not as strong as I expected. The model found a positive relationship between study hours and exam scores, but it wasn't as strong as I thought it would be.

**Key findings:**
- **Slope**: 0.29 - This means each additional hour of studying is associated with about 0.29 points higher on the exam
- **Intercept**: 61.49 - A student who studies 0 hours would be predicted to score about 61.5 points
- **R²**: 0.21 - The model only explains about 21% of the variation in exam scores

This suggests that while study hours do matter, there are a lot of other factors that influence exam performance that aren't captured by just looking at study time.

## The results

Here's how the model performed:

| Metric | Value | What it means |
|--------|-------|---------------|
| **MAE** | 2.53 | On average, predictions are off by about 2.5 points |
| **RMSE** | 3.51 | Larger errors are penalized more heavily |
| **R²** | 0.21 | The model explains 21% of score variation |

The scatter plot shows the relationship clearly - there's definitely a positive trend, but there's also a lot of scatter around the line. Some students who studied a lot still got low scores, while others who studied less got high scores.

## How to run it

You'll need these libraries:
```bash
pip install kaggle pandas numpy matplotlib seaborn scikit-learn
```

The notebook downloads the dataset from Kaggle, so you'll need to:
1. Upload your Kaggle API key (kaggle.json)
2. Run all the cells to see the complete analysis

The notebook covers:
- **Data loading**: Downloads and explores the student performance dataset
- **Data cleaning**: Removes duplicates and handles missing values
- **Exploratory analysis**: Creates scatter plots and correlation heatmaps
- **Model training**: Fits a linear regression model
- **Evaluation**: Tests the model and calculates performance metrics
- **Visualization**: Shows the regression line and predictions

## Key insights

The most important thing I learned is that study hours are just one piece of the puzzle. While there is a positive relationship between studying and exam performance, it's not as strong as I expected. The R² of 0.21 means that 79% of the variation in exam scores is due to other factors.

This makes sense when you think about it - exam performance depends on so many things: natural ability, test anxiety, quality of studying (not just quantity), sleep, stress, the specific exam content, etc. Just counting study hours doesn't capture the full picture.

The model is still useful though. It gives us a baseline prediction, and the slope tells us that studying does have a measurable impact. For every hour a student studies, they can expect to score about 0.29 points higher on average.

## Limitations and next steps

This simple model has obvious limitations:
- **Only one feature**: Study hours alone can't capture all the complexity of student performance
- **Linear relationship**: Assumes the relationship is always linear, which might not be true
- **Other factors**: Ignores important variables like study quality, motivation, learning style, etc.
