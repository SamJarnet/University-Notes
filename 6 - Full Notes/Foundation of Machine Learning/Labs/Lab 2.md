
Samuel Jarnet

School of Electronics and Computer Science  
University of Southampton, England  
`scj1g24@soton.ac.uk`

## Question 1.1

### 1.1.1

$$
\ell(\mu) = \log(L(\mu))=k\log(\mu) + (n-k)\log(1-\mu)
$$

$$
=> \frac {d}{d\mu}\ell(\mu) = \frac k \mu + \frac {(-1)(n-k)}{1-\mu} = \frac k \mu - \frac{n-k}{1-\mu}
$$

$$
=> \frac k \mu - \frac{n-k}{1-\mu} = 0
$$

$$
=>k - k\mu = n\mu - k\mu => \hat{\mu}= \frac k n
$$

### 1.1.2

On Jupyter notebook

### 1.1.3

They both both peak at the same time as log is strictly increasing. We use this as as n becomes large, L could become very small causing rounding errors. With logL it is on a scale without rounding errors, whilst maintaining the same peaks.

### 1.1.4

When $k=0$ or $k=n$ $\ell$ contains $\log(0)$ which is undefined. The derivative cannot be 0 at any point.

## Question 1.2

### 1.2.1

$$
\ell(\mu, \sigma^2)
= -\frac{n}{2}\log(2\pi\sigma^2)
  - \frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i-\mu)^2
$$

With respect to $\mu$

$$
\frac{\partial \ell}{\partial \mu}=\frac{\partial}{\partial \mu}\left[-\frac{n}{2}\log(2\pi \sigma^2)-\frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i-\mu)^2\right]
$$

$$
=> -\frac{1}{2\sigma^2}\sum_{i=1}^{n}2(x_i-\mu)(-1) = \frac{1}{\sigma^2}\sum_{i=1}^{n}(x_i-\mu)
$$

With respect to $\sigma^2$

$$
\frac 1 {\sigma^2}\sum_{i=1}^n(x_i - \mu) = 0 => \sum_{i=1}^nx_i - \sum_{i=1}^n \mu = 0
$$

$$
=> \sum_{i=1}^nx_i - n\mu = 0 => \hat{\mu} = \bar{x}
$$

$$
\left[
-\frac{n}{2}\log(2\pi\sigma^2)
-\frac{1}{2\sigma^2}
\sum_{i=1}^{n}(x_i-\mu)^2
\right]
$$

$$
=> -\frac{n}{2\sigma^2} + \frac 1 {2(\sigma^2)^2}\sum_{i=1}^{n}(x_i-\mu)^2 = 0
$$

$$
=> \sigma_{ml}^2 = \frac 1 n \sum_{i=1}^n(x_i - \hat{\mu})^2
$$

### 1.2.2

$\sigma^2$ is a constant when differentiating with respect to $\mu$ therefore its derivative is zero.

### 1.2.3

Mean =  2.308895027223503 Mu =  2.308895027223503 Var =  18.078710869193834 sigma2 =  18.078710869193834

### 1.2.4

ratio:  0.98 n ratio: 0.98. $\sigma_{MLE}^2 = 1/n$

## Question 1.3

### 1.3.1

$$
\ell(w, \sigma^2)=\sum_{i=1}^{n}\log\left[\frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(y_i-w^Tx_i)^2}{2\sigma^2}\right)\right]
$$

$$
=\sum_{i=1}^{n}\left[-\frac{1}{2}\log(2\pi\sigma^2)-\frac{1}{2\sigma^2}(y_iw^Tx_i)^2\right]
$$

$$
=
-\frac{n}{2}\log(2\pi\sigma^2)
-\frac{1}{2\sigma^2}
\sum_{i=1}^{n}
(y_i-w^Tx_i)^2
$$

$$
w_{MLE}=\arg\max_w\left[-\frac{n}{2}\log(2\pi\sigma^2)-\frac{1}{2\sigma^2}\sum_{i=1}^{n}(y_i-w^Tx_i)^2\right]
$$

We only have to maximise the right side that has $w$ within it. As its part is negative. Instead of maximising a negative part we can minimise a positive part and flip the sign:

$$
w_{MLE}=\arg\min_w\left[\sum_{i=1}^{n}(y_i-w^Tx_i)^2\right]
$$

We also removed constants which means $\sigma^2$ is not part of the MLE.

### 1.3.2

Column 0 and 1 are very close to the same. This means the eigenvector is very small. When we invert the matrix $X^TX$ the eigenvalues become $1/original$ which would be very large.

### 2.1.1

The eigenvalues for $X^TX + \lambda I$ are $v_1 + \lambda, ..., v_d + \lambda$.

### 2.1.2

A small $\lambda$ increases all eigenvalues by $\lambda$ but even if small, it has a large effect on the smallest eigenvalue. The smallest eigenvalue is being rescued, which means the condition number is reduced.

### 2.1.3

On notebook

### 2.1.4

variance: 75.03664033922477, bias$^2$: 0.025576906033863752, total: 75.06221724525864   \newline
variance: 0.9446050231344858, bias$^2$: 0.00027328865765890493, total: 0.9448783117921447   \newline
variance: 0.056903888000864766, bias$^2$: 0.0016710350840876357, total: 0.0585749230849524   \newline
variance: 0.03680221785844683, bias$^2$: 0.10412306196884741, total: 0.14092527982729425\newline

We sacrifice bias, meaning we introduce higher bias so that variance can be smaller.

### 2.2.1

$$
-\log p(w | D) = -\log p(D | w) - \log p(w) + const
$$

$$
w_{MAP} = \arg\min_w\left[-\log p(D | w) - \log p(w) + const\right]
$$

$$
w_{MAP} = \arg\min_w\left[\frac 1 {2\sigma^2}\sum_i(y_i-w^Tx_i)^2 + \frac 1 {2\tau^2}w^Tw\right]
$$

$$
w_{MAP} = \arg\min_w\left[\sum_i(y_i-w^Tx_i)^2 + \frac {\sigma^2} {\tau^2}w^Tw\right]
$$

Ridge: 

$$
\arg\min_w\left[\sum_i(y_i-w^Tx_i)^2 + \lambda w^Tw\right]
$$

Therefore $\lambda = \frac {\sigma^2} {\tau^2}$

### 2.2.1

On Notebook

### 2.2.3

Observations have more noise when $\sigma^2$ increases. This means the prior is relied on more strongly resulting in stronger regularisation. If $\tau^2$ increases, the prior is wider. Larger weights are punished less meaning weights don't have to be as close to zero. Lower regularisation is appropriate.

### 2.2.4

If $\lambda -> 0$ then $\tau^2 -> \infty$. This means the prior becomes extremely wide, meaning it has almost no influence. If $\lambda -> \infty$, then $\tau^2 -> 0$. The prior becomes very narrow and strongly forces the weights towards $0$. The sentence: ordinary least squares is MAP estimation with a uniform prior.

### 2.3.1

On notebook

### 2.3.2

$|w_j^{OLS}| \leq \frac \lambda 2$

$\lambda$: 0.2, $w_j^{OLS}$: [ 2.4396 -1.5051  0.7303 -0.0823  0.0048], $w_j$: [ 2.3396 -1.4051  0.6303 -0.      0.    ]

$\lambda$: 0.6, $w_j^{OLS}$: [ 2.4396 -1.5051  0.7303 -0.0823  0.0048], $w_j$: [ 2.1396 -1.2051  0.4303 -0.      0.    ]

$\lambda$: 1.2, $w_j^{OLS}$: [ 2.4396 -1.5051  0.7303 -0.0823  0.0048], $w_j$: [ 1.8396 -0.9051  0.1303 -0.      0.    ]

We can see $w_j$ becomes 0 when $|w_j^{OLS}| \leq \frac \lambda 2$.

### 2.3.3

On notebook

### 2.3.4

Lasso 0 count: 2, Ridge 0 count: 0\newline
As long as $w_j^{OLS} \neq 0$, if $\lambda$ gets larger, the denominator gets larger, so the coefficient gets closer to zero, however, for finite $\lambda$ it will never reach zero.

### 2.3.5

The Laplace prior has a sharper peak at $w=0$, meaning it hs more mass near zero than the Gaussian prior. Explanation 2: the kink at the origin accounts for the exact zeros as it explains the flat zero segment exists because | · |
has a kink at the origin

### 3.1.1
On notebook

### 3.1.2
M: 1 $\lambda$: 0 MSE: 0.20329470058789026, $\max_j |w_j|$ : 2.4984072071164745
M: 9 $\lambda$: 0 MSE: 0.005211001101476154, $\max_j |w_j|$ : 1603833.8370033398
M: 9 $\lambda$: 0.01 MSE: 0.08656581349364206, $\max_j |w_j|$ : 4.218793885347178
We can see that the max coefficient is very large (1603833.837) as expected for $M=9$ where $\lambda = 0$  and we can see that when $M=9$ but $\lambda = 0.01$ punishes large coefficients to produce smaller values.

### 3.1.3
Error:  0.33850520013375984 training set:  1
Error:  754.9909232559144 training set:  1
Error:  0.1906736248004692 training set:  1
Error:  0.21343397237824704 training set:  2
Error:  0.09696983979622747 training set:  2
Error:  0.058443863317854915 training set:  2
Error:  0.20543173679903112 training set:  3
Error:  644.0729630024375 training set:  3
Error:  0.06372115223717092 training set:  3
Error:  0.20706772866860354 training set:  4
Error:  0.1493449002730173 training set:  4
Error:  0.09818266160195219 training set:  4
Error:  0.26576095574001835 training set:  5
Error:  15.504267712887653 training set:  5
Error:  0.11348130580425311 training set:  5
Medians: [ 0.2134 15.5043  0.0982]

### 3.1.4
$M=9, \lambda = 0$ has the lowest training MSE (0.00521), but it also has the highest median error against the true function(15.504) which indicates overfitting as it is fits the point but doesn't generalise.
$M=1, \lambda=0$ has a higher training MSE (0.203) and a median error against the true function of 0.213 which shows that the model is underfitting as the model is not flexible enough to become closer to the true function.
$M=9, \lambda = 0.1$ has a MSE of 0.0865 which is not the lowest but shows closeness to the points. It has a lowest median error against the true function of 0.0982 which shows it is well-regularised and is close to the true function.

### 3.1.5 
An overfitted model has very large coefficients, a penalty on $∥w∥_2^2$ makes large coefficients costly as they contribute even more (quadtratically) to the penalty. This reduces the models abiltiy to fit noise and produces a stabler modekl. 

### 3.2.1
On notebook

### 3.2.2
Best lambda: 7.017038286703822e-05

### 3.2.3
Answer later

### 3.2.4