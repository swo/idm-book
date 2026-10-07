# Renewal equation

Infections in the past give rise to infections in the future.
In the limit of large population, incident infections $I(t)$, reproduction number $R(t)$, and the generation interval distribution $w(\tau)$ are related by:

$$
  I(t) = R(t) \int_{-\infty}^t I(s) w(t - s) \,ds
$$

Note that the renewal equation involves a convolution:

$$
  (I * w)(t) \equiv \int_{-\infty}^t I(s) w(t - s) \,ds
             = \int_0^\infty I(t - \tau) w(\tau) \,d\tau
$$

In practice, it is difficult to measure $R(t)$ and $w(\tau)$ directly.
Instead, we used $I(t)$ to infer $R(t)$ and $w(\tau)$, then use those values to estimate $I(t)$ in the future.

## Instantaneous growth rate

Rather than work with $I(t)$ directly, it can be more convenient to work with the instantaneous growth rate $r(t)$, defined:

$$
  r(t) \equiv \frac{I'(t)}{I(t)} = \frac{d}{dt} \log I(t)
$$

Equivalently, by integration:

$$
  I(t) = I(0) \exp \left\{ \int_0^t r(s)\,ds \right\}
$$

### General relationship between reproduction number and growth rate

To find an exact formula for $r(t)$ in terms of $R(t)$, $I(t)$, and $w(\tau)$, differentiate the renewal equation, then divide by $I(t)$:

$$
  \begin{align*}
    I'(t)                     & = R'(t) \int_{-\infty}^t I(s) w(t - s) \,ds + R(t) \int_{-\infty}^t I(s) w'(t - s) \,ds \\
    r(t) = \frac{I'(t)}{I(t)} & = \frac{R'(t)}{R(t)} + \frac{R(t)}{I(t)} \int_{-\infty}^t I(s) w'(t - s) \,ds
  \end{align*}
$$

where we assumed that $w(0) = 0$.
This equation is not practicable, so we make a simplifying approximation.

### Wallinga-Lipsitch approximation

Assume there is some finite generation interval $T$ such that $w(\tau) = 0$ for $\tau > T$.
For $t > T$, the renewal equation is:

$$
  I(t) = R(t) \int_0^T I(t - \tau) w(\tau) \,d\tau
$$

with upper integral limit $T$.

At each time $t$, assume that $r(t)$ is approximately constant over the prior period $T$, so that:

$$
  I(t - \tau) = I(t) \exp \left\{ \int_{t-\tau}^t r(s) \,ds \right\}
              \approx I(t) e^{-r(t)\tau} \text{ for } 0 < \tau < T
$$

The renewal equation becomes:

$$
  \begin{align*}
    I(t)
      & = R(t) \int_0^T I(t - \tau) w(\tau) \,d\tau               \\
      & \approx R(t) \int_0^T I(t) e^{-r(t)\tau} w(\tau) \, d\tau \\
    1 & \approx R(t) \int_0^T e^{-r(t)\tau} w(\tau) \,d\tau
  \end{align*}
$$

Recall that the moment generating function for $w(\tau)$ is $M_w(r) = \int_0^\infty e^{r\tau} w(\tau) \,d\tau$, so that:

$$
  \frac{1}{R(t)} \approx M_w\big(-r(t)\big)
$$

For example, if $w(\tau)$ is a Dirac delta function, with mass at some $\tau^\star$, then $M_w(z) = e^{z \tau^\star}$, so that $R(t) \approx e^{r(t)\tau^\star}$.
If $w(\tau)$ is exponentially distributed, with mean $\tau^\star$, then $M_w(z) = 1/( 1 - z\tau^\star)$ and $R(t) \approx 1 + r \tau^\star$.

## Numerical methods

### Time discretization

For sufficiently small time slices $\Delta t$, we can approximate continuous-time-varying quantities like $I(t)$ with discrete-time vectors.
Time-discretize $I_j$ as incidence in each slice and $w_k$ as probability mass in each slice:

$$
  \begin{align*}
    I_j & \equiv \int_{j \Delta t}^{(j+1)\Delta t} I(s) \,ds       \\
    w_k & \equiv \int_{k \Delta t}^{(k+1)\Delta t} w(\tau) \,d\tau
  \end{align*}
$$

Define $K \equiv \lceil T/\Delta t\rceil$, so that $\sum_{k=0}^{K-1} w_k = 1$.
To avoid problems of causality, require that $w_0 = 0$.
(If you think there is substantial transmission happening in the first time slice, then use smaller time slices!)

The renewal equation is then:

$$
  I_j = R_j \sum_{k=0}^{K-1} I_{j-k} w_k
$$

where the $R_j$ are, trivially, the values requires to make this equation true.
We expect that $R_j \approx R(j \Delta t)$.

If working with growth rates, define the dimensionless, per-time-step growth increment $\tilde{r}_j \equiv \log (I_{j+1}/I_j)$ so that:

$$
  \log I_j = \log I_0 + \sum_{k=0}^{j-1} \tilde{r}_k
$$

Note that the growth *increment* $\tilde{r}_j$ is a dimensionless number that depends on the time slice, while the growth *rate* $r(t)$ has per-time dimension.

The increments can be approximated from the Wallinga-Lipsitch growth rates $r(t)$ but must account for the size of the time slice:

$$
  \tilde{r}_j \approx r([j + 1] \Delta t) \cdot \Delta t
$$

### Initialization

In practice, we want a simulation to begin at some $t = 0$.
The naive solution, to implicitly set $I(t) = 0$ for $t < 0$, can lead to undesirable transients.
The better solution is to explicitly set values of $I(t)$ for $-T < t < 0$ by assuming that $r(t) = r(0)$ for $t < 0$.

If $r(0)$ is specified, the result is trivial:

$$
  I(t) = I(0) e^{r(0)t} \text{ for } t < 0
$$

If $R(0)$ is specified, and $w(\tau)$ has an analytically tractable moment generating function, then one can solve the implicit equation [above](#wallinga-lipsitch-approximation) to find $r(0)$.

If only the time-discretized $w_k$ is specified, then find the root of:

$$
  0
  = \frac{1}{R(0)}
    - \sum_{k=0}^{K-1} \exp\left\{ -r(0) \cdot \left( k + 1 \right) \Delta t \right\} w_k
$$

## Further reading

- [Wallinga & Lipsitch (2007)](https://doi.org/10.1098/rspb.2006.3754)
