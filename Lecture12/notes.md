# Lecture 12

#### Friedman's Permanent Income Hypothesis

> "The Permanent Income Hypothesis (PIH) says that the permanent consumption $C_{i}^{P}$ of a individual $i$ is a function of that individual's permanent income $Y_{i}^{P}$ : $C_{i}^{P} = f\Big(Y_{i}^{P}\Big)$."
>
> "For Friedman, the permanent income was the interest rate $r$ times the individual's wealth $W_i$ (human capital plus non-human wealth): $Y_{i}^{P} = r W_i$."
>
> "Now, actual income $Y_i$ is the sum of the permanent income $Y_{i}^{P}$ and the temporary income $Y_{i}^{T}$ (fluctuations at each period of time): $Y_{i} = Y_{i}^{P} + Y_{i}^{T}$. Actual consumption $C_{i}$ is also given by the sum of the permanent consumption $C_{i}^{P}$ and temporary consumption $C_{i}^{T}$: $C_{i} = C_{i}^{P} + C_{i}^{T}$."
>
> "Actual income and consumption are what we, in fact, observe. Whereas an error in the LHS variable of the model $C_{i}^{P}$ does not cause big problem, errors in the measurement of the RHS variable $Y_{i}^{P}$ indeed does."
>
> "Both $C_{i}^{T}$ and $Y_{i}^{T}$ are assumed to be uncorrelated random shocks to consumption and income, respectively, and, as such, random variables uncorrelated between themselves and also with $C_{i}^{P}$ and $Y_{i}^{P}$."

Under this hypothesis, the true model would be $C_{i}^{P} = \beta_1 + \beta_2 Y_{i}^{P}$, with $\beta_1 = 0$ (the consumption curve, in a consumption *versus* disposable income plane, should start from the origin).

To test, we would like to run $C_{i}^{P} = \beta_1 + \beta_2 Y_{i}^{P} + v_i$ ($v_i$ is the stochastic error), under the hypotheses:
$$
\begin{align}
H_{0} : \beta_1 = 0 \\
H_{1} : \beta_1 \neq 0
\end{align}
$$
Since what we truly observe is the actual consumption $C_{i}^{P}$ and actual income $Y_{i}^{P}$, the model we are supposed to run is $C_{i} - C_{i}^{P} = \beta_1 + \beta_2 \big(Y_{i} - Y_{i}^{P}\big) + v_i$, which can be rewritten as:
$$
C_i = \beta_1 + \beta_2 Y_i + u_i,
$$
where $u_i = v_i + C_{i}^T - \beta_2 Y_i^T$.

Thus, there is correlation between two variables on the RHS: $Y_i$ and $Y_i^T$. That will bias down the estimated coefficient $\hat\beta_2$.

- We have seen that $\hat\beta_2 = \beta_2 + \displaystyle\frac{\sum (Y_i - \bar Y) u_i}{\sum (Y_i - \bar Y)^2}$.
- We have also seen that, as $N \rightarrow \infty$, $\textrm{plim } \hat\beta_2 = \beta_2 + \displaystyle\frac{\textrm{Cov}(Y_i,u_i)}{\textrm{Var}(Y_i)}$.
- Thus, $\textrm{plim } \hat\beta_2 = \beta_2 + \displaystyle\frac{\textrm{Cov}\Big(Y_i^P + Y_i^T, \ v_i + C_i^T - \beta_2 Y_i^T\Big)}{\textrm{Var}\big(Y_i^P + Y_i^T\big)}$.
  - Since the only correlated term inside the covariance is $Y_{i}^T$ (with itself), then that probability limit can be rewritten as $\textrm{plim } \hat\beta_2 = \beta_2 - \beta_2 \displaystyle\frac{\textrm{Var}(Y_i^T)}{\textrm{Var}(Y_i^P) + \textrm{Var}(Y_i^T)}$.
    - Remember that $\textrm{Cov}(Y,Y) = \textrm{Var}(Y)$.
    - And, since $Y_i^P$ and $Y_i^T$ are uncorrelated, $\textrm{Var}(Y_i^P + Y_i^T) = \textrm{Var}(Y_i^P) + \textrm{Var}(Y_i^T)$.
  - Thus, $\textrm{plim } \hat\beta_2 = \beta_2 \Bigg(1 - \displaystyle\frac{\textrm{Var}(Y_i^T)}{\textrm{Var}(Y_i^P) + \textrm{Var}(Y_i^T)} \Bigg)$.
    - Since the variances are always positive values, then $\textrm{plim } \hat\beta_2 < \beta_2$.

Having $\hat\beta_2$ to be biased downward causes $\hat\beta_1$ to be biased upward.

- From OLS, we know that $\hat\beta_1 = \bar y - \hat\beta_2 \bar x$.
- As $N \rightarrow \infty$, $\bar y \rightarrow \mu_y$ and $\bar x \rightarrow \mu_x$.
  - Thus, for an unbiased and consistent estimate $\hat\beta_2$, $\textrm{plim } \hat\beta_1 = \mu_y - \beta_2 \mu_x = \beta_1$.
- Suppose $\hat\beta_2$ is biased down by a constant $c > 0$, so that $\textrm{plim } \hat\beta_2 = \beta_2 - c$.
  - Then, $\textrm{plim } \hat\beta_1 = \mu_y - (\beta_2 - c) \mu_x = \mu_y - \beta_2 \mu_x + c\mu_x$.
  - Given that $\beta_1 = \mu_y - \beta_2 \mu_x$, then $\textrm{plim } \hat\beta_1 = \beta_1 + c \mu_x$.
  - For $\mu_x > 0$, $\textrm{plim } \hat\beta_1 > \beta_1$.

If the hypothesis is true, then, rather than a curve that starts from the origin, the measurement errors would cause the consumption function would to form a curve with too flat a slope (biased down $\hat\beta_2$) and a non-zero intercept (biased up $\hat \beta_1$).

More on the PIH [here](https://en.wikipedia.org/wiki/Permanent_income_hypothesis).

***

**Measurement error example**:

True model: $\boldsymbol Q = \beta_1 + \beta_2 \boldsymbol Z + \boldsymbol v$.

Suppose there is a common measurement error $\omega$ :
$$
\begin{align}
y_i = Q_i + \omega_i \\
x_i = Z_i + \omega_i
\end{align}
$$
Substituting: $y_i - \omega_i = \beta_1 + \beta_2 (x_i - \omega_i) + v_i$.

- $y_i = \beta_1 + \beta_2 x_i + u_i$, where $u_i = (v_i + \omega_i - \beta_2 \omega_i)$.
- We have seen that $\textrm{plim } \hat\beta_2 = \beta_2 + \displaystyle\frac{\textrm{Cov}(x_i, u_i)}{\textrm{Var}(x_i)}$.
  - $\textrm{plim } \hat\beta_2 = \beta_2 + \displaystyle\frac{\textrm{Cov}\Big(\omega_i, \omega_i(1-\beta_2)\Big)}{\textrm{Var}(Z_i) + \textrm{Var}(\omega_i)}$.
  - $\textrm{plim } \hat\beta_2 = \beta_2 + (1-\beta_2) \displaystyle\frac{\textrm{Var}(\omega_i)}{\textrm{Var}(Z_i) + \textrm{Var}(\omega_i)}$.
    - $\beta_2 > 1 \rightarrow \textrm{plim }\hat\beta_2 < \beta_2$.
    - $\beta_2 < 1 \rightarrow \textrm{plim } \hat\beta_2 > \beta_2$.

***

<u>Solution</u>: **Instrumental variables**

The model: $y_i = \beta_1 + \beta_{2} x_i + u_i$.

Now, suppose that $x_i$ and $u_i$ are somehow correlated.

>  Measurement errors induce correlation between the error and the RHS variable. However, not every correlation between those terms stems, necessarily, from a measurement error. That being so, the following solution is more general than the issue of errors of measurement.

Suppose we have another variable $\boldsymbol z$ with three properties:

1. $\boldsymbol z$ is correlated with $\boldsymbol x$;
2. $\boldsymbol z$ is <u>un</u>correlated with the error;
3. $\boldsymbol z$ is no one of the $\boldsymbol x$'s (multiple RHS variables).

From OLS, we know $\hat\beta_2^{OLS} = \displaystyle\frac{\sum (x_i-\bar x)(y_i - \bar y)}{\sum (x_i - \bar x)^2}$.

- We know $\hat\beta_2^{OLS}$ is inconsistent if $\boldsymbol x$ and $\boldsymbol u$ are correlated.
- We will introduce a new estimator $\hat\beta_2^{IV} = \displaystyle\frac{\sum (z_i - \bar z)(y_i - \bar y)}{\sum (z_i - \bar z)(x_i - \bar x)}$.
  - $\hat\beta_2^{IV} = \displaystyle\frac{\sum (z_i - \bar z)\Big[(\beta_1 + \beta_2 x_i + u_i)-(\beta_1 + \beta_2 \bar x + \bar u)\Big]}{\sum (z_i - \bar z)(x_i - \bar x)}$.
    - $\bar u$, as always, is assumed to be zero.
  - $\hat\beta_2^{IV} = \displaystyle\frac{\sum (z_i - \bar z)(\beta_2 x_i - \beta_2 \bar x + u_i)\Big]}{\sum (z_i - \bar z)(x_i - \bar x)}$.
    - This can be rewritten as $\hat\beta_2^{IV} = \beta_2 \displaystyle\frac{\sum (z_i - \bar z)(x_i - \bar x)}{\sum (z_i - \bar z)(x_i - \bar x)} + \frac{\sum(z_i - \bar z) u_i}{\sum (z_i - \bar z)(x_i - \bar x)}$.
    - $\hat\beta_2^{IV} = \beta_2 + \displaystyle\frac{\sum (z_i - \bar z) u_i}{\sum (z_i - \bar z)(x_i - \bar x)}$.
  - As $N \rightarrow \infty$, $\textrm{plim } \hat\beta_2^{IV} = \beta_2 + \displaystyle\frac{\textrm{Cov}(z_i,u_i)}{\textrm{Cov}(z_i, x_i)}$.
    - Since we assumed $z_i$ and $u_i$ are uncorrelated, $\textrm{Cov}(z_i,u_i) = 0$.
    - Given that $z_i$ and $x_i$ were assumed to be correlated, $\textrm{Cov}(z_i, x_i) \neq 0$.
  - Then, $\textrm{plim } \hat\beta_2^{IV} = \beta_2$.

Usually, the variance of the estimator $\hat\beta_2^{OLS}$ is given by: $\textrm{Var}\bigg(\hat\beta_2^{OLS}\bigg) = \Bigg(\displaystyle\frac{\textrm{Var}(u_i)}{\sum (x_i - \bar x)}\Bigg)$.

- When using an instrumental variable, $\textrm{Var}\bigg(\hat\beta_2^{IV}\bigg) = \Bigg(\displaystyle\frac{\textrm{Var}(u_i)}{\sum (x_i - \bar x)}\Bigg)\Bigg(\frac{1}{r_{xz}^2}\Bigg)$.
  - $r_{xz}$ is the [Pearson correlation coefficient](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) between $\boldsymbol x$ and $\boldsymbol z$.
    - $-1 \leq r_{xz} \leq 1 \rightarrow 0 \leq r_{xz}^2 \leq 1$. Thus, $\textrm{Var}\bigg(\hat\beta_2^{IV}\bigg) \geq \textrm{Var}\bigg(\hat\beta_2^{OLS}\bigg)$.
    - That means that using an instrumental variable comes with a price: the estimated coefficient for the instrumental variable, while consistent, has a higher variance. Hence, the model loses precision.
  - The lower the correlation between $\boldsymbol x$ and $\boldsymbol z$, the higher the variance of $\hat\beta_2^{IV}$.

###### Example:

In macroeconomics, when modeling consumption $\boldsymbol C$ as a function of income $\boldsymbol Y$: $C_t = a + b Y_t + u_t$.

- If we worry that $Y_t$ and $u_t$ are correlated, $Y_{t-1}$ is a good choice for an instrumental variable.
  - $Y_t$ and $Y_{t-1}$ are - most likely - closely correlated.
  - $Y_{t-1}$ cannot be correlated with a posterior random error $u_t$.
- However, we must beware of serial correlation between $u_{t-1}$ and $u_{t}$.

More on instrumental variables estimation [here](https://en.wikipedia.org/wiki/Instrumental_variables_estimation).