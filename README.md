# Titanic Survival Prediction 🚢

## Overview

This project is my first step into machine learning and helped me build a practical understanding of the complete ML workflow.  
By working on this project, I learned how to analyze real-world data, engineer meaningful features, train and evaluate different models, and improve performance through optimization techniques.

The project focuses on predicting whether a passenger survived the Titanic disaster using machine learning classification algorithms.

The dataset contains information about Titanic passengers, and the target variable `Survived` indicates whether a passenger survived:

The main objective of this project is to analyze passenger characteristics, discover meaningful patterns in the data, perform feature engineering, and build machine learning models capable of predicting survival outcomes.

---

# Dataset

The dataset used in this project is obtained from Kaggle.
🔗 Dataset Link:  
https://www.kaggle.com/datasets/yasserh/titanic-dataset


The dataset contains the following features:

| Feature | Description |
|---|---|
| PassengerId | Unique identifier of each passenger |
| Pclass | Ticket class |
| Name | Passenger name |
| Sex | Passenger gender |
| Age | Passenger age |
| SibSp | Number of siblings/spouses aboard |
| Parch | Number of parents/children aboard |
| Ticket | Ticket number |
| Fare | Ticket price |
| Cabin | Cabin number |
| Embarked | Port of embarkation |

### Target Variable
`Survived`
- `0`: Passenger did not survive
- `1`: Passenger survived

---

# Exploratory Data Analysis (EDA)

Before developing machine learning models, exploratory data analysis was performed to understand relationships between passenger characteristics and survival probability.

The following features were investigated:

- Sex
- Pclass
- Age
- Fare
- SibSp
- Parch

<img width="1625" height="371" alt="output" src="https://github.com/user-attachments/assets/9f055906-22d3-4ea6-bf51-3c659b12b6a8" />



## Key Observations

The analysis revealed several important patterns:

- Gender showed a strong relationship with survival probability.
- Passenger class affected survival rates, suggesting socioeconomic differences influenced survival chances.
- Fare showed correlation with survival, possibly representing differences in passenger status.
- Family-related features showed potential predictive information.

These observations were used to guide the feature engineering process.

---

# Feature Engineering

## Creating Family Size Feature

The original dataset contained two separate family-related features:
- `SibSp`
- `Parch`

Since these features describe different parts of a passenger's family situation, they were combined into a single meaningful feature:
FamilySize = SibSp + Parch + 1

---

## Extracting Passenger Titles

The full passenger name does not directly provide useful information for prediction.

However, titles inside names can provide information about:
- Gender
- Social status
- Professional position
Therefore, titles were extracted from passenger names.

Examples:
```
Mr
Mrs
Miss
Master
Dr
Rev
```

So a new feature called `Title` was created.

Additional cleaning was performed:
- `Mme` → `Mrs`
- `Ms` → `Miss`
- `Mlle` → `Miss`
---

## Handling Rare Titles

Some titles appeared only a few times in the dataset:
```
Dr
Rev
Col
Major
Lady
Sir
Capt
Countess
Jonkheer
...
```

To reduce unnecessary complexity and improve model generalization, uncommon titles were grouped into a single category named "Rare".

---

## Removing Unnecessary Features

After feature engineering, some original features were removed because they did not provide meaningful predictive information.
Removed features:
- PassengerId
- Original Name column
- SibSp
- Parch


## Final form of dataset:
 0   Survived    891 non-null    int64  
 1   Pclass      891 non-null    int64  
 2   Sex         891 non-null    object 
 3   Age         714 non-null    float64
 4   Fare        891 non-null    float64
 5   Embarked    889 non-null    object 
 6   FamilySize  891 non-null    int64  
 7   Title       891 non-null    object
 
---

# Data Preprocessing

Machine learning algorithms require numerical inputs. Therefore, categorical features were converted into numerical representations.
Categorical features:
- Sex
- Embarked
- Title
were transformed using:
```
OneHotEncoder
```

The preprocessing workflow was implemented using Scikit-learn pipelines to ensure consistent data transformation during training and evaluation.

---

# Model Training and Evaluation

Three classification algorithms were trained and compared:

1. Logistic Regression
2. Decision Tree Classifier
3. Random Forest Classifier

The models were evaluated using:

- Accuracy
- Cross Validation
- Confusion Matrix
- Precision Score
- Recall Score

---

# Hyperparameter Optimization

Since tree-based models are highly dependent on their hyperparameters, GridSearchCV was applied to find better parameter combinations for model 2 and mode 3.
Multiple parameter combinations were tested to find the best performing configuration.
After optimization, the performance of tree-based models improved significantly from around 78 percent to around 82 percent.

---

# Model Comparison

The final comparison between models is shown below:

<img width="643" height="144" alt="Capture" src="https://github.com/user-attachments/assets/c4eeea28-34cb-4e52-92ce-5f163aa7b1dd" />

Although Random Forest and Decision Tree improved after hyperparameter tuning, Logistic Regression achieved the highest accuracy and was selected as the final model.

This result highlights that a more complex model does not always guarantee better performance. Proper feature engineering and data understanding can have a significant impact on model quality.

---

# Feature Importance Analysis

To better understand which features contributed most to predictions, feature importance analysis was performed using the optimized tree-based model.

## Top Important Features

| Feature | Importance |
|---|---|
| Title_Mr | 0.527 |
| FamilySize | 0.174 |
| Pclass | 0.122 |
| Fare | 0.073 |
| Title_Rare | 0.053 |
| Age | 0.044 |

The results show that passenger title, family structure, and socioeconomic-related features were among the most important factors affecting survival prediction.

---

# Project Workflow

The complete machine learning workflow followed in this project:

```
Data Loading
      ↓
Exploratory Data Analysis
      ↓
Feature Engineering
      ↓
Data Preprocessing
      ↓
Model Training
      ↓
Cross Validation
      ↓
Hyperparameter Optimization
      ↓
Model Evaluation
      ↓
Feature Importance Analysis
```

---

# Technologies Used

## Programming Language

- Python

## Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

## Machine Learning Techniques

- Logistic Regression
- Decision Tree
- Random Forest
- GridSearchCV
- One-Hot Encoding
- Feature Engineering

---

# Conclusion

In this project, a complete machine learning pipeline was implemented to predict Titanic passenger survival.

The main steps included:

- Understanding the dataset through EDA
- Creating meaningful features
- Handling categorical variables
- Training multiple classification models
- Optimizing tree-based models
- Comparing model performance
- Analyzing feature importance

The final results demonstrated that effective feature engineering and data analysis can significantly improve machine learning performance.

---
