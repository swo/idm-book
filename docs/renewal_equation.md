# Renewal equation

Infections in the past give rise to infections in the future. In the limit of
large population, incident infections $i(t)$, reproduction number $R(t)$, and
the generation interval distribution $w(\tau)$ are related by:

$$
  i(t) = R(t) \int_0^t i(s) w(t - s) \,ds
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

where we assumed that $w(0) = 0$. This equation is essentially unworkable, so we
make a simplifying approximation.

### Wallinga-Lipsitch approximation

- Write the form of the Euler-Lotka equation that is relevant here
- Assume $r(t)$ is quasi-constant over durations $a$
- Show how this relates to the moment generating function
- Give the exponential and delta function examples
