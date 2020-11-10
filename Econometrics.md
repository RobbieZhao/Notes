# Woodridge

Text book: Introductory Econometrics: A Modern Approach, 7th edition.

## Chapter 1 The Nature of Econometrics and Economic Data


#### Data

 - Experimental data
 - Nonexperimental data (aka, observational data or retrospective data)

#### How do perform empirical economic analysis
 1. **Construct a economic model**: consists of mathematical equations that describe various relationships
 2. **Turn the economic model into a econometric model**
    - The betas describe the directions and strengths of the relationshiop between the two variables.
    - Dealing with the error term or disturbance term is perhaps the most important component of any econometrics analysis.

#### Data Structure
 - **Cross-Sectional Data**: A sample of individuals, households, firms, cities, states, countries, or a variety of other units, taken at a given point in time.
    - Often assume it is obtained by random sampling  
    - Be careful when random sampling might be violated by, say, dependent draws  
 - **Time Series Data**: Observations on a variable or several variables over time.
   - More difficult to analyze than cross-sectional data: 
     - Economic observations can rarely be assumed to be independent across time.
     - Trending: highly persistent nature of many economic time series
 - **Pooled Cross Section**: Have both cross-sectional and time series features.
   - Increases sample size
   - See how a key relationship has changed over time
 - **Panel or Longitudinal Data**: A times series for each cross-sectional member in the dataset.
   - Same cross-sectional units are followed over a given time period, can also be treated as a pooled cross section, where members happen to show up in each point in time
   - Multiple observations on the same units allows us to control for certain unobserved characteristics of members
   - Allow us to study the importance of lags in behavior or the result of decision making

#### Other
 - **ceteris paribus**: other (relevant) factors being equal

# Part 1 Regression Analysis with Cross-sectional Data

## Chapter 2 The Simple Regression Model 

### 2.1 Definition of the simple regression model

#### 1. The model

We want to explain y in terms of x or study how y varies with changes in x.

The simple linear regression model (aka two-variable linear regression model, or bivariate linear regression model) is defined by:

> y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x + &mu;

#### 2. Terms

 -  x and y

	|          Y         |           X          |
	|:------------------:|:--------------------:|
	| Dependent variable | Independent variable |
	| Explained variable | Explanatory variable |
	|  Response variable |   Control variable   |
	| Predicted variable |  predictor variable  |
	|     Regressand     |       Regressor      |
	
 - &beta;<sub>0</sub>: slope parameter  
 - &beta;<sub>1</sub>: intercept parameter, or constant term
 - &mu; the error term of disturbance: factors other than x that affect y. Or. the unsystematic part, i.e. the part of y not explained by x
 - &beta;<sub>0</sub> + &beta;<sub>1</sub>x: systematic part of y, i.e. part of y explained by x


#### 3. Assumptions  

1. WLOS, assume E(&mu;) = 0, as long as intercept is included in the equation. 
2. &mu; is **mean independent of** x: E(&mu;|x) = E(&mu;)

=> the **zero conditional mean assumption**: E(&mu;|x) = 0

Taking expectation conditional on x on both sides of y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x + &mu;

=> **population regression function**: E(y|x) = &beta;<sub>0</sub> + &beta;<sub>1</sub>x

























