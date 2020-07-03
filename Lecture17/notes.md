# Lecture 17

### Discrete choice models (or qualitative response models)

Suppose $y_t$ is the probability that a household will purchase a car in a given year and $x_t$ is the household's income.

**Model**:
$$
y_t = \alpha + \beta x_t + u_t
$$
For this regression, all we observe is whether the household purchased the car or not, that is, $y_t \in \{0,1\}$.

<u>Consequences</u>:

1. The discreteness makes the errors non-normal;
2. This introduces heteroskedasticity.

<u>Demonstration</u>:

Let $P_t = \text{Pr}(y_t=1)$. Then:
$$
\begin{align}
P_t &= \text{Pr}(u_t = 1-\alpha-\beta x_t) \\
\therefore 1-P_t &= \text{Pr}(y_t=0) = \text{Pr}(u_t = -\alpha - \beta x_t)
\end{align}
$$

- For a given $x_t$, $u_t$ can only take one of two values. For that reason, $u_t$ cannot be normal; it rather follows a binomial distribution.
- We know that $\text{E}(u_t) = 0$.
  - $E(u_t) = P_t (1-\alpha-\beta x_t) + (1-P_t)(-\alpha-\beta x_t):= 0$.
  - From that, $P_t = \alpha + \beta x_t$.
- We know that $\sigma^2_u = \text{E}(u_t^2 - \bar u) = \text{E}(u_t^2)$.
  - $\text{E}(u_t^2) = P_t(1-\alpha-\beta x_t)^2 + (1-P_t)(\alpha-\beta x_t)^2$.
  - From that, $\sigma_u^2 = P_t(1-P_t)^2 + (1-P_t)(-P_t)^2$.
  - Then, $\sigma^2_u = P_t(1-P_t) = (\alpha + \beta x_t)(1-\alpha-\beta x_t)$, and it means that the variance of the errors varies with $x_t$ (heteroskedasticity).

For those reason, OLS of $\alpha$ and $\beta$ would be *unbiased* and *consistent*, but *inefficient*.

- Due to the non-normality, the test statistics would be invalid.

<u>Solution</u>:

Step 1: Estimate using OLS. Save $\boldsymbol{\hat y_t}$.

Step 2: Estimate the variance by $\hat \sigma^2_t = \hat y_t (1 - \hat y_t)$.

Step 3: Divide dependent and independent variables by $\hat\sigma_t$.

- That will produce $y_t^{*}$ and $x_t^{*}$.

Step 4: Regress $y^{*}$ on $\displaystyle\frac{1}{\sigma_t}, x^{*}$. The estimate will be BLUE.

<u>Possible problems</u>:

- In step 2, there is no guarantee that $\hat\sigma_t^2 > 0$.
- In other terms, there is no guarantee $0 \leq \hat y \leq 1$.

***

### The Probit model

Consider the model:
$$
y_t^{*} = \alpha + \beta x_t + u_t
$$
where $x_t$ is observable, but $y_t^{*}$ is not.

- An example: $y_t^{*}$ is the difference between the wage and the [reservation wage](https://en.wikipedia.org/wiki/Reservation_wage).

What one would actually observe would be:
$$
y_t =
\begin{cases}
1, & \text{if }\ \alpha + \beta x_t + u_t > 0
\quad (y_t^{*} > 0) \\
0, & \text{if }\ \alpha + \beta x_t + u_t < 0
\quad (y_t^{*} < 0)
\end{cases}
$$
Let $F(z)$ be the [cumulative normal distribution](https://en.wikipedia.org/wiki/Normal_distribution#Cumulative_distribution_function).

- Then, $F(z) = \text{Pr}(Z \leq z)$.

Thus:
$$
\begin{align}
\text{Pr}(y_t=1) & = \text{Pr}(u_t > -\alpha-\beta x_t) \\
& = 1 - F\Bigg( \displaystyle\frac{\alpha-\beta x_t}{\sigma_t} \Bigg) \\
\text{Pr}(y_t=0) & = \text{Pr}(u_t \leq -\alpha-\beta x_t) \\
& = F\Bigg( \displaystyle\frac{\alpha-\beta x_t}{\sigma_t} \Bigg)
\end{align}
$$
<u>Likelihood function</u>:
$$
L = \displaystyle\prod_{y_t=0} F\bigg(\frac{-\alpha-\beta x_t}{\sigma_t}\bigg) \prod_{y_t=1} \Bigg[1-F\bigg( \frac{-\alpha-\beta x_t}{\sigma_t} \bigg)\Bigg]
$$
Maximum Likelihood estimation: pick $\alpha$ and $\beta$ that maximize $L$.

- It is always consistent and always efficient.
- It reaches the [Cramér-Rao bound](https://en.wikipedia.org/wiki/Cram%C3%A9r%E2%80%93Rao_bound).

***

### The Logit model

$$
\ln \bigg(\frac{p}{1-p}\bigg) = \alpha + \beta x + u
$$

It works best when $0 < y < 1$.

For this model, $p_t = \displaystyle\frac{1}{1+\mathcal e^{-(\alpha + \beta x_t)}}$.

Thus:
$$
\begin{align}
& \beta x \rightarrow\infty, & p \rightarrow 1 \\
& \beta x \rightarrow -\infty, & p \rightarrow 0
\end{align}
$$
<u>Probit model</u>: errors are assumed normal ($F(z)$).

<u>Logit model</u>: errors are assumed to follow a logistic distribution $f(x) = \displaystyle\frac{\mathcal e^x}{1+ \mathcal e^x} = \frac{1}{1+\mathcal e^{-x}}$.

***

### Estimation

- If $0 < y < 1$, use OLS on $y^{*} = \ln\displaystyle\frac{y}{1-y}$.
- If $y \in \{0,1\}$, use [MLE](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation).