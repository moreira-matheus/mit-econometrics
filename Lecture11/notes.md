# Lecture 11

#### Stochastic Regressors & Measurement Errors

There are random variables in the RHS.

- When those variables are correlated with the errors, there is a bias problem.
- There may also be a consistency problem.

For a two-variable model: $y_i = \beta_1 + \beta_2 x_{i} + u_i$.

According to OLS, $\hat \beta_2 = \displaystyle\frac{\sum (x_i - \bar x)(y_i - \bar y)}{\sum (x_i - \bar x)^2}$.

- We also know that $\hat\beta_2 = \beta_2 + \displaystyle\frac{\sum (x_i - \bar x)(u_i - \bar u)}{\sum (x_i - \bar x)^2}$.
  - Since $\bar u$ is expected to be zero, it is sometimes omitted.
  - Demonstration: We know that $\bar y = \beta_1 + \beta_2 \bar x$. We subtract it from the original model, then we have $y_i - \bar y = \beta_2(x_i - \bar x) + (u_i - \bar u)$. Plugging it into the formula for $\hat \beta_2$, we obtain $\hat\beta_2 = \displaystyle\frac{\sum \Bigg\{(x_i - \bar x)\bigg[\beta_2 (x_i - \bar x) + (u_i - \bar u)\bigg]\Bigg\}}{\sum (x_i -\bar x)^2}$, which can be rewritten as $\hat\beta_2 = \beta_2 \displaystyle\frac{\sum (x_1 - \bar x)^2}{\sum (x_1 - \bar x)^2} + \frac{\sum (x_1 - \bar x)(u_i-\bar u)}{\sum (x_1 - \bar x)^2}$.
- So, if $\textrm{E}\Bigg[ \displaystyle\frac{\sum (x_i - \bar x)(u_i - \bar u)}{\sum (x_i - \bar x)^2} \Bigg] \neq 0$, $\hat\beta_2$ is <u>biased</u>, that is, $\textrm{E}\Big[\hat\beta_2\Big] \neq \beta_2$.
- And if $N \rightarrow \infty : \displaystyle\frac{\sum (x_i - \bar x)(u_i - \bar u)}{\sum (x_i - \bar x)^2} \nrightarrow 0$, $\hat\beta_2$ is <u>inconsistent</u>, that is, $\hat\beta_2 \nrightarrow \beta_2$ or $\textrm{plim}\ \hat\beta_2 \neq \beta_2$.
  - If we multiply both the numerator and the denominator on the RHS by $\frac{1}{N}$, they become estimates of the covariance of $x$ and $u$ and variance of $x$, respectively.
  - As $N$ approaches infinity, the estimates tend to the true values, that is, $\displaystyle\frac{1}{N}\sum (x_i - \bar x)(u_i - \bar u) \rightarrow \textrm{Cov}(x,u)$ and $\displaystyle\frac{1}{N}\sum (x_i - \bar x)^2 \rightarrow \textrm{Var}(x)$ 
    - $\textrm{Var}(x)$ may also be written as $\sigma_x^2$.
  - If $x$ and $u$ **are not independent**, then $\displaystyle\frac{\textrm{Cov}(x,u)}{\textrm{Var}(x)} \neq 0$.

**Measurement errors**:

There are two kinds of measurement errors:

1. Error in the $x$'s: bias, consistency problems.
2. Error in the $y$'s: not a big problem.

Suppose the true relationship is given by $y_i = \beta_1 + \beta_2 z_i + v_i$.

We cannot, however, measure $z_i$ directly; instead, we have a noisy measure $x_i = z_i + w_i$.

- $x_i$: measure.
- $z_i$: true value.
- $w_i$: measurement error.

Let us call $\textrm{Var}(z_i) = \sigma_z^2$ and $\textrm{Var}(w_i) = \sigma_w^2$, and assume that the measurement error and the true value are independent, $w_i \perp z_i$.

- That means that the measurement error is not a function of the measured variable's true value.

Thus, the model can be rewritten as $y_i = \beta_1 + \beta_2 (x_i - w_i) + v_i$ or even $y_i = \beta_1 + \beta_2 x_i + (v_i - \beta_2 w_i)$.

- Let $u_i = v_i - \beta_2 w_i$.
- Then, $y_i = \beta_1 + \beta_2 x_i + u_i$.

Now, since $x_i = z_i + w_i$ and $u_i = v_i - \beta_2 w_i$ (both $x_i$ and $u_i$ depend on $w_i$), there is correlation between a RHS variable and the errors.

We know that $x = z + w$.

- Then $\textrm{Var}(x) = \textrm{Var}(z+w)
   = \textrm{Var}(z) + \textrm{Var}(w) + 2 \textrm{Cov}(z,w)$.
- Since $z \perp w$, then $\textrm{Cov}(z,w) = 0$ and $\textrm{Var}(z+w)
   = \textrm{Var}(z) + \textrm{Var}(w) = \sigma_z^2 + \sigma_w^2$.

We also know that $u = v - \beta_2 w$.

- Then, $\textrm{Cov}(x,u) = \textrm{Cov}(z+w, v-\beta_2 w)$.
- Applying the [properties](https://en.wikipedia.org/wiki/Covariance#Properties) of the covariance, we rewrite it as $\textrm{Cov}(x,u) = \textrm{Cov}(z,v-\beta_2 w) + \textrm{Cov}(w,v-\beta_2 w)$.
  - It can broken down again into $\textrm{Cov}(x,u) = \textrm{Cov}(z,v) - \beta_2 \textrm{Cov}(z,w) + \textrm{Cov}(w,v) - \beta_2 \textrm{Cov}(w,w)$.
  - Since $z \perp v$, then $\textrm{Cov}(z,v) = 0$.
  - Since $z \perp w$ (by assumption), then $\textrm{Cov}(z,w) = 0$.
  - Since $w \perp v$ (unrelated), then $\textrm{Cov}(w,v) = 0$.
- In the end, $\textrm{Cov}(x,u) = -\beta_2 \textrm{Cov}(w,w) = -\beta_2 \sigma_w^2$.

We have already seen that $\textrm{plim}\ \hat\beta_2 = \beta_2 + \displaystyle\frac{\textrm{Cov}(x,u)}{\textrm{Var}(x)}$.

- Thus, $\textrm{plim}\ \hat\beta_2 = \beta_2 -\beta_2 \displaystyle\frac{\sigma_w^2}{\sigma_z^2 + \sigma_w^2}$.
  - If there is no measurement error whatsoever, $\sigma_w^2 = 0 \rightarrow \textrm{plim}\ \hat\beta_2 = \beta_2$ (consistency).
  - As the variance of the measurement error grows, that is, $\sigma_w^2 \rightarrow \infty$, the estimated coefficient gets biased towards zero.

What if the measurement error is in the dependent variable ($y$)?

True relationship: $Q_i = \beta_1 + \beta_2 x_i + u_i$.

Measured variable: $y_i = Q_i + r_i$, where $r_i$ is the measurement error.

- Then, $y_i - r_i = \beta_1 + \beta_2 x_i + u_i$.
- It can be rewritten as $y_i = \beta_1 + \beta_2 x_i + (u_i + r_i)$.
  - By assumption, $x_i$ and $u_i$ are not related ($x_i \perp u_i$).
  - And, according to the definition of the measured variable, $x_i$ and $r_i$ are correlated either ($x_i \perp r_i$).
- Then, the error might get a bit bigger, but there is no bias nor inconsistency.

**Imperfect proxies**:

> "When you use [proxies](https://en.wikipedia.org/wiki/Proxy_(statistics)) for the real variables, you are going to introduce bias."
>
> > "If you could show that there is a tight relationship between, say, house size and what you pay for it - and there probably is -, then your proxy is probably pretty *darn* good."
> >
> > "But it there is not a tight relationship between your proxy and the actual variable, you may be introducing quite a bit of bias."