# Lecture 05

### White's test

- Does not rely upon a specific form of heteroskedasticity.
- It's closely related to the model: $\sigma^{2}_i = \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}$;
  - It's a large sample $\textrm{LM}$ test;
- Does not require normality of the errors.

###### Example

$$
y_i = \beta_1 + \beta_2 x_{2i} + \beta_3 x_{3i} + u_i, \quad \textrm{Var}(u_i) = \sigma^2_i
$$

Model of the variance:
$$
\sigma^2_i = \alpha_1 + \alpha_2 x_{2i} + \alpha_3 x_{3i} + \alpha_4 x^2_{2i} + \alpha_5 x^2_{3i} + \alpha_6 x_{2i} x_{3i}
$$

- All variables, all their squares and all the (unique) inner products.

$$
\begin{align}
H_0 & : \alpha_2 = \alpha_3 = \alpha_4 = \alpha_5 = \alpha_6 = 0 \\
H_1 & : \exists\ \alpha_j \neq 0 \quad (j \in \{2,3,4,5,6\})
\end{align}
$$

- Steps:
  1. Estimate the original model by <abbr value="Ordinary Least Squares">OLS</abbr>;
  2. Find the residuals: $\hat u_i = y_i - \hat\beta_1 - \hat\beta_2 x_{2i} - \hat\beta_3 x_{3i}$ ;
  3. Regress the variance model, using $\hat u_i$ as an estimator for $\sigma^2_i$ ;
  4. Find the test statistic $N R^2$ which follows a $\chi^2$ distribution:
     - $NR^2 \sim \chi^2(p-1)$, where $p-1$ is the number of restrictions (in the example, it would be $5$, after the five $\alpha$'s in $H_0$);
  5. Compare to the critical value for the given level of significance (for instance, $\chi^2_{0.05}(5) = 11.07$):
     - If the test statistic is greater than the critical value, reject $H_0$;
     - Otherwise, we fail to reject $H_0$.

### Estimation

1. White's correction:
   - White's Heteroskedasticity-Consistent Covariance Matrix (HCCM)
   - Non-parametric test that re-weights the variable, regarding the variance (since OLS gives the variables with more variance more weight).
2. Generalized (or Weighted) Least Squares
   - Consists in re-weighting the observations.

###### Example

**Weighted Least Squares**

Linear model: $y_i = \beta_1 + \beta_2 x_{2i} + \beta_3 x_{3i} + u_i$ ;

Variance model: $\sigma^2_i = \textrm{Var for error } i$ .

Dividing both sides of the linear model by $\sigma_i$:
$$
\displaystyle\frac{y_i}{\sigma_i} = \beta_1 \displaystyle\frac{1}{\sigma_i} + \beta_2 \displaystyle\frac{x_{2i}}{\sigma_i} + \beta_3 \displaystyle\frac{x_{3i}}{\sigma_i} + \displaystyle\frac{u_i}{\sigma_i}
$$
Renaming it:
$$
y^{*}_i = \beta_1 x^{*}_{1i} + \beta_2 x^{*}_{2i} + \beta_3 x^{*}_{3i} + u^{*}_i
$$

- Because of heteroskedasticity, the OLS is not <abbr value="Best Linear Un-biased Estimator">BLUE</abbr> for the $y_i$ model; it is BLUE, however, for the $y^{*}_i$ model, in which there is no heteroskedasticity.

Why is it?

- Dividing both sides of the model by $\sigma_i$ up-weights the observations with low variance (which would otherwise be underrated by OLS) and down-weights those with high variance (overrated by OLS).

- Also, it was defined that $\textrm{Var}(u^{*}_i) := \textrm{Var}\bigg(\displaystyle\frac{u_i}{\sigma_i} \bigg)$ .
  - A property of the variance is $\textrm{Var}(a + bX) = b^2 + \textrm{Var}(X)$, where $a, b$ are constants and $X$, a random variable.
  - Then, $\textrm{Var}(u^{*}_i) := \textrm{Var}\bigg(\displaystyle\frac{u_i}{\sigma_i} \bigg) = \displaystyle\frac{1}{\sigma^2_i}\textrm{Var}(u_i)$ , since $\sigma^2_i$ is a number (constant).
  - Given that $\textrm{Var}(u_i) = \sigma^2_i$, then $\textrm{Var}(u^{*}_i) = \displaystyle\frac{1}{\sigma^2_i} \sigma^2_i = 1$.
  - With $\textrm{Var}(u^{*}_i)$ being constant, the $y^{*}_i$ model features <u>homoskedasticity</u>.
- Conclusion: by re-weighting the variables (dividing them by $\sigma_i$), it is possible to get rid of heteroskedasticity - which makes OLS BLUE -, <u>provided that $\sigma_i$ is known</u>.
  - It is possible to use the LM models for variance from Lecture 03 (*Breusch-Pagan*, *Glejser* or *Park*) to estimate $\sigma_i$ and make the procedure work.

---

### Matrix form

$$
\boldsymbol y = \boldsymbol X \boldsymbol\beta + \boldsymbol u
$$

where $\boldsymbol y = \begin{bmatrix} y_1 \\ y_2 \\ y_3 \\ \vdots \\ y_N \end{bmatrix}$ , $\boldsymbol X = \begin{bmatrix} 1 & x_{21} & x_{31} & \cdots & x_{p1} \\ 1 & x_{22} & x_{32} & \cdots & x_{p2} \\ 1 & x_{23} & x_{33} & \cdots & x_{p3}\\ \vdots & \vdots & \vdots & \cdots & \vdots \\ 1 & x_{2N} & x_{3N} & \cdots & x_{pN} \end{bmatrix}$ , $\boldsymbol\beta = \begin{bmatrix} \beta_1 \\ \beta_2 \\ \beta_3 \\ \vdots \\ \beta_p \end{bmatrix}$ , $\boldsymbol u = \begin{bmatrix} u_1 \\ u_2 \\ u_3 \\ \vdots \\ u_N \end{bmatrix}$ .

Then, the estimator is given by $\hat{\boldsymbol{\beta}}_{OLS} = \big( \boldsymbol X^T \boldsymbol X \big)^{-1}\boldsymbol  X^T \boldsymbol y$ (normal equation).

- This is the vectorized, multivariate version for $\beta = \displaystyle\frac{\sum (x_i - \bar x)(y_i - \bar y)}{\sum (x_i - \bar x)^2}$ .

$\Omega = \textrm{Var}(\boldsymbol u)$ is the variance-covariance matrix.

- $\Omega = \boldsymbol u \boldsymbol{u}^T= \begin{bmatrix} u_1 \\ u_2 \\ \vdots \\ u_N  \end{bmatrix} \begin{bmatrix} u_1 & u_2 & \cdots & u_N \end{bmatrix} = \begin{bmatrix} \sigma^2_1 & & \\ & \ddots & \\ & & \sigma^2_N \end{bmatrix} $ .
- All the elements of $ \Omega$ are inner products $u_i u_j$, so that $i,j \in \{1,2, ... , N\}$ .
  - Those in the main diagonal are the variances for each observation.
  - If the errors are uncorrelated, every $u_i u_j$ where $i\neq j$ (that is, all elements outside the main diagonal) are equal to zero.
  - If there is <u>homoskedasticity</u>, then all the element in the main diagonal are the same (*i. e.*, $\sigma^2_1 = \sigma^2_2 = \dots = \sigma^2_N$).

> "So, the problems you can run into are twofold: either the elements on the diagonal of your variance-covariance matrix are not the same (<b>heteroskedasticity</b>), or there is correlation among your errors, which is what we call **autocorrelation**."

- $\Omega$ is a positive-definite matrix (more on <abbr value="Positive-Definite Matrix">PDMs</abbr> [here](https://towardsdatascience.com/what-is-a-positive-definite-matrix-181e24085abd)):
  - As every positive-definite matrix, it can be decomposed in the form $\Omega = Q \Lambda Q^T$ - where the columns of $Q$ are the eigenvectors of $\Omega$ and the diagonal entries of matrix $\Lambda$, the respective eigenvalues (more [here](http://slpl.cse.nsysu.edu.tw/chiaping/la/pdm.pdf)).
  - Under that condition, it is possible to write $\Omega = Q I Q^T$ (where $I$ is the identity matrix), [without loss of generality](https://en.wikipedia.org/wiki/Without_loss_of_generality).
  - A correction technique consists in transforming the model so that, instead of having $\Omega$ as the variance-covariance matrix, we have $I$ .
    - $Q^{-1} \Omega (Q^{-1})^T = I \quad\Rightarrow\quad Q^{-1} \boldsymbol u \boldsymbol u^T (Q^{-1})^T = I$ .
    - $E\big(\boldsymbol u \boldsymbol u^T \big) = \begin{bmatrix} \sigma^2_1 & 0 & \cdots & 0 \\ 0 & \sigma^2_2 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & \sigma^2_N \end{bmatrix}$ .
    - That can be decomposed $E\big(\boldsymbol u \boldsymbol u^T \big) = Q I Q^T$, where $Q = Q^T = \begin{bmatrix} \sigma_1 & 0 & \cdots & 0 \\ 0 & \sigma_2 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & \sigma_N \end{bmatrix}$. Thus, $Q^{-1} = \begin{bmatrix} \frac{1}{\sigma_1} & 0 & \cdots & 0 \\ 0 & \frac{1}{\sigma_2} & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & \frac{1}{\sigma_N} \end{bmatrix}$ .

- Then, the model is re-weighted: $Q^{-1} \boldsymbol y = Q^{-1} \big( \boldsymbol X \boldsymbol \beta + \boldsymbol u \big)$ .
  - In the case shown in the previous section (WLS), the diagonal of $Q$  would formed by the variances (with zero elsewhere). Consequently, the diagonal of $Q^{-1}$ would be filled by the reciprocals of those variances: $\big(\sigma^2_i\big)^{-1}$ .
  - Then, pre-multiplying both sides of the model by $Q^{-1}$ has the same effect as dividing both sides by the variances.

- The form $\boldsymbol\beta = \big( \boldsymbol X^T \Omega^{-1} \boldsymbol X \big)^{-1} \big( \boldsymbol X^T \Omega^{-1} \boldsymbol y \big)$ - derived from the normal equation - is called **Generalized Least Squares** (GLS) estimator.
  - If there is no heteroskedasticity nor autocorrelation, $\Omega = I$ and the GLS is equal to the normal equation.
  - Otherwise, the model is re-weighted by the variance-covariance matrix.

---

Model: $y_i = \beta_1 + \beta_2 x_{2i} + \beta_3 x_{3i} + u_i$ , $\textrm{Var}(u_i) = \sigma^2_i$ .

Method: Re-weight by $\displaystyle\frac{1}{\sigma_1}$ .

**Problem**: We do not know $\sigma_i$ .

**Solution**: Use a model of variance as a way to estimate $\sigma_i$ (that is, use $\hat \sigma_i$ instead of $\sigma_i$) .

- Simplest case: $\textrm{Var}(u_i) = \sigma^2 Z^2_i \equiv \sigma^2_i$, where $Z^2_i$ is known data.
  - Then, $\sigma_i = \sigma Z_i$ ;
  - We divide the model by $Z_i$ : $\displaystyle\frac{y_i}{Z_i} = \beta_1 \displaystyle\frac{1}{Z_i} + \beta_2 \displaystyle\frac{x_{2i}}{Z_i} + \beta_3 \displaystyle\frac{x_{3i}}{Z_i} + \displaystyle\frac{u_i}{Z_i}$ .
  - Then, we re-write it: $y^{*}_i = \beta_1 x^{*}_{1i} + \beta_2 x^{*}_{2i} + \beta_3 x^{*}_{3i} + u^{*}_i$ .
  - $\textrm{Var}(u^{*}_i) = \textrm{Var}\bigg( \displaystyle\frac{u_i}{Z_i} \bigg) = \displaystyle\frac{1}{Z^2_i} \textrm{Var}(u_i) = \displaystyle\frac{1}{Z^2_i} \big(\sigma^2 Z^2_i\big) = \sigma^2$ (<u>homoskedasticity</u>) .

#### Feasible Generalized Least Squares (FGLS)

Variance models:

(a) $\sigma^2_i = \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}$ ;

(b) $\sigma_i = \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}$ ;

(c) $\ln \sigma^2_i = \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}$ .

Steps:

1. Regress $y$ on constant, $x_2, ..., x_k$ : get $\hat\beta_{OLS}$ ;
2. Compute $\hat u_i = y_i - \hat\beta_1 - \hat\beta_2 x_{2i} - ... - \hat\beta_k x_{ki}$ ;
3. (a) Regress $\hat u^2$ on constant, $z_2, ..., z_p$ : get $\hat\alpha$ and apply to $\sigma^2_i = \hat\alpha_1 + \hat\alpha_2 z_{2i} + ... + \hat\alpha_p z_{pi}$ ;
4. Divide the linear model by $\hat\sigma_i$ : $\displaystyle\frac{y_i}{\hat\sigma_i} = \beta_1 \displaystyle\frac{1}{\hat\sigma_i} + \beta_2 \displaystyle\frac{x_{2i}}{\hat\sigma_i} + ... + \beta_k \displaystyle\frac{x_{ki}}{\hat\sigma_i} + \displaystyle\frac{u_i}{\hat\sigma_i}$ .

**Problems**:

- There is no guarantee that $\hat\sigma^2_i > 0$ : use absolute value.

