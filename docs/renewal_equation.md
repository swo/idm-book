# Renewal equation

Infections in the past give rise to infections in the future. In the limit of
large population, incident infections $i(t)$, reproduction number $R(t)$, and
the generation interval distribution $w(\tau)$ are related by:

$$
  i(t) = R(t) \int_0^t i(s) w(t - s) \,ds
       = R(t) \int_0^t i(t - \tau) w(\tau) \,d\tau
$$

In practice, it is difficult to measure $R(t)$ and $w(\tau)$ directly. Instead,
we used $i(t)$ to infer $R(t)$ and $w(\tau)$, then use those values to estimate
$i(t)$ in the future.

## Instantaneous growth rate

Rather than work with $i(t)$ directly, it can be more convenient to work with
the instantaneous growth rate $r(t)$, defined:

$$
  r(t) \equiv \frac{i'(t)}{i(t)} = \frac{d}{dt} \log i(t)
$$

Equivalently, by integration:

$$
  i(t) = i(0) e^{\int_0^t r(s)\,ds}
$$

To find the exact relationship between $r(t)$, $R(t)$, $i(t)$, and $w(\tau)$,
differentiate the renewal equation, then divide by $i(t)$:

$$
  \begin{align*}
    i'(t)                     & = R'(t) \int_0^t i(s) w(t - s) \,ds + R(t) \int_0^t i(s) w'(t - s) \,ds \\
    r(t) = \frac{i'(t)}{i(t)} & = \frac{R'(t)}{R(t)} + \frac{R(t)}{i(t)} \int_0^t i(s) w'(t - s) \,ds
  \end{align*}
$$

where we assumed that $w(0) = 0$. This equation is not practicable, so we make a
simplifying approximation.

### Wallinga-Lipsitch approximation

At each time $t$, assume that, over a past time period $a$, $r(t)$ is
approximately constant, so that:

$$
  i(t - \tau) \approx i(t) e^{-r(t)\tau}
$$

The renewal equation becomes:

$$
  \begin{align*}
    i(t)
      & = R(t) \int_0^t i(t - \tau) w(\tau) \,d\tau               \\
      & \approx R(t) \int_0^t i(t) e^{-r(t)\tau} w(\tau) \, d\tau \\
    1 & = R(t) \int_0^t e^{-r(t)\tau} w(\tau) \, d\tau
  \end{align*}
$$

Recall that the moment generating function for $w(\tau)$ is
$M_w(r) = \int_0^\infty e^{-r\tau} w(\tau) \,d\tau$, so that:

$$
  R(t) \approx M_w(-r(t))
$$

(Strictly speaking, we should look at the *truncated* moment generating
function, but this is only relevant as a transient at the start of the time
series.)

For example, if $w(\tau)$ is a Dirac delta function, with mass at some
$\tau^\star$, $M_w(-r) = e^{-r \tau^\star}$, so that
$R(t) \approx e^{r(t)\tau^\star}$. If $w(\tau)$ is exponentially distributed,
with mean $\tau^\star$, then $M_w(-r) = 1/\left[ 1 + (r/\tau^\star) \right]$ and
$R(t) \approx 1 + r \tau^\star$.

## Further reading

- [Wallinga & Lipsitch (2007)](https://doi.org/10.1098/rspb.2006.3754)
