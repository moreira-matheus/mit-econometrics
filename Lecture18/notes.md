# Lecture 18

### Linear probability model

$$
y_i = \alpha + \beta x_i + u_i
$$

where $y_i \in \{0,1\}$.

<u>Problems</u>:

1. $u_i$ not normal;
2. $u_i$ heteroskedastic.

<u>Solution</u>: as usual, re-weight by the reciprocal of the estimated std. deviation.

### Probit model

$$
y_i^{*} = \alpha + \beta x_i + u_i
$$

where $y_i^{*}$ is unobservable. What is actually observed is:
$$
y_i =
\begin{cases}
1, & \alpha + \beta x_i + u_i > 0 \\
0, & \alpha + \beta x_i + u_i < 0
\end{cases}
$$
This has [likelihood function](https://en.wikipedia.org/wiki/Likelihood_function):
$$
\mathcal L = \prod_{y_i = 0} F\bigg(\frac{-\alpha -\beta x_i}{\sigma_i}\bigg) \prod_{y_i=1} \Bigg[1-F\bigg(\frac{-\alpha -\beta x_i}{\sigma_i}\bigg)\Bigg]
$$
Solution: [MLE](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation).

### Logit model

$$
\ln \bigg(\frac{p}{1-p}\bigg) = \alpha + \beta x + u
$$

where $0 < p < 1$.

Estimate this equation, then find:
$$
p = \frac{1}{1+\mathcal e^{-(\alpha + \beta x + u)}}
$$
<u>Advantage</u>: guaranteed that $0 < \hat p_i < 1$.

***

#### Lessons:

1. If data is such that $0 < y_i < 1$, use OLS to estimate $\ln\bigg(\displaystyle\frac{y_i}{1-y_i}\bigg)$.
2. If $y_i \in \{0,1\}$, use MLE.

***

### Limited Dependent Variables

Consider the model:
$$
y_i = \alpha + \beta x_i + u_i
$$
where $y_i$ cannot be negative. In other terms:
$$
y_i =
\begin{cases}
\alpha + \beta x_i + u_i, & y_i > 0 \\
0, & y_i \leq 0
\end{cases}
$$

- The truncation of the data will produce a **biased slope** and a **biased intercept**.

If $u \sim \mathcal N(0, \sigma^2)$, **use MLE**.

***

### Maximum Likelihood Estimation

Suppose that $X \sim \mathcal N (\mu, 10)$ (known variance) and one draws a sample of, say, $500$ observations.

- Suppose the sample mean is $\bar X = 24.5$.
- Then, most likely, the data were drawn from $\mathcal N (24.5, 10)$.

<u>More generally</u>:

Let $X$ be a random variable with a probability density function depending on unknown parameters $\boldsymbol{\theta}$.

*Example*:
$$
f(x|\mu, \sigma^2) = \frac{1}{\sigma\sqrt{2\pi}} \exp \bigg\{-\frac{(x-\mu)}{2\sigma^2}\bigg\}
$$
If we assume draws are independent, for a random sample $x_1, x_2, ..., x_n$, then $f(x_1|\boldsymbol\theta) f(x_2|\boldsymbol\theta)...f(x_n|\boldsymbol\theta)$ is called the **likelihood function**.
$$
\mathcal L(\boldsymbol\theta | x) = \prod_{i=1}^n f(x_i|\boldsymbol\theta)
$$
To maximize $\mathcal L$, choose $\boldsymbol\theta$ such that $\displaystyle\frac{\partial \mathcal L}{\partial \boldsymbol\theta} = 0,\ \frac{\partial^2 \mathcal L}{\partial \boldsymbol\theta^2} < 0$.

To simplify, take the log ([monotonic transformation](https://en.wikipedia.org/wiki/Monotonic_function#Monotonic_transformation), i.e., it does not change the maximum).
$$
\ln\mathcal L(\boldsymbol\theta|x) = \sum_{i=1}^n \ln f(x_i|\boldsymbol\theta)
$$
Then, choose $\boldsymbol\theta$ such that $\displaystyle\frac{\partial \ln\mathcal L}{\partial \boldsymbol\theta} = 0,\ \frac{\partial^2 \ln\mathcal L}{\partial \boldsymbol\theta^2} < 0$.

**Properties of MLE**:

1. Consistent, but biased in small samples;
2. Asymptotically efficient, that is, for large $n$, no other consistent estimator has a smaller variance.
3. The estimates are asymptotically normal (true even if underlying distribution of $X$ is non-normal).

*Example 1*:

Assume $X \sim \mathcal N (\mu, \sigma^2)$ and a sample $x_1, x_2, ..., x_n$.

For individual observations:
$$
f(x_i|\mu, \sigma^2) = \frac{1}{\sigma \sqrt{2\pi}}\ \exp \bigg\{-\frac{(x_i-\mu)}{2\sigma^2}\bigg\}
$$
The likelihood function:
$$
\mathcal L(\hat\mu,\hat\sigma^2 | x) = \prod_{i=1}^n \Bigg[\frac{1}{\sigma \sqrt{2\pi}}\ \exp \bigg\{-\frac{(x_i-\mu)}{2\sigma^2}\bigg\} \Bigg]
$$
The log-likelihood function:
$$
\ln \mathcal L(\hat\mu,\hat\sigma^2|x) = -n \ln \hat\sigma - \frac{n}{2} \ln 2\pi - \frac{1}{2\hat\sigma^2} \sum_{i=1}^n \big( x_i-\hat\mu \big)^2
$$
Taking the derivative for $\hat\mu$:
$$
\begin{align}
\frac{\partial \ln \mathcal L}{\partial \hat\mu} & = -\frac{2}{2\hat\sigma^2} \sum_{i=1}^n (x_i-\hat\mu)(-\hat\mu) := 0\\
& = \sum_{i=1}^n (x_i - \hat\mu) := 0 \\
& \therefore \sum x_i = n \hat\mu \quad\Rightarrow\quad \hat\mu = \frac{1}{n}\sum x_i
\end{align}
$$
Taking the derivative for $\hat\sigma$:
$$
\begin{align}
\frac{\partial \ln \mathcal L}{\partial \hat\sigma} & = -\frac{n}{\hat\sigma} - \bigg(-\frac{4\hat\sigma}{4\hat\sigma^4}\bigg) \sum(x_i - \mu)^2 := 0 \\
& = -\frac{n}{\hat\sigma} + \frac{1}{\hat\sigma^3} \sum(x_i - \mu)^2 := 0 \\
& \therefore\ \frac{1}{\sigma^2} \sum(x_i - \mu)^2 = N \quad\Rightarrow\quad \hat\sigma^2 = \frac{1}{n} \sum (x_i - \mu)^2 
\end{align}
$$
For an estimated mean (and [unbiased estimator of the variance](https://en.wikipedia.org/wiki/Unbiased_estimation_of_standard_deviation)): $\hat\sigma^2 = \displaystyle\frac{1}{n-1}\sum (x_i - \bar x)$.

*Example 2*:

Suppose:
$$
y_i = x_i \beta + u_i
$$
Assuming $u_i \sim \mathcal N (0, \sigma^2)$, then:
$$
\begin{align}
\mathcal L (\hat\beta, \sigma|x) & = \prod_{i=1}^n \frac{1}{\sigma\sqrt{2\pi}} \exp\bigg\{-\frac{\hat u_i^2}{2\sigma^2}\bigg\} \\
& = \prod_{i=1}^n \frac{1}{\sigma\sqrt{2\pi}} \exp\bigg\{-\frac{(y_i - x_i \beta)^2}{2\sigma^2}\bigg\}
\end{align}
$$
Taking the $\text{log}$:
$$
\ln \mathcal L (\hat\beta, \sigma|x) = -n\ln \sigma - \frac{n}{2}\ln 2\pi - \frac{1}{2\sigma^2}\sum(y_i-x_i\beta)^2
$$
Thus, $\max\ \underset{\hat\beta}{\ln \mathcal L}$ is equivalent to $\min\ \underset{\hat\beta}{\text{SSE}} = \sum (y_i - x_i\beta)^2$.