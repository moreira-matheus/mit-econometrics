# Lecture 14

## Simultaneity bias

Consider the model:
$$
\begin{cases}
y_t = \alpha x_t + u_t \\
x_t = \beta y_t + v_t
\end{cases}
$$
Substituting the second equation into the first one, we get the reduced-form equation:
$$
y_t = \displaystyle\frac{1}{1-\alpha\beta} (\alpha v_t + u_t)
$$
Similarly:
$$
x_t = \displaystyle\frac{1}{1-\alpha\beta} (\beta u_t + v_t)
$$
Since $x_t$ is a function of $y_t$ which, in turn, has $u_t$, there is correlation between to variable in the RHS (first equation).

- The same goes for the second equation of the system: $y_t$ is a function of $x_t$ which contains $v_t$.
- The simultaneity then introduces bias.

**Is the estimate consistent if we regress $y$ on $x$**?

- We have already seen that $\hat\alpha = \displaystyle\frac{\displaystyle\sum (x_i - \bar x)(y_i - \bar y)}{\displaystyle\sum (x_i - \bar x)^2}$.

- As $N \rightarrow \infty$, $\text{plim}\ \hat\alpha = \displaystyle\frac{\text{Cov}(x,y)}{\text{Var}(x)}$.

  - Since $y = \alpha x + u$, then:
    $$
    \displaystyle\frac{\text{Cov}(x,y)}{\text{Var}(x)} = \frac{\text{Cov}(x,\alpha x + u)}{\text{Var}(x)} = \displaystyle\frac{\alpha\text{Cov}(x,x) + \text{Cov}(x,u)}{\text{Var}(x)} = \alpha + \displaystyle\frac{\text{Cov}(x,u)}{\text{Var}(x)}.
    $$

  - Thus, $\text{plim}\ \hat\alpha = \alpha + \displaystyle\frac{\text{Cov}(x,u)}{\text{Var}(x)}$.

    - We know that $x = \displaystyle\frac{1}{1-\alpha\beta} (\beta u + v)$.
    - Then, $\text{Cov}(x,u) = \text{Cov}\Bigg(\displaystyle\frac{1}{1-\alpha\beta}(\beta u  + v),u\Bigg)$.
    - Since we assume $u \perp v$ (uncorrelated), $\text{Cov}(x,u) = \displaystyle\frac{1}{1-\alpha\beta} \bigg[ \beta\text{Cov}(u,u) + \text{Cov}(v,u) \bigg] = \frac{\beta}{1-\alpha\beta}\text{Var}(u)$. 
    - Also, $\text{Var}(x) = \Bigg( \displaystyle\frac{1}{1-\alpha\beta} \Bigg)^2 \bigg[ \text{Var} (\beta u, v)\bigg]$.
    - Then, $\text{Var}(x) = \Bigg( \displaystyle\frac{1}{1-\alpha\beta} \Bigg)^2 \bigg[ \text{Var} (\beta u) + \text{Var}(v) + 2\text{Cov}(\beta u, v)\bigg]$.
    - Again, $u \perp v \rightarrow \text{Var}(x) = \Bigg(\displaystyle\frac{1}{1-\alpha\beta}\Bigg)^2 \bigg[\beta^2\text{Var}(u) + \text{Var}(v)\bigg]$.

  - Plugging those back in and simplifying: $\text{plim}\ \hat\alpha = \alpha + \beta (1-\alpha\beta)\displaystyle\frac{\text{Var}(u)}{\beta\text{Var}(u) + \text{Var}(v)}$.

    1. $\hat\alpha$ is <u>inconsistent</u>;
    2. Unless $\beta = 0$, $\hat\alpha$ is <u>biased</u>.

###### Example:

$$
\begin{cases}
P = \beta_1 + \beta_2 W + u_P \\
W = \alpha_1 + \alpha_2 P + \alpha_3 \text{UN} + u_W \quad(\alpha_3 < 0)
\end{cases}
$$

where:

- $P$: price growth (inflation), $W$: wage growth (endogenous variables).
- $\text{UN}$: unemployment (exogenous variable).
- $u_P$ and $u_W$: stochastic noise associated with $P$ and $W$, respectively.

Substituting the second equation into the first one, we obtain the reduced-form equation for $P$:
$$
P = \displaystyle\frac{1}{1-\beta_2 \alpha_2}\bigg[(\beta_1 + \beta_2\alpha_1) + \beta_2 \alpha_3\text{UN} + (\beta_2 u_W + u_P)\bigg].
$$
Similarly:
$$
W = \displaystyle\frac{1}{1- \beta_2\alpha_2} \bigg[ (\alpha_1 + \alpha_2\beta_1) + \alpha_3 \text{UN} + (\alpha_2 u_P + u_W) \bigg].
$$
We can see above that the reduced form of $W$ has $u_P$ in it. Then, there is correlation between $W$ and $u_P$ and, consequently, $\hat\beta_2$ will be biased.

- $\text{plim}\ \hat\beta_2 = \beta_2 + \displaystyle\frac{\text{Cov}(W,u_p)}{\text{Var}(W)}$.
  - $\text{Cov}(W,u_P) = \displaystyle\frac{\alpha_2}{1-\beta_2\alpha_2} \text{Var}(u_P)$.
  - $\text{Var}(W) = \displaystyle\frac{1}{(1-\beta_2 \alpha_2)^2}\bigg[ \alpha_3^2 \text{Var}(\text{UN}) + \alpha_2^2 \text{Var}(u_P) + \text{Var}(u_W)\bigg]$.
  - Then, $\text{plim}\ \hat\beta_2 = \beta_2 + \alpha_2 \Big(1-\beta_2\alpha_2\Big) \displaystyle\frac{\text{Var}(u_P)}{\alpha_3^2 \text{Var}(\text{UN}) + \alpha_2^2 \text{Var}(u_P) + \text{Var}(u_W)}$.
- If $\alpha_2$ were equal to zero, there would be no simultaneity bias.
  - Note that, were $\alpha_2$ equal to zero, $W$ would not be a function of $P$, it would rather only be a function of the exogenous variable $\text{UN}$.

### Identification problem

###### Model 1:

$$
\begin{cases}
Q^D = \alpha_0 + \alpha_1 P + u \\
Q^S = \beta_0 + \beta_1 P + v \\
Q^D = Q^S \equiv Q
\end{cases}
$$

Reduced form:
$$
P = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1} + \frac{1}{\alpha_1 -\beta_1}(v-u) \\
$$

- $P = \lambda_0 + \varepsilon_P$:
  - $\lambda_0 = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1}$.
  - $\varepsilon_P = \displaystyle\frac{1}{\alpha_1 -\beta_1}(v-u)$.

$$
Q = \displaystyle\frac{\alpha_1 \beta_0 - \alpha_0 \beta_1}{\alpha_1 - \beta_1} + \frac{1}{\alpha_1 - \beta_1}\Big(\alpha_1 v + \beta_1 u\Big)
$$

- $Q = \gamma_0 + \varepsilon_Q$:
  - $\gamma_0 = \displaystyle\frac{\alpha_1 \beta_0 - \alpha_0 \beta_1}{\alpha_1 - \beta_1}$.
  - $\varepsilon_Q = \displaystyle\frac{1}{\alpha_1 - \beta_1}\Big(\alpha_1 v + \beta_1 u\Big)$.

To estimate the reduced form we would regress $P$ and $Q$ on constants, $\lambda_0$ and $\gamma_0$, respectively.

- $\hat\lambda_0 = \bar P$, $\hat\gamma_0 = \bar Q$.

However, we have $4$ structural parameters (unknowns) - $\alpha_0, \alpha_1, \beta_0, \beta_1$ -, while running the regression will produce two pieces of information ($\hat\lambda_0$ and $\hat\gamma_0$).

- That means that $\begin{cases} \hat\lambda_0 = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1} \\ \hat\gamma_0 = \displaystyle\frac{\alpha_1 \beta_0 - \alpha_0 \beta_1}{\alpha_1 - \beta_1} \end{cases}$ is an unidentified system (it has more unknowns than equations).

This model is said to be <u>under-identified</u>

###### Model 2:

$$
\begin{cases}
Q^D = \alpha_0 + \alpha_1 P + \alpha_2 Y + u \\
Q^S = \beta_0 + \beta_1 P + v \\
Q^D = Q^S \equiv Q
\end{cases}
$$

Reduced form:
$$
P = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1} - \frac{\alpha_2}{\alpha_1 - \beta_1} Y + \frac{1}{\alpha_1 - \beta_1} (v-u).
$$

- $P = \lambda_0 + \lambda_1 Y + \varepsilon_P$.
  - $\lambda_0 = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1}$.
  - $\lambda_1 = - \displaystyle\frac{\alpha_2}{\alpha_1 - \beta_1}$.
  - $\varepsilon_P = \displaystyle\frac{1}{\alpha_1 - \beta_1} (v-u)$.
- $Q = (\beta_0 + \beta_1 \lambda_0) + \beta_1 \lambda_1 Y + \varepsilon_Q = \gamma_0 + \gamma_1 Y + \varepsilon_Q$.

Running the regression on the reduced-form equations we obtain four estimates: $\hat\lambda_0, \hat\lambda_1, \hat\gamma_0, \hat\gamma_1$.

- Can we thus retrieve the structural parameters $\alpha_0, \alpha_1, \alpha_2, \beta_0, \beta_1$?
  - Generally, no, because, once again, we have more unknowns that equations!
  - But we can identify a subset of those structural parameters:
    - $\gamma_1 = \beta_1 \lambda_1 \Rightarrow \hat\beta_1 = \displaystyle\frac{\hat\gamma_1}{\hat\lambda_1}$.
    - $\gamma_0 = \beta_0 + \beta_1\lambda_0 \Rightarrow \hat\beta_0 = \hat\gamma_0 - \hat\beta_1 \hat\lambda_0$.

The system is then partially identified, due to the presence of the variable $Y$ which discriminates the demand curve ($Q^D$) and allows us to identify a particular supply curve ($Q^S$) for a given value of $Y$.

TO BE CONTINUED...