# Lecture 06

### Steps for correcting heteroskedasticity

1. Regress $y$ on constant, $x_2, ..., x_k$ ;
   - This produces $\hat\beta_{OLS}$ .

2. Calculate the estimated error (residuals):  $\hat u_i = y_i - \hat\beta_1 - \hat\beta_2 x_{2i} - ... - \hat\beta_k x_{ki}$ ;

3. (a) Regress $\hat u_i^2$ on constant, $z_2, ..., z_p$ ;

   - $\hat u_i^2 = \alpha_1 + \alpha_2 z_2 + ... \alpha_p z_p + \textrm{error}$ ;

   - This produces $\hat\alpha_i$ .

4. Use the predicted variance $\hat\sigma_i^2$ to get $\hat\sigma_i$:

   - $\hat\sigma_i^2 = \hat\alpha_1 + \hat\alpha_2 z_2 + ... + \hat\alpha_p z_p \quad \Rightarrow \quad \hat\sigma_i^2 = \hat u_i^2 - \textrm{error}$;
   - Since there is no guarantee that $\hat\sigma_i^2 > 0$, it might be a good idea to use the absolute value.

5. Divide the whole original model by $\hat\sigma_i$:

   - $\displaystyle\frac{y_i}{\hat\sigma_i} = \beta_1 \displaystyle\frac{1}{\hat\sigma_i} + \beta_2 \displaystyle\frac{x_{2i}}{\hat\sigma_i} + ... + \beta_k \displaystyle\frac{x_{ki}}{\hat\sigma_i} + \displaystyle\frac{u_i}{\hat\sigma_i}$ .

6. Obtain the new model: $y^{*} = \beta_1 + \beta_2 x_2^{*} + ... + \beta_k x_k^{*} + u^{*}$;
   - This model features no heteroskedasticity.
   - OLS is BLUE.

---

Suppose you have **serial correlation** (<u>autocorrelation</u>) and you do OLS:

1. Coefficients remain unbiased and consistent, <u>but not if there is a lagged dependent variable</u>.

$$
y_t = \beta_1 + \color{red} \beta_2 y_{t-1} \color{black} + \beta_3 x_t + u_t, \quad t = 1,2,..., T
$$

2. OLS is inefficient: better estimator exists.
3. The standard errors of $\beta_i$ are wrong:
   - In Economics, they are often biased downwards, when there is positive serial correlation.
   - In this case, the $t$ statistic is overestimated, since $t = \displaystyle\frac{\beta^{H_0} - \hat\beta}{\hat\sigma}$ .

---

Generalization of assumptions for an estimator to be BLUE:

1. The model is linear;
2. The $x$'s are non-stochastic;
3. There is no perfect multicollinearity;
4. The error has zero mean;
5. The errors are homoskedastic;
6. $u_t \perp u_s,\ \forall\ t \neq s$ (errors are independent):
   - Common model: $u_t = \rho u_{t-1} + e_t, \quad |\rho|<1$ .
7. The $u$'s and the $x$'s are uncorrelated:
   - If $y_t = \beta_1 + \beta_2 y_{t-1} + \beta_3 x_t + u_t$ and $u_t = \rho u_{t-1} + e_t$, then $y_t$ can be rewritten as $y_t = \beta_1 + \beta_2 y_{t-1} + \beta_3 x_t + \big(\rho u_{t-1} + e_t\big)$;
   - There is a clear correlation between $y_{t-1}$ and $u_{t-1}$.
8. The errors are normally distributed.