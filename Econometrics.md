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

### 2.2 Deriving the Ordinary Least Squares Estimates

#### Method I

Step 1: Based on two assumptions:

 - E(&mu;) = 0
 - E(&mu;|x) = E(&mu;)
   - This implies zero covariance between &mu; and x. (see [proof](https://math.stackexchange.com/questions/967641/prove-that-mean-independent-random-variables-are-uncorrelated))
   - so, Cov(&mu;, x) = E(&mu;x) - E(&mu;)E(x) = E(&mu;x) = 0

Step 2: From E(&mu;) = 0 & E(&mu;x) = 0:

 - E(&mu;) = 0 => E(y - &beta;<sub>0</sub> - &beta;<sub>1</sub>x) = 0
 - E(&mu;x) = 0 => E[x(y - &beta;<sub>0</sub> - &beta;<sub>1</sub>x)] = 0

Step 3: Replacing expectation with averages, and solve for &beta;<sub>0</sub>
 and &beta;<sub>1</sub>
 
#### Method II

To minimize the sum of squared residuals. Take the derivative of SSR w.r.t. &beta;<sub>0</sub> and &beta;<sub>1</sub>, get the **first order conditions** for OLS estimates

#### Comments on the estimates: 

 - The estimates are called the ordinary least squares estimates
 - The equation is called **sample regression function (SRF)**
 - &beta;<sub>1</sub> is just a scaled version of &rho;<sub>xy</sub>. In effect, simple regression is an analysis of correlation between two variables
 - If the estimates intercept is negative but y should always be position, it could be that the sample size near origin is too small, thus it's no surprising that the regression line does poorly at low values of x.
 - We run the regression of y on x, or regress y on x.

### 2.3 Properties of OLS on Any Sample of Data

From E(&mu;) = 0

 - The sum of the residuals is 0 => y̅ = ŷ-bar
 - The point (x̅, y̅) is always on the OLS regression line.

From E(&mu;x) = 0

 - The sample covariance between x and residuals is 0.
 - Sample covariance between ŷ and residual is 0

Goodness of fit

 - Total sum of squares (SST); explained sum of squares (SSE); residual sum of squares (SSR): SST = SSE + SSR. 
 - R<sup>2</sup> = SSE/SST, assuming SST != 0
 - R<sup>2</sup> = &rho;<sub>y, ŷ</sub><sup>2</sup>
 - Seemingly low R-squared does not necessary mean that an OLS regression equation is useless. 

### 2.4 Units of Measurement and Functional Form

 - Changing units of x and y changes estimates in expected ways, and doesn't changed R<sup>2</sup>.
 - In the log-level model, 100&beta;<sub>1</sub> is called semi-elasticity of y w.r.t. x; In the log-log model, &beta;<sub>1</sub> is the elasticity of y w.r.t. x
 - Linear means the equation is linear in the parameters &beta;<sub>0</sub> and &beta;<sub>1</sub>.

### 2.5 Expected Values and Variances of the OLS Estimators (statistical properties of OLS)

##### SLR 1 Linear in parameters

 - y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x + &mu;
 - y, x, &mu; are random variables
 - &beta;<sub>0</sub> and &beta;<sub>1</sub> are not random variables. They're fixed values that we don't know.

##### SLR 2 Random sampling

 - We have a random sample of size n.
 - To write y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x + &mu; in terms of the random sample as: y<sub>i</sub> = &beta;<sub>0</sub> + &beta;<sub>1</sub>x<sub>i</sub> + &mu;<sub>i</sub>

##### SLR 3 Sample variation in the Explanatory Variable
 
 - The sample outcomes on x (i.e. x<sub>1</sub>, x<sub>1</sub>, ...) are not all the same value

##### SLR 4 Zero Condit ional Mean

 - E(&mu;|x) = 0
 - This is equivalent to E(&mu;|x) = E(&mu;) & E(&mu;) = 0
 - For a random sample, this implies E(&mu;<sub>i</sub>|x<sub>i</sub>) = 0 (&mu;<sub>i</sub> is r.v., x<sub>i</sub> is not)

##### Theorem: using SLR 1—4, we can prove the OLS estimates of &beta;<sub>0</sub> and &beta;<sub>1</sub> are unbiased

##### SLR 5 Homoskedasticity

 - Var(&mu;|x) = &sigma;<sup>2</sup>
 - We can derive: Var(&mu;) = &sigma;<sup>2</sup>, so &sigma;<sup>2</sup> is often called the error variance or disturbance variance.

It's often useful to write SLR 4 & 5 as:
 
 - E(y|x) = &beta;<sub>0</sub> + &beta;<sub>1</sub>x
 - Var(y|x) = &sigma;<sup>2</sup>

![](https://robertdkirkby.github.io/introtoeconometrics/Topic6_Heteroskedasticity/Material/Topic6_Fig1.png)

##### Theorem: sample variances of OLS estimates

 - &beta;<sub>1</sub>-hat: &sigma;<sup>2</sup> / SST<sub>x</sub> 
 - &beta;<sub>0</sub>-hat: &sigma;<sup>2</sup> * sum of x<sub>i</sub><sup>2</sup> / (n * SST<sub>x</sub>)

##### Theorem: unbiased estimation of &sigma;<sup>2</sup>

 - E(SSR/(n-2)) = &sigma;<sup>2</sup>
 - sqrt(SSR/(n-2)) is called the standard error of the regression (SER), which is not an unbiased estimator of &sigma;, but an consistent estimator of &sigma;

### 2.6 Regression through the Origin and Regression on a Constant

 - Regression through the origin is not done very often because if the intercept is not 0, then the estimator for &beta;<sub>1</sub> is biased.
 - What if we set the slope to zero and estimate an intercept only? Then the intercept is y̅. The constant that produces the smallest sum of squared deviations is always the sample average.












