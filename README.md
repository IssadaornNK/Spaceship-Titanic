# Space Titanic Survival Prediction

This repository contains a machine learning project aimed at predicting whether passengers aboard the 'Space Titanic' were transported to an alternate dimension. This project was developed as a solution for a Kaggle competition.

## Project Goal
The primary objective is to predict the `Transported` status for each passenger, which indicates whether they were transported to another dimension (True) or not (False).

## Dataset
The dataset used for this competition consists of two main files:
-   `train.csv`: Contains passenger data including various personal details, spending habits, and the `Transported` status.
-   `test.csv`: Contains similar passenger data but without the `Transported` status, which needs to be predicted.

Key features include `PassengerId`, `HomePlanet`, `CryoSleep`, `Cabin`, `Destination`, `Age`, `VIP`, `RoomService`, `FoodCourt`, `ShoppingMall`, `Spa`, `VRDeck`, and `Name`.

## Methodology
The solution involves several key steps:

1.  **Data Loading and Initial Overview**: Loading the `train.csv` and `test.csv` datasets and performing initial checks on shape, info, missing values, and data types.

2.  **Exploratory Data Analysis (EDA)**:
    -   Visualizing the distribution of the target variable (`Transported`).
    -   Identifying and visualizing missing values across features.
    -   Plotting distributions of numerical features (`Age`, `RoomService`, etc.).
    -   Analyzing distributions of categorical features (`HomePlanet`, `CryoSleep`, `Destination`, `VIP`).
    -   Investigating the relationship between key features and the `Transported` target.

3.  **Data Cleaning**: Filling missing values in critical columns:
    -   Categorical columns (`HomePlanet`, `CryoSleep`, `Destination`, `VIP`, `Cabin`) were filled with 'Unknown'.
    -   Numerical `Age` was filled with the median age.
    -   Spending-related numerical columns (`RoomService`, `FoodCourt`, `ShoppingMall`, `Spa`, `VRDeck`) were filled with 0, assuming no spending if missing.

4.  **Feature Engineering**: New features were created to enhance model performance:
    -   `Group`: Extracted from `PassengerId` to identify groups of travelers.
    -   `GroupSize`: The number of passengers in each group.
    -   `Deck`, `CabinNum`, `Side`: Extracted from the `Cabin` column.
    -   `TotalSpend`: Sum of all spending features.
    -   `NoSpending`: A binary flag indicating if a passenger had no spending across all categories.
    -   `LastName`: Extracted from the `Name` column.

5.  **Data Preparation for Modeling**:
    -   Unnecessary columns (`PassengerId`, `Name`, `Cabin`, `Group`, `LastName`) were dropped.
    -   Categorical features were explicitly converted to `object` type.
    -   Numerical features were identified.
    -   The dataset was split into training and validation sets (`X_train`, `X_val`, `y_train`, `y_val`) using an 80/20 split with stratification.
    -   Missing values in categorical columns were filled with 'Unknown' and converted to string type for CatBoost compatibility.

6.  **Model Training**: A **CatBoostClassifier** was used for prediction.
    -   The model was trained with 500 iterations, a depth of 6, and a learning rate of 0.1.
    -   Early stopping was implemented based on the validation accuracy.

7.  **Model Evaluation**: The model's performance was assessed on the validation set using:
    -   Accuracy score.
    -   Classification report (precision, recall, f1-score).
    -   Confusion matrix visualization.

## Results

On the validation set, the CatBoost model achieved an **Accuracy of approximately 80.68%**.

## How to Reproduce

1.  **Clone the Repository**: Clone this GitHub repository to your local machine.
2.  **Google Colab**: Open the `[Your-Notebook-Name].ipynb` (or similar) file in Google Colab.
3.  **Upload Data**: Upload `train.csv` and `test.csv` (obtained from the Kaggle competition) to your Colab environment.
4.  **Run Cells**: Execute all cells in the notebook sequentially. The notebook will handle data loading, preprocessing, model training, evaluation, and generate a `submission.csv` file.

## Files in this Repository
-   `[Your-Notebook-Name].ipynb`: The main Colab notebook containing all the code.
-   `train.csv`: The training dataset (Kaggle).
-   `test.csv`: The test dataset (Kaggle).
-   `submission.csv`: The generated submission file with predictions for the test set.
