# Lecture 07

**Assumptions**:
$$
\begin{align}
(\textrm C.6) \quad & u_t \perp u_s, \quad \forall\ t \neq s \\
(\textrm C.7) \quad & u_t \perp x_t, \quad \forall\ t \in \{1,2,...,T\}
\end{align}
$$
Considering $(\textrm C.7)$:

- Given the model $y_t = \beta_1 + \beta_2 x_{2,t} + u_t$ , then $\hat\beta_2^{OLS} = \displaystyle\frac{\sum(x_t - \bar x)(y_t - \bar y)}{\sum (x_t - \bar x)^2}$ .
- Use that $(y_t - \bar y) = \beta_2 (x_t - \bar x) + (u_t - \bar u)$ - with $\bar u = 0$ -, since $\hat\beta_1 = \bar y - \hat\beta_2 \bar x$  (more [here](https://en.wikipedia.org/wiki/Simple_linear_regression)).
- We have $\hat\beta_2^{OLS} = \beta_2 \displaystyle\frac{\sum (x_t - \bar x)^2}{\sum (x_t - \bar x)^2} + \displaystyle\frac{\sum (x_t - \bar x)u_t}{\sum (x_t - \bar x)^2} = \beta_2 + \displaystyle\frac{\sum (x_t - \bar x)u_t}{\sum (x_t - \bar x)^2}$ 
  -  Let $a_t := \displaystyle\frac{x_t - \bar x}{\sum (x_t - \bar x)^2}$ , then $\hat\beta_2 = \beta_2 + \sum a_t u_t$ .
- To show it is unbiased, we take the expected value: $\textrm E(\hat\beta_2) = \beta_2 + \textrm E\big[\sum (a_t u_t) \big]$ .
  - If $a_t$ and $u_t$ are uncorrelated, then $\textrm E(\hat\beta_2) = \beta_2 + \sum \big[ \textrm E(a_t) \textrm E(u_t) \big]$ .
  - Since $\textrm E (u_t) = 0$, then $\textrm E (\hat\beta_2) = \beta_2$, provided that $a_t$ and $u_t$ are uncorrelated.
  - $a_t$ depends upon **all** $x_t, \quad t = 1,2,..., T$ .

1. If $x_t$ (current) and $u_t$ are correlated, then $\hat\beta_2$ is <u>biased</u> ($\textrm E (\hat\beta_2) \neq \beta_2$) and <u>inconsistent</u> - $\underset{N\ \rightarrow\ \infty}{\textrm{plim}} \hat\beta_2 \neq \beta_2$.
   - More on the bias and consistency of an estimator [here](https://en.wikipedia.org/wiki/Bias_of_an_estimator) and [here](https://en.wikipedia.org/wiki/Consistent_estimator), respectively.
2. If $x_t$ and $u_t$ are uncorrelated, but $x_t$ and $u_s$ are correlated, for $t \neq s$, then $\hat\beta_2$ is <u>biased</u> but <u>consistent</u>.

**Basic models**
$$
(1) \quad y_t = \beta_1 + \beta_2 x_{2t} + u_t, \quad u_t = \rho u_{t-1} + e_t
$$

- In this case, $\hat\beta_2$ is unbiased and consistent, but inefficient, because $u_t$ and $u_{t-1}$ are correlated.
  - $(\textrm C.6)$ might be an example.
  - More on the efficiency of an estimator [here](https://en.wikipedia.org/wiki/Efficiency_(statistics)).

***

$$
(2) \quad y_t = \beta_1 + \beta_2 x_{2t} + \beta_3 y_{t-1} + u_t
$$

- $y_{t-1}$ is a function of $u_{t-1}$ .
  - $y_{t-1}$ is correlated to $u_{t-1}$.
  - In other words, the error is correlated with a variable that is not its contemporaneous.
- In this case, $\hat\beta_2$ is biased and inefficient but consistent.

***

$$
(3) \quad y_t = \beta_1 + \beta_2 x_{2t} + \beta_3 y_{t-1} + u_t, \quad u_t = \rho u_{t-1} + e_t
$$

- The model can be rewritten as: $y_t = \beta_1 + \beta_2 x_{2t} + \beta_3 y_{t-1} + \rho u_{t-1} + e_t$ .
- Since $u_{t-1}$ is inside $y_{t-1}$, then $u_{t-1}$ and $y_{t-1}$ are correlated.
  - Now, the errors are dependent upon its contemporaneous *and* other variables.
- Then, $\hat\beta_2$ is biased, inefficient and inconsistent.

***

For the model:
$$
(1) \quad y_t = \beta_1 + \beta_2 x_{2t} + u_t, \quad u_t = \rho u_{t-1} + e_t
$$

- It violates the assumption $(\textrm C.6)$, because the errors are correlated.
- $\hat\beta$ is thus unbiased, inconsistent and <u>inefficient</u>.
  - When positive serial correlation exists (*i. e.*, $\rho > 0$), the standard errors are too small.
  - The $t$ statistic $t = \displaystyle\frac{\hat\beta - \beta^{H_0}}{\sigma_{\hat\beta}}$ then blows up.
  - $F$ statistics will get too big, as well.

- Misspecification can also give rise to serial correlation:
  - Suppose a serially correlated variable $x_3$ (say, GDP) is left out of the model.
    - The effect of that variable would be added to the errors, making them serially correlated, as well.
  - Trying to fit a non-linear relation (say, quadratic) through linear regression may give the impression of serial correlation.
    - If the line is secant to the curve, for instance, the errors would be positive-negative-positive (or negative-positive-negative) and would *seem* serially correlated.

***

#### Durbin-Watson test for autocorrelation

This is a test for first order serial correlation **only**.

- For instance, a model $y_t = \beta_1 + \beta_2 x_{2t} + u_t, \quad u_t = \rho u_{t-1} + e_t$ with $|\rho| < 1$.

- This is called a first-order autoregressive process (or $\textrm{AR}(1)$), because it has one lag.
  - Analogously, if the errors were defined as $u_t = \rho_1 u_{t-1} + \rho_2 u_{t-2} + \rho_3 u_{t-3} + e_t$, it would be an $\textrm{AR}(3)$.
  - Since there is no lag on the term $e_t$, this a $0^{\textrm{th}}$ order moving average process ($\textrm{MA}(0)$).
    - An error defined as, say, $u_t = \rho_1 u_{t-1} + \rho_2 u_{t-2} + \rho_3 u_{t-3} +  \delta_1 e_{t-1} + \delta_2 e_{t-2}$ would be classified as an autoregressive moving average model $\textrm{ARMA}(3,2)$.
    - More generally, an $\textrm{ARMA}(p,q)$ is given by $u_t = \displaystyle\sum_{i=1}^p \rho_i u_{t-i} + \displaystyle\sum_{j=1}^q \delta_j e_{t-j}$, for $p,q < t$.
  - For more on autoregressive models, see [this link](https://en.wikipedia.org/wiki/Autoregressive%E2%80%93moving-average_model).

**Hypotheses**:
$$
\begin{align}
H_0 & : \rho = 0 \\
H_1 & : \rho \neq 0
\end{align}
$$
**Steps**:

1. Estimate $y_t = \beta_1 + \beta_2 x_{2t} + ... + \beta_k x_{kt} + u_t$ by OLS, save $\hat u_t$.
2. Compute the test statistic $d = \displaystyle\frac{\displaystyle\sum_{t=2}^T (\hat u_{t} - \hat u_{t-1})^2}{\displaystyle\sum_{t=1}^T \hat u_{t}^2}$, so that $0 < d < 4$.
   - $0 < d < 2$ would suggest a positive serial correlation one-tailed test, while $2 < d < 4$, a negative serial correlation one-tailed test.
3. (a) For the one-tailed test version of the test $H_1 : \rho > 0$ (testing for positive serial correlation), obtain from the [table](./Durbin_Watson_tables.pdf) (external link [here](https://www3.nd.edu/~wevans1/econ30331/Durbin_Watson_tables.pdf)) the critical lower and upper values $d_{\textrm L}$ and $d_{\textrm U}$ for the $N$ observations, $k$ variables and significance $\alpha$.
   - For the positive test, the area of interest will be the interval $[0,2]$, so that $d_{\textrm L}, d_{\textrm U} \in [0,2]$ with $d_{\textrm L} < d_{\textrm U}$.
   - If the test statistic $d_{\textrm U} < d_{\textrm{test}} < 2$, we fail to reject the null hypothesis.
   - If $0 < d_{\textrm{test}} < d_{\textrm L}$, we reject the null hypothesis.
   - Otherwise, if $d_{\textrm L} < d_{\textrm{test}} < d_{\textrm U}$, the (positive serial correlation) test is inconclusive.
     - Usually, another test is performed (namely, the $\textrm{LM}$ test).

3. (b) For the other one-tailed version of the test $H_1 : \rho < 0$ (testing for negative serial correlation), obtain $d_{\textrm L}$ and $d_{\textrm U}$ for the given $N$, $k$ and $\alpha$.
   - For the negative test, the area of interest will be the interval $[2,4]$ so that $(4 - d_{\textrm U}), (4 - d_{\textrm L}) \in [2,4]$ with $(4 -d_{\textrm U}) < (4 - d_{\textrm L})$.
   - If $2 < d_{\textrm{test}} < (4 - d_{\textrm U})$ - *id est*, $(4-d) > d_{\textrm U}$ -, we fail to reject the null hypothesis.
   - If $(4 - d_{\textrm L}) < d_{\textrm{test}} < 4$ - *id est*, $(4-d) < d_{\textrm L}$ -, we reject the null hypothesis.
   - Otherwise, if $(4 - d_{\textrm U}) < d_{\textrm{test}} < (4 - d_{\textrm L})$ - *id est*, $d_{\textrm L} < (4 - d) < d_{\textrm U}$ -, the (negative serial correlation) test is inconclusive.

For more on the Durbin-Watson test, see [this link](https://en.wikipedia.org/wiki/Durbin%E2%80%93Watson_statistic).

***

Why is $d$ between $0$ and $4$?

- The correlation can be estimated by $\hat\rho = \displaystyle\frac{\displaystyle\sum_{t=2}^T \hat u_{t} \hat u_{t-1}}{\displaystyle\sum_{t=1}^T \hat u_{t}^2}$.
  - Then, $\hat \rho = \displaystyle\frac{\frac{1}{(N-k)} \displaystyle\sum_{t=2}^T \hat u_{t} \hat u_{t-1}}{\frac{1}{(N-k)} \displaystyle\sum_{t=1}^T \hat u_{t}^2} \approx \displaystyle\frac{\widehat{\textrm{Cov}}(\hat u_t, \hat u_{t-1})}{\widehat{\textrm{Var}}(\hat u_t)}$: note that the sum in the numerator is missing one term.
- The test statistic is given by $d = \displaystyle\frac{\displaystyle\sum_{t=2}^T (\hat u_{t} - \hat u_{t-1})^2}{\displaystyle\sum_{t=1}^T \hat u_{t}^2}$.
  - Expanding the numerator $d = \displaystyle\frac{\displaystyle\sum_{t=2}^T (\hat u_{t}^2 - 2\hat u_{t}\hat u_{t-1} + \hat u_{t-1}^2)}{\displaystyle\sum_{t=1}^T \hat u_{t}^2}$.
  - Rewriting it: $d = \displaystyle\frac{(N-k-1) \displaystyle\sum_{t=2}^T \frac{1}{(N-k-1)} (\hat u_{t}^2 - 2\hat u_{t}\hat u_{t-1} + \hat u_{t-1}^2)}{(N-k) \displaystyle\sum_{t=1}^T \frac{1}{(N-k)} \hat u_{t}^2}$.
    - $\displaystyle\sum_{t=1}^T \frac{1}{(N-k)} \hat u_{t}^2$ is an estimate of the variance.
    - $\displaystyle\sum_{t=2}^T \frac{1}{(N-k-1)} \hat u_{t}^2$ is an estimate of the variance (with one less observation: $\hat u_1$).
    - $\displaystyle\sum_{t=2}^T \frac{1}{(N-k-1)} \hat u_{t-1}^2$ is also an estimate of the variance (short of one observation: $\hat u_t$).
    - $\displaystyle\sum_{t=2}^T \frac{1}{(N-k-1)} \hat u_{t} \hat u_{t-1}$ is an estimate of the covariance of $\hat u_t$ and $\hat u_{t-1}$.
  - The test statistic may be thus estimated $d = \displaystyle\frac{N-k-1}{N-k} \bigg( \displaystyle\frac{\widehat{\textrm{Var}}(\hat u_t) - 2 \widehat{\textrm{Cov}}(\hat u_t, \hat u_{t-1}) + \widehat{\textrm{Var}}(\hat u_t)}{\widehat{\textrm{Var}}(\hat u_t)} \bigg)$.
    - The larger the number of observations, the closer $\displaystyle\frac{N-k-1}{N-k}$ is to $1$.
    - $\displaystyle\frac{\widehat{\textrm{Var}}(\hat u_t) - 2 \widehat{\textrm{Cov}}(\hat u_t, \hat u_{t-1}) + \widehat{\textrm{Var}}(\hat u_t)}{\widehat{\textrm{Var}}(\hat u_t)} = 2\bigg( 1 - \displaystyle\frac{\widehat{\textrm{Cov}}(\hat u_t, \hat u_{t-1})}{\widehat{\textrm{Var}}(\hat u_t)}\bigg)$.
  - Thus, $d \approx 2(1 - \hat\rho)$.
    - Asymptotically, as $t \rightarrow \infty$, $d = 2(1-\rho)$.
    - If there is perfect positive correlation ($\rho = 1$), then $d = 0$.
    - If there is no correlation ($\rho = 0$), then $d = 2$.
    - If there is perfect negative correlation ($\rho = -1$), then $d = 4$.

***

**Observation**:
$$
\hat\beta_2^{\textrm{OLS}} = \displaystyle\frac
{\displaystyle\sum (X_i - \bar X)(Y_i - \bar Y)}
{\displaystyle\sum (X_i - \bar X)^2}
$$
If we multiply both the numerator and denominator by $\displaystyle\frac{1}{N-k}$:
$$
\hat\beta_2^{\textrm{OLS}} = \displaystyle\frac
{\frac{1}{N-k} \displaystyle\sum (X_i - \bar X)(Y_i - \bar Y)}
{\frac{1}{N-k}  \displaystyle\sum (X_i - \bar X)^2}
$$
then the numerator becomes an estimate of the covariance of $X$ and $Y$, whereas the denominator turns into an estimate of the variance of $X$:
$$
\hat\beta_2^{\textrm{OLS}} = \displaystyle\frac
{\widehat{\textrm{Cov}}(X,Y)}
{\widehat{\textrm{Var}}(X)}.
$$
