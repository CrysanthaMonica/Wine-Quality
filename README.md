# Wine Quality Prediction Using Bayesian Data Analysis

This project applies **Bayesian statistical methods** to analyze and predict the quality of wine based on its physicochemical properties. The dataset consists of two variants of Portuguese wine—**red** and **white**—with 11 input features related to the chemical properties of the wine and one target variable representing the quality rating.

## Table of Contents
1. [Overview](#overview)
2. [Dataset](#dataset)
3. [Methodology](#methodology)
4. [Modeling](#modeling)
5. [Results](#results)
6. [Evaluation](#evaluation)
7. [Future Improvements](#future-improvements)
8. [Model Output](#model-output)
9. [Model Comparison](#model-comparison)
10. [Conclusion](#conclusion)

## Overview

This project is focused on predicting the quality of wine using Bayesian logistic regression. We built multiple models to understand how the chemical properties of wine influence its quality and used **MCMC sampling** to approximate posterior distributions.

## Dataset

The dataset is sourced from [Kaggle](https://www.kaggle.com/). It includes the following features:
- **Input Features**: 
  - `fixed acidity`
  - `volatile acidity`
  - `citric acid`
  - `residual sugar`
  - `chlorides`
  - `free sulfur dioxide`
  - `total sulfur dioxide`
  - `density`
  - `pH`
  - `sulphates`
  - `alcohol`
- **Target Variable**: `quality`, which is a binary indicator of wine quality (good/bad).

## Methodology

We performed Bayesian logistic regression to identify key factors influencing wine quality. Three models were developed, each varying in complexity and feature selection:

1. **Model 1**: Full Bayesian logistic regression using all features.
2. **Model 2**: A feature selection model using **Stochastic Search Variable Selection** (SSVS).
3. **Model 3**: Bayesian logistic regression with simplified priors.

## Modeling

- **Bayesian Framework**: The prior distributions for the parameters were normal with a mean of 0 and a variance of either 0.01 or 1, depending on the model.
- **Likelihood**: Bernoulli distribution with a logit link function.
- **MCMC Sampling**: Implemented using the `rjags` package in R, with a burn-in phase of 1000 iterations followed by 5000 iterations for sampling.

### Model Comparisons

We compared the models using:
- **Deviance Information Criterion (DIC)**
- **Watanabe-Akaike Information Criterion (WAIC)**
- **Posterior Predictive P-value (PPP)**

## Results

The results of the models showed that:
- Model 3 outperformed the others, achieving the lowest WAIC and DIC scores.
- Key features that significantly influenced wine quality included:
  - `volatile acidity`
  - `residual sugar`
  - `free sulfur dioxide`
  - `total sulfur dioxide`
  - `sulphates`
  - `alcohol`

## Evaluation

- **Model Performance**: The posterior predictive p-values were close to 0.5, indicating that the models fit the data well.
- **Convergence Diagnostics**: All models were checked for convergence using **Geweke** and **Gelman-Rubin** diagnostics. Both tests confirmed good convergence in most variables.
- **Autocorrelation**: The samples from the chains exhibited low autocorrelation, ensuring independent samples.

## Future Improvements

Several improvements can be made to enhance the model and overall project:
1. **Feature Engineering**: Adding or transforming features such as interaction terms or non-linear transformations could improve the model's performance.
2. **More Advanced Models**: Exploring more complex Bayesian models, like Gaussian processes or hierarchical Bayesian models, might capture more intricate relationships.
3. **Cross-Validation**: Adding cross-validation methods to ensure model generalization and avoid overfitting.
4. **Hyperparameter Tuning**: Experimenting with different priors and variance values could refine the model further.

## Model Output

The model will output:

- **MCMC samples**
- **Convergence diagnostics**
- **Model comparison metrics**: DIC, WAIC

### Model Comparison

| Metric     | Model 1 | Model 2 | Model 3 |
|------------|---------|---------|---------|
| DIC        | 6728    | 6735    | 6728    |
| WAIC       | 6729.875| 6735.902| 6729.285|
| PPP        | 0.4896  | 0.4914  | 0.4936  |

- **DIC**: Deviance Information Criterion
- **WAIC**: Watanabe-Akaike Information Criterion
- **PPP**: Posterior Predictive P-value

## Conclusion

In conclusion, **Model 3** provided the most reliable predictions for wine quality using Bayesian analysis. With further improvements, such as enhanced feature selection and more sophisticated modeling, the results could be even more robust and applicable in real-world wine quality assessment scenarios.
