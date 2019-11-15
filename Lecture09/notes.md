# Lecture 09

##### Review on $F$ statistics:

$$
\begin{align}
H_0 & : 4\beta_2 - 2\beta_3 = 6 \\
H_1 & : 4\beta_2 - 2\beta_3 \neq 6
\end{align}
$$

The model:
$$
y_i = \beta_1 + \beta_2 x_{2i} + \beta_3 x_{3i} + u_i
$$

- Rewrite the restriction: $\beta_2 = \displaystyle\frac{3}{2} + \frac{1}{2}\beta_3$.
- Apply it to the model: $y_i = \beta_1 + \bigg(\displaystyle\frac{3}{2} + \frac{1}{2}\beta_3 \bigg) x_{2i} + \beta_3 x_{3i} + u_i$ .
- Rewrite the result: $y_i - \displaystyle\frac{3}{2} x_{2i} = \beta_1 + \beta_3 \bigg(\frac{1}{2}x_{2i} + x_{3i} \bigg) + u_i$.
  - It may be useful to rename the variables: $y_i^{*} = \beta_1 + \beta_3 x_i^{*} + u_i$.
- Running this regression will produce the residual sum of squares for the restricted model $RSS_{\textrm R}$.
- Running the regression on the original model, one will obtain the residual sum of squares for the unrestricted model $RSS_{\textrm{UR}}$.
- The test statistic is $F = \displaystyle \frac{RSS_{\textrm R} - RSS_{\textrm{UR}}}{p_{\textrm{UR}} - p_{\textrm R}} \cdot \frac{n-p_{\textrm{UR}}}{RSS_{\textrm{UR}}}$.
  - $n$ is the number of observations.
  - $p_{\textrm R}$ is the number of parameters in the restricted model (in the example, $2$).
  - $p_{\textrm{UR}}$ is the number of parameters in the unrestricted model ($3$, in the given example).
- The critical value is obtained from an $F$ distribution with $(p_{\textrm{UR}}-p_{\textrm R}, n-p_{\textrm{UR}})$ degrees of freedom.
- If $F > F_{\textrm{critical}}$, reject the null hypothesis.
  - Otherwise, one fails to reject the null hypothesis

***

**Review on heteroskedasticity**:

The model:
$$
y_i = \beta_1 + \beta_2 x_{2i} + ... + \beta_k x_{ki} + u_i \\
\textrm{Var}(u_i) = \sigma_i^2, \quad (i = 1,2,...,N)
$$
Models for the variance:
$$
\begin{align}
& (1) \quad \sigma_i^2 = & \sigma^2 z_i^2\\
& (2) \quad \sigma_i^2 = & \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}\\
& (3) \quad \sigma_i = & \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}\\
& (4) \quad \ln\sigma_i^2 = & \alpha_1 + \alpha_2 z_{2i} + ... + \alpha_p z_{pi}
\end{align}
$$

- One can think of the $\sigma^2$ in $(1)$ as an $\alpha$ : it is simply another parameter to estimate.
- $(1)$ is a special case of $(3)$.

Generally, solving heteroskedasticity involves dividing the original model by the standard deviation $\sigma_i$.

- Originally, $\textrm{Var}(u_i) = \sigma^2_i$ : this is the source of the problem.
- Once the model is divided by $\sigma_i$, then $\textrm{Var}\bigg(\displaystyle\frac{u_i}{\sigma_i}\bigg) = \frac{1}{\sigma^2_i} \textrm{Var}(u_i) = \frac{\sigma^2_i}{\sigma^2_i} = 1$.
  - More generally, $\textrm{Var}\bigg(\displaystyle\frac{u_i}{c\cdot\sigma_i}\bigg) = \frac{1}{c^2\cdot\sigma^2_i} \textrm{Var}(u_i) = \frac{\sigma^2_i}{c^2\sigma^2_i} = \frac{1}{c^2}$, where $c \in \R$ is a constant.
- **The brawn of most methods for correcting heteroskedasticity is to find a model to estimate the variance $\sigma_i$ by which to divide the original linear model**.
  - Considering the model of the variance $(1)$: dividing the original model by $z_i$ would have the same effect, since that is the variable that defines the behavior of $\sigma^2_i$ in the model.
  - Dividing by the original model by $\sigma \cdot z_i$ would have the same effect, given that $\sigma$ is a constant.
  - In both cases (dividing by $z_i$ or $\sigma z_i$), one will be in fact dividing the original model by a constant times the standard deviation (or rather an estimate thereof).
    - First case: $\textrm{Var}\bigg(\displaystyle\frac{u_i}{z_i}\bigg) = \frac{1}{z^2_i} \textrm{Var}(u_i) = \frac{\sigma^2 z_i^2}{z^2_i} = \sigma^2$.
    - Second case: $\textrm{Var}\bigg(\displaystyle\frac{u_i}{\sigma z_i}\bigg) = \frac{1}{\sigma^2 z^2_i} \textrm{Var}(u_i) = \frac{\sigma^2 z^2_i}{\sigma^2 z^2_i} = 1$.

And why is heteroskedasticity really a problem?

> If the variance varies with the data points, those with larger variances will be given larger weights by OLS. That means that less precise points (those with larger variances to the regression model) will have more importance in determining the parameters. When the whole model is divided by the standard deviation, it is rebalanced, since the observations with larger variances are down-weighted.

***

**Review on the Durbin-Watson test**:

Why is the test statistic $d$ between $0$ and $4$?

- Remembering:
  - The correlation of two variables is given by: $\rho_{XY} = \textrm{Corr}(X,Y) = \displaystyle\frac{\textrm{Cov}(X,Y)}{\sigma_X \sigma_Y}$, where $\textrm{Cov}(X,Y)$ is the covariance of $X$ and $Y$, while $\sigma_X$ and $\sigma_Y$ are standard deviations of those variables.
    - A population covariance is given by $\textrm{Cov}(X,Y) = \displaystyle\frac{1}{N} \sum (x_i -\bar x)(y_i - \bar y)$, where $N$ is the population size.
    - A sample covariance is given by $\textrm{Cov}(X,Y) = \displaystyle\frac{1}{n-1} \sum (x_i -\bar x)(y_i - \bar y)$, where $n$ is the sample size.
    - The covariance can also be written as a expected value: $\textrm{Cov}(X,Y) = \textrm E \big[\big(X - \textrm E [X]\big) \big(Y - \textrm E [Y]\big) \big]$.

The test statistic is given by:
$$
d = \displaystyle\frac
{\displaystyle\sum_{i=2}^N (u_i - u_{i-1})^2}
{\displaystyle\sum_{i=1}^N u_i^2}
$$

- The denominator, when divided by the number of observations, works as an estimate of the variance of $u_i$.
- If we multiply both the numerator and the denominator by $\frac{1}{N}$ and, we obtain: $d = \displaystyle\frac
  {\displaystyle\frac{1}{N} \sum_{i=2}^N (u^2_i -2u_t u_{t-1}+ u^2_{i-1})}
  {\displaystyle\frac{1}{N}\sum_{i=1}^N u_i^2}$.
  - That can be rewritten as: $d = \displaystyle\frac
    {\displaystyle\frac{1}{N} \sum_{i=2}^N u^2_i -2 \frac{1}{N} \sum_{i=2}^N u_t u_{t-1} + \frac{1}{N} \sum_{i=2}^N u^2_{i-1})}
    {\displaystyle\frac{1}{N}\sum_{i=1}^N u_i^2}$.
    - $\displaystyle\frac{1}{N}\sum_{i=1}^N u_i^2$ is an estimate of the variance $\sigma^2$.
    - $\displaystyle\frac{1}{N}\sum_{i=2}^N u_i^2$ is also an estimate of the variance, but shorter an observation (from $u_2$ to $u_N$).
    - $\displaystyle\frac{1}{N}\sum_{i=2}^N u_{i-1}^2$, too, is an estimate of the variance, shorter an observation (from $u_1$ to $u_{N-1}$).
    - $\displaystyle\frac{1}{N}\sum_{i=2}^N u_i u_{i-1}$ is an estimate of the the covariance of $u_i$ and $u_{i-1}$.
  - Thus, the test statistic can be approximated as $d \approx \displaystyle\frac{\textrm{Var}(u) - 2\textrm{Cov}(u_i, u_{i-1}) + \textrm{Var}(u)}{\textrm{Var}(u)}$.
    - That means $d \approx 2 - 2 \displaystyle\frac{\textrm{Cov}(u_,u_{i-1})}{\textrm{Var}(u)}$.
    - The correlation between a variable and itself can be written as $\textrm{Corr}(X,X) = \displaystyle\frac{\textrm{Cov}(X,X)}{\sigma_X \sigma_X} = \displaystyle\frac{\textrm{Cov}(X,X)}{\sigma_X^2}$.
    - Thus, $d \approx 2 - 2 \textrm{Corr}(u_i,u_{i-1}) = 2(1-\rho)$.
  - When there is perfect positive correlation, $\rho=1 \Rightarrow d=0$.
  - When there is perfect negative correlation, $\rho=-1\Rightarrow d=4$.
  - When there is no correlation, $\rho=0\Rightarrow d=2$.

***

**Review on the Durbin $H$ statistic**:

The model:
$$
y_t = \beta_1 + \beta_2 x_{2t} + ... + \beta_k x_{kt} + u_t \\
u_t = \rho u_{t-1} + e_t
$$
When one of $x_{jt}\ (j=2,...,k)$ is lagged variable, for instance $x_{kt} = y_{t-1}$, bias is introduced.

- From the model, we know that $y_{t-1}$ and $u_{t-1}$ are correlated.
- Since $x_{kt} = y_{t-1}$ and $u_t = \rho u_{t-1} +e_t$, there is correlation between and error term and a RHS variable.
  - According to OLS, $\hat\beta = \beta + \displaystyle\frac{\sum (x_i - \bar x)u_i}{\sum (x_i - \bar x)^2}$.
  - If we multiply both the numerator and the denominator by $\frac{1}{N}$, we get $\hat\beta = \beta + \displaystyle\frac{\frac{1}{N}\sum (x_i - \bar x)u_i}{\frac{1}{N}\sum (x_i - \bar x)^2}$.
  - Taking the expected value, we get: $\textrm E[\hat\beta] = \beta + \textrm E \Bigg[ \displaystyle\frac{\frac{1}{N}\sum (x_i - \bar x)u_i}{\frac{1}{N}\sum (x_i - \bar x)^2} \Bigg]$.
  - Then, $\textrm E[\hat\beta] = \beta + \displaystyle\frac{\textrm{Cov}(x,u)}{\textrm{Var}(x)}$.
  - So, whenever $\textrm{Corr}(x,u) \neq 0$, the estimated parameter will be biased, *id est*, $\textrm E[\hat\beta] \neq \beta$.
    - If the parameters are biased, the estimated errors $u_t$ will be biased, as well.
    - If the errors are biased, the Durbin-Watson $d$ statistic, too, will be biased.
- Then, the estimated error becomes biased, and so does the Durbin-Watson $d$ statistic.

The Durbin $H$ statistic is a means of overcoming that bias and it is given by:
$$
\begin{align}
h &= \bigg(1 - \frac{1}{2} d \bigg)\sqrt{\displaystyle\frac{T}{1-T\cdot\widehat{\textrm{Var}}(\hat\beta_j)}} \\
&= \hat\rho\sqrt{\displaystyle\frac{T}{1-T\cdot\widehat{\textrm{Var}}(\hat\beta_j)}} \sim \mathcal N (0,1)
\end{align}
$$
where $d$ is the Durbin-Watson statistic, $T$ is the length of the time series, and $\hat\beta$ is the estimated parameter for the $x_{jt}$ that equals the lagged variable.

- **This test only works if $T\cdot\widehat{\textrm{Var}}(\hat\beta_j) < 1$**.
  - Otherwise, do the Breusch-Godfrey LM test.

