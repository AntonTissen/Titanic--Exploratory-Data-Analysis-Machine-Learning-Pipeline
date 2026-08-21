🚢 Titanic – Machine Learning Classification Study
Predicting survival on the Titanic using 6 different ML algorithms, feature engineering, and in-depth EDA.

PythonScikit-LearnPandasJupyter

🎯 Project Goal
The goal of this project is to build and compare multiple Machine Learning models that predict whether a passenger survived the Titanic disaster — based on demographic and travel information.

This is not a quick copy-paste notebook. Every step of the pipeline was built from scratch with a deep focus on understanding the data before modeling it.

📊 Model Comparison Results
Rank	Model	Accuracy
🥇	Gradient Boosting Classifier	86.0 %
🥈	Logistic Regression	79.3 %
🥈	Random Forest Classifier	79.3 %
🥉	Decision Tree Classifier	78.2 %
Support Vector Machine (SVM)	70.4 %
K-Nearest Neighbors (KNN)	69.8 %
📌 Baseline (predicting "everyone dies"): ~61.6 % — all models beat this significantly.

Model Comparison

🔍 Key Insights from EDA
Before writing a single line of model code, the data was explored carefully. Here are the most striking findings:

🚻 Gender was the strongest predictor
Women: 74.2 % survival rate
Men: 18.9 % survival rate
"Women and children first" was not just a saying — the data proves it.

Survival by Gender

🎫 Class & Gender combined
Even a wealthy man in 1st class (36.9 %) had a lower survival chance than a poor woman in 3rd class (50.0 %). Gender dominated social status.

Survival by Class and Gender

🏠 Cabin Registration mattered
Has Cabin	Survival Rate
No (0)	30.0 %
Yes (1)	66.7 %
Passengers with a registered cabin number had more than double the survival rate — even within the same ticket class.

👨‍👩‍👧 The Family Size Sweet Spot
Traveling alone or in very large groups was dangerous:

Family Size	Survival Rate
1 (Alone)	30.4 %
2–4 (Small family)	55–72 %
5+ (Large family)	< 20 %
🛠️ Full Pipeline
1. Exploratory Data Analysis (EDA)
Identified missing values: Age (177), Cabin (687), Embarked (2)
Analyzed distributions, survival rates and correlations
2. Feature Engineering
New Feature	Logic
Title	Extracted from passenger names (Mr, Mrs, Miss, Master, Rare)
Has_Cabin	1 if cabin was registered, 0 if not
Family_Size	SibSp + Parch + 1
3. Data Cleaning (Imputation)
Age: Missing values filled with the median age per title group (e.g. "Master" = young boys → median ~5 years)
Embarked: Filled with the most frequent port (Southampton)
Cabin: Converted to binary Has_Cabin feature
4. Encoding
Binary Encoding: Sex → female = 0, male = 1
One-Hot Encoding: Title and Embarked split into dummy columns via pd.get_dummies()
5. Feature Selection
Dropped: PassengerId, Name, Ticket, Cabin (original)

6. Model Training & Evaluation
Train/Test Split: 80 % / 20 % (random_state=42)
Trained and compared 6 different classifiers
Best model: Gradient Boosting Classifier (86.0 %)
🔑 Feature Importance (Best Model)
The Gradient Boosting model revealed which features mattered most:

Feature Importance

❌ Where Does the Model Still Make Mistakes?
The Confusion Matrix shows where even the best model fails:

Confusion Matrix

💻 Tech Stack
Tool	Purpose
Python 3	Programming Language
Pandas	Data manipulation
Scikit-Learn	Machine Learning models
Matplotlib & Seaborn	Visualizations
Jupyter Notebook	Interactive development
📁 Repository Structure

titanic-ml/
│
├── titanic_eda_ml.ipynb       # Full notebook (EDA + ML)
├── README.md                  # This file
├── model_comparison.png       # Model accuracy chart
├── survival_by_sex.png        # EDA visualization
├── survival_by_class_sex.png  # EDA visualization
├── feature_importance.png     # Best model feature importance
└── confusion_matrix.png       # Best model error analysis
🚀 How to Run
bash

git clone https://github.com/YOUR_USERNAME/titanic-ml.git
cd titanic-ml
pip install pandas scikit-learn matplotlib seaborn jupyterlab
jupyter lab titanic_eda_ml.ipynb
💡 Key Takeaways
Feature Engineering beats raw data. The Title extraction for age imputation was the single most impactful data preparation step.
Gradient Boosting dominates tabular classification tasks — it outperformed all other models by a significant margin.
KNN and SVM underperform without feature scaling — their low scores are not a flaw of the algorithm, but a result of unscaled features like Fare (0–500) drowning out binary features like Sex (0–1).
Gender > Social Class. The data confirms "women and children first" overruled the class hierarchy in the chaos of that night.
