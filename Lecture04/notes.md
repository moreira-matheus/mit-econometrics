# Lecture 04

<u>Quick recap</u>:

Linear regression: $y_i = \beta_1 + \beta_2 x_{2i} + \beta_3 x_{3i} + ... + \beta_k x_{ki} + u_i , \quad \text{Var}(u_i) = \sigma^2_i$

Parametric models:
$$
\begin{align}
\sigma^2_i = \alpha_1 + \alpha_2 z_{2i} + \alpha_3 z_{3i} + ... + \alpha_p z_{pi} \quad\textrm{(a)} \\
\sigma_i = \alpha_1 + \alpha_2 z_{2i} + \alpha_3 z_{3i} + ... + \alpha_p z_{pi} \quad\textrm{(b)} \\
\ln\sigma^2_i = \alpha_1 + \alpha_2 z_{2i} + \alpha_3 z_{3i} + ... + \alpha_p z_{pi} \quad\textrm{(c)}
\end{align}
$$
where $\hat u^2_i$ , $|\hat u_i|$ and $\ln \hat u^2_i$ are used as estimator of $\sigma^2_i$, $\sigma_i$ and $\ln \sigma^2_i$ .

Steps:

1. Regress $y_i$ on the constant term and $x_{2i}, ..., x_{ki}$ : that produces all $\hat\beta_{OLS}$ ;
2. Save residuals: $\hat u_i = y_i - \hat\beta_1 - \hat\beta_2 x_{2i} - ... - \hat\beta_k x_{ki}$ ;

3. Apply parametric models:

   (a) square $\hat u_i$, obtain $\hat u^2_i$, and regress on constant term and $z_{2i}, ..., z_{pi}$ ;

   (b) find $|\hat u_i|$ and regress on constant term and $z_{2i}, ..., z_{pi}$ ;

   (c) find $\ln \hat u^2_i$ and regress on constant term and $z_{2i}, ..., z_{pi}$ ;

4. Compute $\textrm{LM}$ statistics: $\textrm{LM} = N \cdot R^2$ ;

<i>"So, [it is] a Lagrange Multiplier because we're comparing an unconstrained to a constrained model and looking at the difference between the maximum under the unconstrined and the maximum under the constrained. If that distance is big, we reject; if that difference is small, we don't reject. [...] Lagrange Multipliers are ways of opposing constraints on maximization problems. [...] And we're looking at the distance between the two solutions. If the constraints are valid, it shouldn't matter if they're imposed, they should be in the data anyway: the two maximums should be very close together. If the restrictions are invalid, you're imposing something false on the data, it can't find the maximum anymore, and it will be very far away from the maximum (because you imposed a false assumption on it)."</i> (Mark Thoma)

5. $\textrm{LM} \sim \chi^2 (p-1) \textrm{ d.f.}$ .

   Since 
   $$
   \begin{align}
   H_0 & : \alpha_2 = \alpha_3 = ... = \alpha_p = 0 \\
   H_1 & : \exists\ \alpha_j \neq 0\quad (j=2,3,...,p) ,
   \end{align}
   $$
    if the null hypothesis is true, then:

   (a) $\sigma^2_i = \alpha_1$ ;

   (b) $\sigma_i = \alpha_1$ ;

   (c) $\ln \sigma^2_i = \alpha_1$ .

   Then a $\chi^2$-test should be performed with $p-1$ degrees of freedom (due to the number of restriction, from $2$ to $p$) and the given level of significance.

   If the $\textrm{LM} > \chi^2_{\textrm{crit}}$, $H_0$ should be rejected, which means that there is heteroskedasticity.

   Otherwise, we fail to reject $H_0$ and we assume there to be homoskedasticity.

***

Moving on to a test based upon the model of variance $\sigma^2_i = \alpha x^2_j$ ...

### Goldfeld-Quandt test

- Sort the data in ascending order of magnitude of the explanatory variable(s) and divide it into three parts;
- Ignore the middle part (which might represent from one sixth to one third of the data);
- Perform regressions for the lowest-$x$ and highest-$x$ data points, separately;
- Estimate the variances for each of those two parts and divide the higher variance by the lowest one:
  - Not necessarily the lowest variance will stem from the lowest $x$ values!
- As previously seen, each of those two variances follows a $\chi^2$ distribution; thus, the ratio of the two follows an $\textrm{F}$ [distribution](https://en.wikipedia.org/wiki/F-distribution):
  - $\sigma^2_H \sim \chi^2(d_1),\ \sigma^2_L \sim \chi^2(d_2) \quad\Rightarrow\quad \displaystyle\frac{\sigma^2_H}{\sigma^2_L} \sim \textrm{F}(d_1, d_2)$, where, $d_1$ and $d_2$ are, respectively, the degrees of freedom in the numerator and in the denominator.
- If there is no heteroskedasticity, that ratio should be very close to one;
- On the other hand, if the ratio is significantly higher than one, then there is heteroskedasticity.

More about this test [here]([https://en.wikipedia.org/wiki/Goldfeld%E2%80%93Quandt_test](https://en.wikipedia.org/wiki/Goldfeld–Quandt_test)).

- If the errors are not normal or if the variances do not follow the expected variance model, the test will perform poorly:
  - $\textrm{LM}$ tests are more robust under those circumstances.
- The test attempts to explain the variance with only one variable:
  - That is, for $\sigma^2_i = \alpha x^2_j$, $j$ can only assume one value, so that $j \in \{1,2,..., k\}$ .

##### Detailed steps:

1. Identify a variable, say $X$, that is suspected of being positively or negatively related to the variance;

2. Divide sample into three parts:

   - Define $N_1$ and $N_2$, so that $1 < N_1 < N_2 < N$ ;

   - It is not required that $N_1 = N - N_2 + 1$, *i.e.*, that the first and the third parts have the same number of observations ;
   - The number of observations between $N_1$ and $N_2$ are usually one sixth to one third of all data;

3. Estimate two regressions: one for the first $N_1$ observations and other for the last $N - N_2 + 1$ ones;

4. Calculate $\textrm{RSS}_1 =  \displaystyle\sum_{i=1}^{N_1} \hat u^2_i$ and $\textrm{RSS}_2 = \displaystyle\sum_{i = N_2}^{N}$ ;

5. Compute $\textrm{F} = \displaystyle\frac{\hat\sigma^2_2}{\hat\sigma^2_1}$, with $\hat\sigma^2_1 = \displaystyle\frac{\textrm{RSS}_1}{N_1 - k}$ and $\hat\sigma^2_2 = \displaystyle\frac{\textrm{RSS}_2}{(N-N_2+1)-k}$ :

   - $\textrm{F} \sim F\big( N-N_2+1-k  , N_1-k \big)$ .

