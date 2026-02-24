# Data Generation using Modelling & Simulation for Machine Learning  
## Multi-Criteria Model Selection using TOPSIS


## Abstract


This project focuses on generating synthetic data using a physics-based simulation environment and applying multiple machine learning models to predict system performance. Instead of selecting the best model using a single evaluation metric, a Multi-Criteria Decision Making (MCDM) technique - **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)** - is used to scientifically rank the models.

The project integrates:

- Simulation
- Synthetic data generation
- Machine learning regression models
- Multi-criteria decision analysis



## 1. Problem Statement

Collecting large-scale real-world data can be expensive or impractical. Simulation-based modelling allows us to generate synthetic datasets under controlled conditions.

However, selecting the best machine learning model based on a single metric (like R²) may lead to biased conclusions.

This project aims to:

1. Generate 1000 simulation samples.
2. Train multiple ML regression models.
3. Evaluate them using multiple performance metrics.
4. Use TOPSIS to rank and select the best model.



## 2. Simulation Tool

We used the **CartPole-v1** environment from Gymnasium.

### Why CartPole?

- Physics-based dynamic system
- Controlled and reproducible environment
- Adjustable initial parameters
- Produces measurable reward output
- Suitable for regression modelling



## 3. Methodology

### Step 1: Simulation Data Generation

The CartPole system includes four state parameters:

| Parameter | Description |
|-----------|------------|
| Cart Position | Horizontal position of cart |
| Cart Velocity | Speed of cart |
| Pole Angle | Angle from vertical |
| Pole Angular Velocity | Angular velocity |

### Parameter Ranges Used

- Cart Position: [-2.4, 2.4]
- Cart Velocity: [-2, 2]
- Pole Angle: [-0.2, 0.2]
- Pole Velocity: [-2, 2]

For each simulation:

1. Random initial parameters are generated.
2. The simulation runs using random actions.
3. Total reward (number of steps before failure) is recorded.

This process is repeated **1000 times** to generate the dataset.

Final Dataset Structure:

| cart_pos | cart_vel | pole_angle | pole_vel | reward |
|----------|----------|------------|----------|--------|

The reward is used as the target variable.



### Step 2: Machine Learning Models

The following 8 regression models were trained:

1. Linear Regression
2. Ridge Regression
3. Lasso Regression
4. Decision Tree
5. Random Forest
6. Gradient Boosting
7. XGBoost
8. K-Nearest Neighbors (KNN)

Dataset split:

- 80% Training
- 20% Testing



### Step 3: Evaluation Metrics

Each model was evaluated using five metrics:

| Metric | Type | Description |
|--------|------|------------|
| MSE | Cost | Mean Squared Error |
| MAE | Cost | Mean Absolute Error |
| RMSE | Cost | Root Mean Squared Error |
| R² | Benefit | Coefficient of Determination |
| Training Time | Cost | Computational efficiency |

Why multiple metrics?

- MSE penalizes large errors.
- MAE gives average error magnitude.
- RMSE is interpretable in original units.
- R² measures goodness of fit.
- Training time measures computational cost.



## 4. TOPSIS for Model Ranking

Instead of selecting a model based only on R², we applied **TOPSIS**.

### Why TOPSIS?

TOPSIS ranks alternatives based on:

- Distance from ideal best solution
- Distance from ideal worst solution

It evaluates all criteria simultaneously.



### TOPSIS Steps

1. Normalize the decision matrix  
2. Multiply by weights  
3. Determine ideal best and ideal worst  
4. Compute distance from ideal best and worst  
5. Calculate closeness coefficient  
6. Rank models  



### Criteria Weights Used

| Metric | Weight | Impact |
|--------|--------|--------|
| MSE | 0.20 | Minimize |
| MAE | 0.15 | Minimize |
| RMSE | 0.20 | Minimize |
| R² | 0.35 | Maximize |
| Training Time | 0.10 | Minimize |

R² was given the highest weight because predictive accuracy is the most important factor.



## 5. Results

### Model Evaluation Table

| Model | MSE | MAE | RMSE | R² | Train Time |
|-------|-----|-----|------|----|------------|
| Linear Regression | 93.907535 | 7.087400 | 9.690590 | 0.000186 | 0.002228 |
| Ridge | 93.871945 | 7.089869 | 9.688754 | 0.000565 | 0.001825 |
| Lasso | 93.925952 | 7.197025 | 9.691540 | -0.000010 | 0.001827 |
| Decision Tree | 141.075000 | 6.655000 | 11.877500 | -0.501997 | 0.006959 |
| Random Forest | 68.261340 | 5.104400 | 8.262042 | 0.273235 | 0.494874 |
| Gradient Boosting | 68.264419 | 5.399247 | 8.262228 | 0.273203 | 0.242785 |
| XGBoost | 69.445058 | 5.394202 | 8.333370 | 0.260633 | 0.118432 |
| KNN | 92.842800 | 6.670000 | 9.635497 | 0.011522 | 0.004623 |



### TOPSIS Ranking Table

| Rank | Model | TOPSIS Score |
|------|--------|--------------|
| 1 | XGBoost | 0.948 |
| 2 | Gradient Boosting | 0.904 |
| 3 | Random Forest | 0.821 |
| ... | ... | ... |

The model with the highest TOPSIS score is selected as the optimal model.



## 6. Result Graph

The bar graph shows the TOPSIS score of each model.

Interpretation:

- Higher score → Closer to ideal solution
- Ensemble models outperform linear models
- Tree-based methods capture non-linear simulation dynamics effectively



## 7. Discussion

Observations:

- Tree-based ensemble methods outperform linear models.
- The simulation environment exhibits non-linear behavior.
- Random Forest and XGBoost effectively capture feature interactions.
- Training time introduces trade-offs between performance and efficiency.

Using TOPSIS ensures balanced decision-making across all evaluation criteria.



## 8. Conclusion

This project demonstrates:

- Synthetic data generation using simulation
- Application of multiple ML regression models
- Multi-criteria evaluation
- Scientific model selection using TOPSIS

The best model selected using TOPSIS provides an optimal balance between:

- Accuracy
- Error minimization
- Computational efficiency

This approach ensures robust and unbiased model selection.



## 9. Project Structure

```
CartPole-Simulation-ML/
│
├── CartPole_Simulation.ipynb
├── simulation_data.csv
├── model_ranking_topsis.csv
├── README.md
```



## 10. Future Improvements

- Hyperparameter tuning
- Cross-validation
- Entropy-based automatic weight calculation
- Neural network comparison
- Sensitivity analysis of weights



## 11. How to Run

1. Open the notebook in Google Colab.
2. Install required libraries.
3. Run all cells.
4. Results and rankings will be generated automatically.



## Final Statement

This project integrates Simulation + Machine Learning + Multi-Criteria Decision Making to provide a comprehensive framework for data-driven model evaluation.
