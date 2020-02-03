# Lecture 13

### Structural Equations

Usually take the form $\text{endogenous} = f(\text{endogenous}, \text{exogenous})$.

Example 1:
$$
\begin{cases}
Q^D = \alpha_0 + \alpha_1 P + \alpha_2 Y + u \\
Q^S = \beta_0 + \beta_1 P + \beta_2 r + v \\
Q^D = Q^S
\end{cases}
$$

- The variables are:
  - $Q^D$: quantity demanded, $Q^S$: quantity supplied;
  - $P$: price;
  - $Y$: income, $r$: rainfall.
    - To know more about the *rainfall* variable, see the Model IV in Professor [Jeffrey A. Parker](https://www.reed.edu/economics/parker/)'s [notes](./JeffreyAParker_Notes10.pdf) and Section 9.2, p. 253, of [Hanushek & Jackson, 1977](http://hanushek.stanford.edu/publications/statistical-methods-social-scientists).
- There are $2$ behavioral equations and $1$ equilibrium condition.
- More on simultaneous supply and demand equations [here](http://rstudio-pubs-static.s3.amazonaws.com/195495_d47be7c818424a3c9bfa5452dd17c6c6.html).

![](supply-demand.PNG)

- The system has $2$ endogenous variables ($Q \equiv Q^D = Q^S$ and $P$) and $3$ exogenous variables ($Y$, $r$ and the constants*).
  - Didactically, the constants will be the column of ones added to the model, which multiplies $\alpha_0$, $\beta_0$ etc.
  - <u>The number of endogenous variables will be denoted as</u> $G$.
    - In the supply and demand model above, $G=2$.
  - <u>The number of exogenous variables will be denoted as</u> $K$.
    - In the supply and demand model above, $K=3$.

Example 2:
$$
\begin{cases}
C_t = \alpha_0 + \alpha_1 Y^D_t + \alpha_2 Y^D_{t-1} + u_t \\
I_t = \beta_0 + \beta_1 Y_t + \beta_2 Y_{t-1} + v_t \\
Y_t = C_t + I_t + G_t \\
Y^D_t \equiv Y_t - T_t
\end{cases}
$$

- The variables are:
  - $C_t$: consumption, $I_t$: investment, $Y^D_t$: disposable income;
  - $G_t$: government spending, $Y_t$: income, $T_t$: taxes.
- There are $2$ behavioral equations, $1$ equilibrium condition and $1$ [identity](https://en.wikipedia.org/wiki/Identity_(mathematics)).
- The system features:
  - $4$ endogenous variables ($Y_t$, $C_t$, $I_t$, $Y^D_T$);
  - $2$ predetermined variables ($Y^D_{t-1}$, $Y_{t-1}$), which were endogenous in the previous step ($t-1$), but now work *as if they were* exogenous;
  - $3$ exogenous variables ($G_t$, $T_t$ and the constants).

Another type of equation that can feature in simultaneous models is the technical equation.

- One notable example is the production function $Y = f(K,L)$.
  - E. g., $\ln Y = d_0 + d_1 \ln K + d_2 \ln L$.
- Rather than modeling a behavior, this type of equation describes the transformation of inputs into output.

### Reduced-form equations

Take the form $\text{endogenous} = f(\text{exogenous})$.

Resuming the supply-demand model:
$$
\begin{cases}
Q = \alpha_0 + \alpha_1 P + \alpha_2 Y + u \\
Q = \beta_0 + \beta_1 P + \beta_2 r + v
\end{cases}
$$

- Putting the two equation together, we get: $\alpha_0 + \alpha_1 P + \alpha_2 Y + u = \beta_0 + \beta_1 P + \beta_2 r + v$.
  - Solving for $P$ : $P = \displaystyle\frac{1}{\alpha_1 - \beta_1} \bigg[ (\beta_0 - \alpha_0) - \alpha_2 Y + \beta_2 r + v - u \bigg]$.
  - That can be rewritten as: $P = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1} - \frac{\alpha_2}{\alpha_1 - \beta_1} Y + \frac{\beta_2}{\alpha_1 - \beta_1} r + \frac{v-u}{\alpha_1 - \beta_1}$, which is <u>the reduced form equation for</u> $P$.
- For purposes of simplification, the equation will be rewritten as $P = \lambda_0 + \lambda_1 Y + \lambda_2 r + \varepsilon_1$:
  - $\lambda_0 = \displaystyle\frac{\beta_0 - \alpha_0}{\alpha_1 - \beta_1}$;
  - $\lambda_1 = - \displaystyle\frac{\alpha_2}{\alpha_1 - \beta_1}$;
  - $\lambda_2 = \displaystyle\frac{\beta_2}{\alpha_1 - \beta_1}$;
  - $\varepsilon_1 = \displaystyle\frac{v-u}{\alpha_1 - \beta_1}$.
- Thus, to solve it for $Q$, we plug $P$ back into one the original equations:
  - For the first equation, $Q = \alpha_0 + \alpha_1 \big(\lambda_0 + \lambda_1 Y + \lambda_2 r + \varepsilon_1 \big) + \alpha_2 Y + u$.
  - Rewriting: $Q = (\alpha_0 + \alpha_1 \lambda_0) + (\alpha_1 \lambda_1 + \alpha_2) Y + \alpha_1 \lambda_2 r + (u + \alpha_1 \varepsilon_1)$. This is <u>the reduced form equation for</u> $Q$.
- Again, for purposes of simplification: $Q = \gamma_0 + \gamma_1 Y + \gamma_2 r + \varepsilon_2$.
  - $\gamma_0 = \alpha_0 + \alpha_1 \lambda_0$;
  - $\gamma_1 = \alpha_1 \lambda_1 + \alpha_2$;
  - $\gamma_2 = \alpha_1 \lambda_2$.
  - $\varepsilon_2 = u + \alpha_1 \varepsilon_1$.
- The reduced form of this system is, then, $\begin{cases} P = \lambda_0 + \lambda_1 Y + \lambda_2 r + \varepsilon_1 \\ Q = \gamma_0 + \gamma_1 Y + \gamma_2 r + \varepsilon_2 \end{cases}$.

Resuming the income model:
$$
\begin{cases}
C_t = \alpha_0 + \alpha_1 Y^D_t + \alpha_2 Y^D_{t-1} + u_t \\
I_t = \beta_0 + \beta_1 Y_t + \beta_2 Y_{t-1} + v_t \\
Y_t = C_t + I_t + G_t \\
Y^D_t \equiv Y_t - T_t
\end{cases}
$$

- We can solve it for $Y_t$ by substituting the other LHS variables into its equation:
  - $\begin{align} Y_t & = (\alpha_0 + \alpha_1 Y^D_t + \alpha_2 Y^D_{t-1} + u_t) + (\beta_0 + \beta_1 Y_t + \beta_2 Y_{t-1} + v_t) + G_t \\ & = \alpha_0 + \alpha_1 (Y_t - T_t) + \alpha_2 (Y_{t-1} - T_{t-1}) + u_t + \beta_0 + \beta_1 Y_t + \beta_2 Y_{t-1} + v_t + G_t \end{align}$.
  - Isolating $Y_t$: $Y_t (1 -\alpha_1 - \beta_1) = (\alpha_0 + \beta_0) -\alpha_1 T_t - \alpha_2 T_{t-1} + (\alpha_2 + \beta_2) Y_{t-1} + G_t + u_t +v_t$.
  - Rewriting: $Y_t = \displaystyle\frac{\alpha_0 + \beta_0}{1-\alpha_1-\beta_1} - \frac{\alpha_1}{1-\alpha_1-\beta_1} T_t - \frac{\alpha_2}{1-\alpha_1-\beta_1} T_{t-1} + \frac{\alpha_2 + \beta_2}{1-\alpha_1-\beta_1} Y_{t-1} + \frac{1}{1-\alpha_1-\beta_1} G_t + \frac{u_t + v_t}{1-\alpha_1-\beta_1}$.
- Simplifying: $Y_t = \lambda_0 + \lambda_1 T_t + \lambda_2 T_{t-1} + \lambda_3 Y_{t-1} + \lambda_4 G_t + \varepsilon^Y_t$, which is the reduced form equation for $Y_t$.
  - $\lambda_0 = \displaystyle\frac{\alpha_0 + \beta_0}{1 - \alpha_1 - \beta_1}$;
  - $\lambda_1 = -\displaystyle\frac{\alpha_1}{1 - \alpha_1 - \beta_1}$;
  - $\lambda_2 = -\displaystyle\frac{\alpha_2}{1 - \alpha_1 - \beta_1}$;
  - $\lambda_3 = \displaystyle\frac{\alpha_2 + \beta_2}{1 - \alpha_1 - \beta_1}$;
  - $\lambda_4 = \displaystyle\frac{1}{1 - \alpha_1 - \beta_1}$;
  - $\varepsilon^Y_t = \displaystyle\frac{u_t + v_t}{1 - \alpha_1 - \beta_1}$.

### Simultaneity bias

Consider the simple model:
$$
\begin{cases}
y_t = \alpha x_t + u_t \\
x_t = \beta y_t + v_t
\end{cases}
$$
In this case, $x_t$ is function of $y_t$ which, in turn, is a function of $u_t$.

- The terms $x_t$ and $u_t$ in the first equation are correlated.
  - Then, any estimate of $\alpha$ will be biased.
  - As seen before, $\text{plim}\ \hat\alpha = \alpha + \displaystyle\frac{\text{Cov}(x,u)}{\text{Var}(x)}$.

- Were $\beta$ equal to zero, there would not be bias.
  - There would be a correlation between $x_t$ and $u_t$, given that $x_t$ would not be a function of $y_t$.
  - In that case, $x_t$ would then be an exogenous variable, since $v_t$ is random.

- The reduced form equations for $y_t$ and $x_t$ are: $\begin{cases} y_t = \displaystyle\frac{1}{1 - \alpha \beta}(\alpha v_t + u_t) \\ x_t = \displaystyle\frac{1}{1 - \alpha\beta}(\beta u_t + v_t) \end{cases}$.
  - That being so, $\text{Var}(x) = \bigg( \displaystyle\frac{1}{1 - \alpha\beta} \bigg)^2 \Big[ \beta^2 \text{Var}(u) + \text{Var}(v) \Big]$.

TO BE CONTINUED...