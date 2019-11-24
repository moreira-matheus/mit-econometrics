# Lecture 10

Model with serial correlation:
$$
y_{t} = \beta_1 + \beta_2 x_{2t} + ... + \beta_k x_{kt} + u_t, \quad u_t = \rho u_{t-1} + e_t
$$
We take the one-step-back model: $y_{t-1} = \beta_1 +\beta_2 x_{2,t-1} + ... + \beta_k x_{k,t-1} + u_{t-1}$;

Multiply it through by $\rho$ : $\rho y_{t-1} = \rho\beta_1 +\rho\beta_2 x_{2,t-1} + ... + \rho\beta_k x_{k,t-1} + \rho u_{t-1}$;

And subtract from the original model:
$$
y_{t} - \rho y_{t-1} = \beta_1 \big( 1 - \rho \big) + \beta_2 \big( x_{2t} - \rho x_{2,t-1} \big) + ... + \beta_k \big( x_{kt} - \rho x_{k,t-1} \big) + \color{red}u_t - \rho u_{t-1}
$$

- The part in red equals $e_t$.

The model can thus be rewritten as follows:
$$
y_{t}^{*} = \beta_1^{*} + \beta_2 x_{2t}^{*} + ... + \beta_k x_{kt}^{*} + e_t
$$
where $y_{t}^{*} = y_{t} - \rho y_{t-1}$, $\beta_1^{*} = \beta_1(1-\rho)$ and $x_{it}^{*} = x_{it} - \rho x_{i,t-1}$.

This procedure is known as **quasi differencing**. More [here](./ECON2228_2014_10.slides.pdf) and [here](https://www.sciencedirect.com/science/article/abs/pii/S0304407600000245).

- If knew $\rho$, then the transformed model would be fully efficient (and unbiased, since the original model already was).
- However, if we obtain a <u>consistent</u> estimate of $\rho$, then, as time goes to infinity, the estimated model will converge to the true (transformed) model.

##### Cochrane-Orcutt procedure

1. Estimate $y_t = \beta_1 + \beta_2 x_{2t} + ... + \beta_k x_{kt} + u_t$ with OLS. Save the residuals $\hat{u}_t,\ t = 1, 2, ..., T$.
   - We rely upon the fact that the estimated $\beta_i$ will be unbiased albeit inefficient, so we will obtain an estimate of the residuals which is unbiased and consistent.
2. Estimate $\rho$ with $\hat\rho = \displaystyle\frac{\displaystyle\sum_{t=2}^{T} \hat{u}_{t}\hat{u}_{t-1}}{\displaystyle\sum_{t=1}^{T-1}\hat{u}_t^2}$.
   - This is the same as a regression of $\hat{u}_t$ on $\hat{u}_{t-1}$ : $\hat{u}_t = \rho \hat{u}_{t-1} + e_t$.
3. Transform the data, considering:
   - $y_{t}^{*} = y_t - \hat\rho y_{t-1}$ ;
   - $\beta_1^{*} = \beta_1 (1-\hat\rho)$ ;
   - $x_{it}^{*} = x_{it} - \hat\rho x_{i,t-1}$ ;
   - $e_t = u_t - \hat\rho u_{t-1}$.
4. Regress $y_{t}^{*}$ with OLS.
   - This will produce $\hat\beta_1^{*}, \hat\beta_2, ..., \hat\beta_k$.
   - $\hat\beta_1 = \displaystyle\frac{\hat\beta_1^{*}}{1-\hat\rho}$.
   - The coefficients $\hat\beta_i$ obtained here are "less inefficient" than those of step 1.
   - The residuals of this regression are estimates of $e_t$ (rather than $u_t$).
5. Use these estimates $\hat\beta_i$ to get a new estimate of $\hat{u}_t$.
   - The new $\hat{u}_{t} = y_t - \hat\beta_1 - \hat\beta_2 x_{2t} + ... + \hat\beta_k x_{kt}$.
6. Repeat steps 2-5 until $\hat\rho$ changes by less than $.0001$ (rule of thumb).
   - By there, the coefficients will have converged to their fully efficient values.

***

#### Engle's ARCH Test

[ARCH](https://en.wikipedia.org/wiki/Autoregressive_conditional_heteroskedasticity): Autoregressive Conditional Heteroskedasticity.

<u>Most basic model</u>: $\sigma^2_t = \alpha_0 + \alpha_1 \sigma^2_{t-1} + ... + \alpha_p \sigma^2_{t-p}$.

**How do we test for ARCH?**

The original regression model is of the form:
$$
y_t = \beta_1 + \beta_2 x_{2t} + ... + \beta_k x_{kt} + u_t
$$
where $\textrm{Var}(u_t) = \sigma^2_t$.

Hypothesis test:
$$
\begin{align}
H_0 & : \alpha_1 = \alpha_2 = ... = \alpha_p = 0 \\
H_1 & : \exists\ \alpha_i \neq 0 \ \big( i \in \{1,2,...,p\}\big)
\end{align}
$$
Steps:

1. Run $y_t$ on constant, $x_{2t}, ..., x_{kt}$. Save $\hat{u}_t$ and square it: $\hat{u}^2_t$.
2. Run $\hat{u}^2_t$ on constant ($\alpha_0$), $\hat{u}^2_{t-1}, ..., \hat{u}^2_{t-p}$.
3. The test statistic is given by: $(T-p) \cdot R^2$.
   - $(T-p)$ is the number of observations ($T$) minus the number of restrictions ($p$).
   - $R^2$ is coefficient of determination.
   - The test statistic follows a chi-squared distribution with $p$ degrees of freedom: $(T-p)\cdot R^2 \sim \chi^2(p)$.

