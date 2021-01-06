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

##### SLR 4 Zero Conditional Mean

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

### 2.7 Regression on a Binary Explanatory Variable

 - x is called a binary variable or dummy variable if x takes on only two values, zero and one.
   - 𝛽̂<sub>0</sub> = y̅<sub>0</sub>
   - 𝛽̂<sub>1</sub> = y̅<sub>1</sub> - y̅<sub>0</sub>
 - Small R<sup>2</sup> only means the variance in the unobservables, Var(&mu;), is large relative to Var(y)
 - Random sampling means that the data we obtain are independent, identically distributed draws from the population distribution represented by the random variables x and y.

### Summary

Problem: There are two random variables: X and Y. We wan't to know how X affects Y. (this is not the same as causality).

#### Step 1: Establish a model

 - Assume a linear (in parameters) relationship: Y = &beta;<sub>0</sub> + &beta;<sub>1</sub>X + U
 - We think that there's a lot of other stuff affecting Y, but we're only interested in X.
 - This relationship might be wrong. We have various criteria to see if it's a good modeling of the relationship.

#### Step 2: collect data

 - Random sampling: this means the data are i.i.d. draws from the population
 - Why do we need random sampling?
   - Intuitively, to make the sample representative of the whole population
   - Algebraically, to prove unbiasedness we need independence of Us
 - How does the process work?
   - Think of each individual as an experiment: (X<sub>i</sub>, Y<sub>i</sub>), each experiment are independent and all have the same distribution.
   - Do the experiment n times, and we have the data (x<sub>i</sub>, y<sub>i</sub>)
   - x<sub>i</sub> can't be all the same. If it is, all the data points are on a vertical line, there's no way you could get good estimates. If they turn out to be the same, you might want to do more experiments.

#### Step 3: Run the model through data

 - Assume: E(U|X) = 0, which is the equivalent as the following:
   - E(U) = 0. If it's not 0, then we can always redefine U and &beta;<sub>0</sub> to make it 0
   - E(U|X) = E(U). This is stronger than uncorrelation and weaker than independence.
     - We need the "idea" that U and X are uncorrelated. If part of X is in part of U, then we can't isolate X's effect.
     - But uncorrelation only measures linear dependence. Even if U and X are uncorrelated, they can still be largely dependent.
     - Mean independence suffices for our purposes. Independence is too strong an assumption.
 - E(U|X) = 0 also means E(Y|X) = &beta;<sub>0</sub> + &beta;<sub>1</sub>X, which, geometrically, means the Y values are distributed evenly on both sides of the modeling line.
 - Calculate the estimates:
   - E(U) = 0 & E(U|X) = 0. Replacing the expection with averages.
   - The results are in terms of (X<sub>i</sub>, Y<sub>i</sub>). You could also write it in terms of (x<sub>i</sub>, y<sub>i</sub>), which will already have some sense of conditioning.
   - The results are the same as what we get from minimizing SSR, which is why the estimates are also called OLS estimates.

#### Step 4: Assess the model (the estimates)

 - Unbiasedness: On average, do the estimates represent the real value of &beta;<sub>0</sub> and &beta;<sub>1</sub>?
   - E(&beta;<sub>1</sub>-hat | X<sub>1</sub>=x<sub>1</sub> ...) = &beta;<sub>1</sub>
   - E(&beta;<sub>0</sub>-hat | X<sub>1</sub>=x<sub>1</sub> ...) = &beta;<sub>0</sub>
   - Conditioning on the values of Xs, but Ys are still random variables.
 - Variance: How far can those estimates be away from the real values on average?
   - Assume homoskedasticity. Why?
   - Get unbiased estimates of &sigma;<sup>2</sup>
   - Get variance of estimates (conditioning on Xs)

Question: Why don't we assume cov(x, &mu;) = 0 & E(&mu;) = 0 instead of SLR4? it seems that if we only assume these two conditions, we could still get the estimates and prove unbiasedness.

## Chapter 3 Multiple Regression Analysis: Estimation

Why do we need multiple regression analysis?

 - The key assumption for SLR, that all other factors affecting y are uncorrelated with x, is often unrealistic.
 - If we add more factors to our model that are useful for explaning y, then more of the variation in y can be explained.
 - It can incorporate fairly general functional form relationship.

### 3-1 Motivation for multiple regression

Multiple linear regression (MLR) model (aka multiple regression model):

 - y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x<sub>1</sub> + &beta;<sub>2</sub>x<sub>2</sub> + &beta;<sub>3</sub>x<sub>3</sub> + ... + &beta;<sub>k</sub>x<sub>k</sub> + &mu;
 - terms: 
   - &beta;<sub>0</sub>: intercept
   - &beta;<sub>i</sub> are slope parameters
   - u: error term or disturbance
 - key assumption: E(&mu;|x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub>) = 0 
   - intuitively, this the key for estimating ceteris paribus relationship.
   - algebraically, without this assumption, the estimators will be biased.
   - from this we can derive that all xs are uncorrelated to &mu;

### 3-2 Mechanics and interpretation of ordinary least squares

The power of multiple regression analysis is that it provides partial effect or ceteris paribus interpretation even though the data have not been collected in a ceteris paribus fashion.

To solve for estimates, must assume that the first order conditions can be solved uniquely for &beta;s. For example, to solve for &beta;<sub>1</sub>:

 - To derive &beta;<sub>1</sub>, regression x<sub>1</sub> on x<sub>2</sub>, x<sub>3</sub>, ... , x<sub>k</sub>, get the residuals. The residuals are part of  x<sub>1</sub> that's uncorrelated with other xs. Another way of saying this is that residuals are x<sub>1</sub> after the effects of other xs have been partialled out or netted out.
 - Then regress y on the residuals
 - In econometrics, the general partialling out result is usually called the Frisch-Waught theorem.
   
The simple regression of y on x<sub>1</sub> and the multiple regression of y on x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub> produce an identical estimate of x<sub>1</sub> only if:

 - the OLS coefficients on x<sub>2</sub> through x<sub>k</sub> are all zero
 - or x<sub>1</sub> is uncorrelated with each of x<sub>2</sub>, ... , x<sub>k</sub>

An important fact about R<sup>2</sup> is that it never decreases, and it usually increases, when another independent variable is added to a regression and the same set of observations is used for both regressions:

 - the variance of y doesn't change
 - SSR only decreases. (the model with less vars is just a special case of the one with more vars)

Generally, a low R<sup>2</sup> indicates that it is hard to predict individual outcomes on y with much accuracy.
   
Regression through the origin:

 - OLS residuals no longer have a zero sample average
 - R<sup>2</sup> can be negative. This means the sample average explains more of the variation in the y than the explanatory variables. Either we should include an intercept in the regression or conclude that the explanatory variables poorly explain y.
 - If the intercept in the population model is different from 0, then OLS estimators of the slope parameters will be biased.
 - The upside to regression through the origin is that the variances of the estimators are smaller.

### 3-3 The expected value of the OLS estimators

Statistical properties have nothing to do with a particular sample, but rather with the property of estimators when random sampling is done repeatedly.

**Assumption MLR.1 Linear in parameters**

 - The model in the population can be written as: y = &beta;<sub>0</sub> + &beta;<sub>1</sub>x<sub>1</sub> + &beta;<sub>2</sub>x<sub>2</sub> + &beta;<sub>3</sub>x<sub>3</sub> + ... + &beta;<sub>k</sub>x<sub>k</sub> + &mu;
   - &beta;<sub>0</sub>, &beta;<sub>1</sub>, ... , &beta;<sub>k</sub> are the unknown parameters (constants) of interest
   - &mu; is an unobserved random error or disturbance term.
 - This is called the **population model** or **true model**

**Assumption MLR.2 Random sampling**

 - We have a random sample of n observations {(x<sub>i1</sub>, x<sub>i2</sub>, ... , x<sub>ik</sub>, y<sub>i</sub>): i=1, 2, ... , n}

**Assumption MLR.3 No perfect collinearity**

 - In the sample (and therefore in the population), there are no exact linear relationships among the independent variables.
   - If an independent variable is an exact linear combination of the other independent variables, then we say the model suffers from **perfect collinearity**, and it cannot be estimated by OLS.
     - Intuitively, the problem is that we cannot interpret the equation in a ceteris paribus fashion.
     - Algebraically, suppose x<sub>1</sub> is determined by other variables, then regressing x<sub>1</sub> on other variables will give us residuals all 0. Then when we try to compute &beta;<sub>1</sub>, the denominator will be 0.
     - Possible solution: drop some variables from the model
   - This assumption does allow the independent variables to be correlated; they just cannot be perfectly correlated.
 - Violations to this assumption
   - One of the independent variable is constant
   - The sample size is too small in relation to the number of parameters being estimated. (n < k+1)

**Assumption MLR.4 Zero conditional mean**

 - The error &mu; has an expected value of zero given any values of the independent variables: E(&mu;|x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub>) = 0.
   - When MLR.4 holds, we often say that we have **exogenous explanatory variables**.
   - If x<sub>j</sub> is correlated with &mu;for any reason, then x<sub>j</sub> is said to be an **endogenous explanatory variable**.
 - Violations to this assumption
   - The functional relationship between the explained and explanatory variables is misspecified.
   - Omitting an important factor that is correlated with any of x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub> causes MLR.4 to fail.

**Theorem 3.1 Unbiasedness of OLS**

 - Under assumption MLR.1-4, all estimates are unbiased.
 - We do not mean any particular estimate is unbiased. We mean that the procedure by which the OLS estimates are obtained is unbiased when we view the procedure as being applied across all possible random samples.

**Some issues with MLR**

 - **Inclusion of an irrelevant variable** or **overspecifying the model**: This does not affect the unbiasedness of the OLS estimators.
 - **Excluding a relevant variable** or **underspecifying the model**
   - Expectation — true value is called **omitted variable bias**
   - Correlation between a single explanatory variable and the error generally results in all OLS estimators being biased.
   - We can not say a particular estimate is too big or too small. We can only say if we collect many random samples and obtain the simple regression estimates each time, then the average of these estimates will be greater than or less than their true values.
   - direction of bias
     - expectation > true value: **upward bias**
     - expectation < true value: **downward bias**
     - 0 < abs(expectation) < abs(true value): **biased toward zero**

### 3-4 The variance of the OLS estimators

**Assumption MLR.5 Homoskedasticity**

 - The error &mu; has the same variance given any value of the explanatory variables: Var(&mu;|x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub>) = &sigma;<sup>2</sup>
 - We need this for two reasons:
   - The formulas of variance of &beta;s are simplified by imposing the constant error variance assumption.
   - OLS has an important efficiency property if we add the homoskedasticity assumption.
 - MLR.1—MLR.5 are collectively known as the Gauss-Markov assumptions (for cross-sectional regression)

**Theorem 3.2 Sampling variances of the OLS slope estimators**

 - The variance of estimate of &beta;<sub>j</sub> = &sigma;<sup>2</sup> / SST<sub>j</sub>(1 - R<sub>j</sub><sup>2</sup>)
   - SST<sub>j</sub> is the total sample variance in x<sub>j</sub>
   - R<sub>j</sub><sup>2</sup> is the R-squared from regressing x<sub>j</sub> on all other independent variables (including an intercept)
   - square root of this is called **standard deviation** of &beta;<sub>j</sub>-hat
   - replacing &sigma; with its estimate gives us the **standard error** of &beta;<sub>j</sub>-hat
 - Is there a simple formula for the variance where we do not condition on the sample outcomes of the explanatory variables?
   - None that is useful. The above formula is a highly nonlinear function of xs, making averaging out across the population distribution of the explanatory variables virtually impossible.
 - Remember, all of the Gauss-Markov assumptions are used in obtaining this formula.
 - Components of the formula:
   - &sigma;<sup>2</sup>: the error variance. For a given dependent y, there is really only one way to reduce the error variance, and that is to add more explanatory variables to the equation (take some factors out of the error term)
   - SST<sub>j</sub>: the total sample variation in x<sub>j</sub>. We can increase the sample size to increase SST<sub>j</sub> and reduce the variance.
   - R<sub>j</sub><sup>2</sup>: the linear relationships among the independent variables
     - R<sub>j</sub><sup>2</sup> = 0 iff x<sub>j</sub> has zero sample correlation with every other independent variable
     - High (but not perfect) correlation between two or more independent variables is called **multicollinearity**.
 - The choice of whether to include a particular variable in a regression model can be made by analyzing the tradeoff between bias and variance. But we would prefer including the variable because:
   - (main reason) The bias doesn't shrink to 0 as the sample size grows (it doesn't follow any pattern), but the variance shrinks to 0 as sample size grows.
   - &sigma;<sup>2</sup> increases when a variable is excluded from the model. Simply comparing between &sigma;<sup>2</sup> / SST<sub>j</sub>(1 - R<sub>j</sub><sup>2</sup>) and &sigma;<sup>2</sup> / SST<sub>j</sub> ignores this fact.

**Theorem 3.3 Unbiased estimation of &sigma;<sup>2</sup>**

 - Under Gauss-Markov assumptions MLR.1—MLR.5, E(SSR/(n-k-1)) = &sigma;<sup>2</sup>
   - n-k-1 is the degrees of freedom: #obervations-#number of estimated parameters.
   - sqrt(SSR/(n-k-1)) is called the standard error of the regression (SER), or standard error of the estimate, or the root mean squared error.

### 3-5 Efficiency of OLS: The Guass-Markov Theorem

**Theorem 3.4 Guass-Markov Theorem**

 - Under Assumptions MLR.1through MLR.4, the estimators for &beta;s are the best linear unbiased estimators
   - best: having the smallest variance
   - linear: it can be expressed as a linear function of the data on the dependent variable
   - estimator: it is a rule that can be applied to any sample of data to produce an estimate
 - If we want to estimate any linear function of the &beta;<sub>j</sub>, then the corresponding linear combination of the OLS estimators achieves the smallest variance among all linear unbiased estimators.

### 3-6 Some comments on the language of multiple regression analysis

It's wrong to say we "estimated an OLS model"

 - OLS is an estimation method, not a model
 - A model describes an underlying population and depends on unknown parameters
 - We should say, we "estimated a linear model by OLS"

## Chapter 4: Multiple Regression Analysis: Inference

### 4-1 Sampling distributions of the OLS estimators

**Assumption MLR.6 Normality assumption**

 - The population error &mu; is independent of the explanatory variables, and &mu; ~ Normal (0, &sigma;<sup>2</sup>)
 - MLR.6 implies MLR.4 and MLR.5
   - E(&mu;|x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub>) = E(&mu;) = 0
   - Var(&mu;|x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>k</sub>) = Var(&mu;) = &sigma;<sup>2</sup>
 - Assumptions MLR.1—MLR.6 are called **classical linear model (CLM)** assumptions
 - The model under these six assumptions is called the **classical linear model**
 - Under CLM assumptions, the OLS estimators have a stronger efficiency property than they would under Gauss-Markov assumptions
   - OLS estimators has the smallest variance among unbiased estimators

**Theorem 4.1 Normal sampling distributions**

 - Under CLM assumptions MLR.1—MLR.6, conditional on the sample values of the independent variables:
   - the estimator of &beta;<sub>j</sub> ~ Normal (&beta;<sub>j</sub>, Var(&beta;-hat<sub>j</sub>))