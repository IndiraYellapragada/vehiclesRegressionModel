
The repository performs an analysis of used vehicle prices, aiming to build a regressive model that identifies the features that effect the price of an used car.  
Dataset Used is found [here](../data/vehicles.csv)  
All the prompts given to achieve the below analysis can be found [here](../UsedCars_prompt_II.ipynb).  

Here's a breakdown of the key steps and insights:

**1. Exploratory Data Analysis (EDA):**

* **Data Inspection:** The code starts by examining the number of unique values for each column in the `vehicles` dataset. This helps identify potential categorical and numerical features. 
* **Visualizations:**  Scatter plots are generated to visualize the relationship between various features (categorical and numerical like 'odometer', 'price', 'year') and the target variable ('price'). These visualizations help understand the correlation and potential non-linear relationships.  A line plot visualizes the relationship between vehicle condition, title status, and type against price. Pair plots visualize pairwise relationships between numerical features.
* **Correlation Analysis:** The correlation between numerical features and the target variable is calculated.  The code determines the most correlated feature to price.
* **Crosstab:**  This compares price to the manufacturer.
* **Data Distribution:**  Examining the value counts for numerical columns shows distribution, which informs cleaning and transformation strategies.

**2. Data Preparation:**

* **Feature Engineering:**  An 'age' column is created (2025-year), representing the vehicle's age.
* **Data Cleaning:**
    * Columns with identifiers (`id`, `VIN`) are removed as they don't contribute to price prediction.
    * Columns with high cardinality or null values are dropped.
    * `odometer` values of zero are removed as invalid.
    * Missing values in numerical columns are filled with median/mode of that column.
    * Price values of zero are replaced with the mean price.
    * Outliers in price are removed using the IQR method.
* **Data Type Conversion:** Categorical columns are converted to string type.

**3. Modeling:**

* **Feature Scaling & Encoding:**  Numerical features are scaled using `StandardScaler`.  Categorical features are encoded using `JamesSteinEncoder`.  Polynomial features are added.
* **Train-Test Split:** Data is split into 80% training and 20% testing sets.
* **Linear Regression:** A linear regression model is trained and evaluated using RMSE and R-squared.  Coefficients of the linear regression model are interpreted.
* **Hyperparameter Tuning (GridSearchCV):** Hyperparameter tuning is performed on the linear regression model, and the code obtains best hyperparameter.
* **Polynomial Regression:** Polynomial regression models (up to degree 5) are trained.  The model that minimizes the test MSE is selected.
* **Ridge Regression:** A Ridge regression model with polynomial features is used, and hyperparameter tuning is performed to find the best alpha.
* **LASSO and Feature Selection:** LASSO is used for feature selection by shrinking some coefficients to zero.
* **Sequential Feature Selection:** A sequential feature selection process selects the top 3 features based on their importance.

**4. Evaluation:**

The model's performance is evaluated using metrics like Mean Squared Error. The best performing models are identified.  

**5. Deployment:**  

* Linear Reression without intercept shows that manufacturer, odometer and type of the car are most important features that determine the price.  
* Ridge model shows age^2,model,state,type are the important features deciding the price of used car.  
* Lasso Model Shows that Odometer, odometer^2 and age are the important features that impact the price of used car.  
* SEquential Selection model indicates that odometer and age are the important features for price determination  



