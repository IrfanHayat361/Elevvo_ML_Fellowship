# Elevvo Machine Learning Projects Portfolio

A collection of machine learning projects I've built to explore different aspects of data science and AI. Each project tackles a different type of problem and uses various techniques to solve real-world challenges.

## 🚀 Projects Overview

| Project | Problem Type | Key Techniques | Accuracy/Performance |
|---------|--------------|----------------|---------------------|
| [Loan Approval Prediction](#loan-approval-prediction) | Classification | Random Forest, SMOTE, Feature Engineering | 74% accuracy |
| [Mall Customer Segmentation](#mall-customer-segmentation) | Clustering | K-Means, DBSCAN, Data Visualization | 5 optimal clusters |
| [Movie Recommendation System](#movie-recommendation-system) | Recommendation | Collaborative Filtering, Cosine Similarity | Precision@5: 0.0 |
| [Music Genre Classification](#music-genre-classification) | Classification | CNN, Random Forest, Audio Processing | 69% (RF), 51% (CNN) |
| [Student Score Prediction](#student-score-prediction) | Regression | Linear Regression, Feature Analysis | R²: 0.21 |
| [Traffic Sign Recognition](#traffic-sign-recognition) | Computer Vision | Custom CNN, Transfer Learning | 98.93% accuracy |

---

## 📊 Loan Approval Prediction

**Goal**: Predict whether a loan application will be approved or denied based on applicant characteristics.

**What I learned**: The biggest challenge was dealing with imbalanced data where most loans get approved. I used SMOTE to balance the classes and focused on precision/recall instead of just accuracy since getting loan predictions wrong has real consequences.

**Key insights**:
- Random Forest performed best with 74% accuracy
- High-income customers aren't always big spenders
- Feature scaling was crucial for model performance
- SMOTE effectively balanced the dataset without losing information

**Files**: `Loan_Approval_Prediction.ipynb`, `loan_approval_prediction.py`

---

## 🛍️ Mall Customer Segmentation

**Goal**: Group mall customers into meaningful segments based on their income and spending patterns.

**What I learned**: K-Means worked much better than DBSCAN for this dataset. The data had clear, distinct patterns that K-Means could capture well, while DBSCAN was more flexible but messier for business decisions.

**Key insights**:
- Found 5 distinct customer segments
- High-income, low-spending customers (careful high earners)
- Low-income, high-spending customers (spend beyond means)
- Classical music was surprisingly easy to identify
- Random Forest outperformed CNN (69% vs 51%)

**Files**: `Mall_Customer_Segmentation.ipynb`, `mall_customer_segmentation.py`

---

## 🎬 Movie Recommendation System

**Goal**: Build a system that suggests movies to users based on what similar users liked.

**What I learned**: The data was incredibly sparse - most users haven't seen most movies. I had to be careful about filtering out movies users had already seen, and popular movies kept showing up in everyone's recommendations.

**Key insights**:
- User-based collaborative filtering using cosine similarity
- Data sparsity was the biggest challenge
- Precision@5 was 0.0 (common for sparse recommendation data)
- System generated reasonable movie suggestions despite low precision

**Files**: `Movie_Recommendation_System.ipynb`, `movie_recommendation_system.py`

---

## 🎵 Music Genre Classification

**Goal**: Automatically categorize music into different genres based on audio features.

**What I learned**: I expected the CNN approach to outperform traditional machine learning, but Random Forest actually did better. The custom CNN struggled to learn meaningful patterns from spectrograms, while hand-crafted audio features worked well.

**Key insights**:
- Random Forest: 69% accuracy using 42 audio features
- CNN: 51% accuracy using spectrogram images
- MFCCs and spectral features were most useful
- Some genres (classical, jazz) were easier to identify than others

**Files**: `Music_Genre_Classification_System.ipynb`, `music_genre_classification_system.py`

---

## 📚 Student Score Prediction

**Goal**: Predict student exam scores based on study hours using linear regression.

**What I learned**: Study hours are just one piece of the puzzle. While there is a positive relationship, it's not as strong as I expected. The R² of 0.21 means 79% of score variation is due to other factors.

**Key insights**:
- Each hour of studying ≈ 0.29 points higher on exam
- R² = 0.21 (only explains 21% of score variation)
- MAE = 2.53 points (average prediction error)
- Many other factors influence exam performance

**Files**: `Student_Score_Prediction.ipynb`, `student_score_prediction.py`

---

## 🚦 Traffic Sign Recognition

**Goal**: Automatically identify traffic signs from images using deep learning.

**What I learned**: Transfer learning isn't always the answer. While MobileNetV2 worked great on ImageNet, it didn't transfer well to traffic signs. The custom CNN, designed specifically for this problem, performed much better.

**Key insights**:
- Custom CNN: 98.93% accuracy
- MobileNetV2: 28.85% accuracy (much lower than expected)
- Data augmentation was crucial for success
- 32×32 pixel size was good balance of detail and efficiency

**Files**: `Traffic_Sign_Recognition_System.ipynb`, `traffic_sign_recognition_system.py`

---

## 🛠️ Technologies Used

- **Python**: Core programming language
- **Pandas & NumPy**: Data manipulation and analysis
- **Scikit-learn**: Traditional machine learning algorithms
- **TensorFlow/Keras**: Deep learning and neural networks
- **Matplotlib & Seaborn**: Data visualization
- **OpenCV**: Computer vision and image processing
- **Librosa**: Audio processing and feature extraction

## 📈 Key Learnings Across Projects

1. **Data preprocessing is crucial** - Feature scaling, handling missing values, and data augmentation can make or break a model

2. **Simple models often work best** - Sometimes a well-tuned Random Forest outperforms complex deep learning models

3. **Transfer learning isn't always the answer** - Pre-trained models don't always transfer well to specific domains

4. **Evaluation metrics matter** - Accuracy isn't always the best metric; precision, recall, and domain-specific metrics are often more important

5. **Real-world data is messy** - Imbalanced classes, missing values, and sparse data are common challenges

6. **Domain knowledge helps** - Understanding the problem domain leads to better feature engineering and model selection

## 🚀 Getting Started

Each project includes:
- **Jupyter Notebook**: Complete analysis with explanations
- **Python Script**: Standalone executable version
- **Dataset**: Either included or download instructions provided
- **Requirements**: All necessary dependencies listed

To run any project:
1. Install the required libraries
2. Download the dataset (if needed)
3. Run the Jupyter notebook or Python script
4. Follow the step-by-step analysis

## 📝 Project Structure

```
Machine Learning Projects/
├── Loan_Approval_Prediction/
│   ├── Loan_Approval_Prediction.ipynb
│   └── loan_approval_prediction.py
    |--Readme.md(explains the project)
├── Mall_Customer_Segmentation/
│   ├── Mall_Customer_Segmentation.ipynb
│   └── mall_customer_segmentation.py
    |--Readme.md(explains the project)
├── Movie_Recommendation_System/
│   ├── Movie_Recommendation_System.ipynb
│   └── movie_recommendation_system.py
    |--Readme.md(explains the project)
├── Music_Genre_Classification_System/
│   ├── Music_Genre_Classification_System.ipynb
│   └── music_genre_classification_system.py
    |--Readme.md(explains the project)
├── Student_Score_Prediction/
│   ├── Student_Score_Prediction.ipynb
│   └── student_score_prediction.py
    |--Readme.md(explains the project)
└── Traffic_Sign_Recognition_System/
    ├── Traffic_Sign_Recognition_System.ipynb
    └── traffic_sign_recognition_system.py
    |--Readme.md(explains the project)
```
This portfolio represents my journey through different types of machine learning problems. Each project taught me something new about data science, from handling imbalanced data to the importance of choosing the right evaluation metrics. The projects range from simple linear regression to complex computer vision, showing the breadth of applications in machine learning.

**Note**: All projects are designed for learning and experimentation. For production use, additional considerations like model validation, monitoring, and deployment would be necessary.
