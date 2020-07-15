# Lecture 19

Review on:

**Instrumental variables using two-stage least squares there is heteroskedasticity**

For a model:
$$
y_1 = \beta_1 + \beta_2 y_2 + \beta_3 x_3 + u
$$
When modeling the variance, it is possible to use OLS if the endogenous variable is left out:
$$
\sigma_i^2 = \alpha_1 + \alpha_2 x_3 + \text{error}
$$
In the original model it is still necessary to use instrumental variables, though.

**What a large sample size on White test is**

It will depend on the context of the data but:

- Short of $30$ will never be a large sample;
- At least $100$ to $200$ observations, for most applications, in order to be able to exploit the large samples properties, for instance, calculating the [rate of convergence](https://www.jstor.org/stable/2958093?seq=1).

**When to use probit and logit models**

<u>Probit</u>: useful when trying to model an unobservable variable, and what is actually observed is only a choice ($0$ or $1$).

<u>Logit</u>: an alternative to a linear probability model.

- In the linear probability model, the estimator has 1) heteroskedasticity and 2) non-normal errors and 3) there is no guarantee the result will be between $0$ and $1$.

**Proofs of bias and consistency**

Model:
$$
y_i = x^{*}_i\beta + v_i, \quad\text{where}\quad x_i = x^{*}_i + e_i
$$
Substituting:
$$
\begin{align}
y_i & = (x_i - e_i)\beta + v_i \\
& = x_i \beta + u_i
\end{align}
$$
where $u_i = (v_i - \beta e_i)$.

Then
$$
\begin{align}
\text{plim}\ \hat\beta & = \beta + \frac{\text{Cov}(x,u)}{\text{Var}(x)} \\
& = \beta + \frac{\text{Cov}(x^{*} + e,\ v - \beta e_i)}{\text{Var}(x^{*} + e)} \\
& = \beta + \frac{-\beta \sigma^2_{e}}{\sigma^2_{x^{*}} + \sigma^2_{e}} \\
& = \beta \bigg(1 - \frac{\sigma^2_{e}}{\sigma^2_{x^{*}} + \sigma^2_{e}}\bigg)
\end{align}
$$

***

For a model:
$$
y = \beta_1 + \beta_2 x + u
$$
Apropos $\beta_2$:
$$
\text{plim}\ \hat\beta_2 = \beta_2 + \frac{\text{Cov}(x,u)}{\text{Var}(x)}
$$
As for $\beta_1$:
$$
\hat\beta_1 = \bar y - \hat\beta_2 \bar x \\
\therefore \text{plim}\ \hat\beta_1 = \mu_y - \text{plim}\ \hat\beta_2 \mu_x
$$
And from that we conclude that any bias in $\hat\beta_2$ will introduce bias in $\hat\beta_1$.

Ways of *biasing* the constant $\hat\beta_1$:

- Non-zero measurement errors (which affect $\mu_y$ or $\mu_x$);
- Bias in $\hat\beta_2$.

**Structural model estimation**

When we do 2SLS, implicitly, what we are doing is:

- Starting with a structural model.
- Then, deriving the reduced form;
- Estimating the reduced form;
- And, finally, using the reduced form to recover the structural model.

The identification question is all about the possibility of recovering the structural parameters through the estimated reduced form.

For instance, for a structural model
$$
\begin{align}
Q_i & = \beta_0 + \beta_1 P_i + \beta_2 Y_i + u_i \\
Q_i & = \alpha_0 + \alpha_1 P_i + v_i 
\end{align}
$$
we obtain the reduced form:
$$
\alpha_0 + \alpha_1 P_i + v_i = \beta_0 + \beta_1 P_i + \beta_2 Y_i + u_i \\
\therefore P_i = \frac{1}{\alpha_1 - \beta_1} \bigg[ (\beta_0 - \alpha_0) + (\beta_1 - \alpha_1) P_i + \beta_2 Y_i + (u_i - v_i) \bigg]
$$
which can be rewritten as:
$$
P_i = \lambda_0 + \lambda_1 P_i + \lambda_2 Y_i + \text{error}
$$
where $\lambda_0 = \displaystyle\frac{1}{\alpha_1-\beta_1}(\beta_0-\alpha_0)$, $\lambda_1 = \displaystyle\frac{1}{\alpha_1-\beta_1}(\beta_1-\alpha_1)$ and $\lambda_2 = \displaystyle\frac{1}{\alpha_1-\beta_1}\beta_2$. 

Analogously:
$$
Q_i = \gamma_0 + \gamma_1 P_i + \gamma_2 Y_i + \text{error}
$$
Once we estimate $\lambda$'s and $\gamma$'s, we can supposedly retrieve $\alpha$'s and $\beta$'s.

If there are not enough $\lambda$ and $\gamma$ equations to solve for $\alpha$'s and $\beta$'s, the system is <u>under-identified</u>.

If there are more than enough $\lambda$ and $\gamma$ equations to solve for $\alpha$'s and $\beta$'s, the system is <u>over-identified</u>.

In that model:

- Endogenous: $Q$, $P$.
- Exogenous: constants, $Y$.

$G = \text{num. exog. variables} = 2$.

- In the first structural equation there are **no** excluded variables, then, since $G-1 > 0$, it is under-identified.
- In the second structural equation there is **one** excluded variable ($Y$), then, since $G-1 = 1$, it is exactly identified.
- Were $G-1 > \text{num. excluded variables}$, it would be over-identified.