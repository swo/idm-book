# Renewal equation

Infections in the past give rise to infections in the future:

$$
  i(t) = R(t) \int_0^t i(s) w(t - s) \,ds
$$

## Instantaneous growth rate

We're interested in:

$$
  r(t) \equiv \frac{i'(t)}{i(t)} = \frac{d}{dt} \log i(t)
$$

Or, by integration:

$$
  i(t) = i(0) e^{\int_0^t r(s)\,ds}
$$

Differentiate the renewal equation:

$$
  i'(t) = R'(t) \int_0^t i(s) w(t - s) \,ds + R(t) \int_0^t i(s) w'(t - s) \,ds
$$

Divide by $i(t)$ to find:

$$
  r(t) = \frac{R'(t)}{R(t)} + \frac{R(t)}{i(t)} \int_0^t i(s) w'(t - s) \,ds
$$

## Euler-Lotka / Wallinga-Lipsitch

Assume $r(t)$ is quasi-constant over durations $a$, so that

$$
  \int_{t-a}^t r(s) \,ds \approx r(t) \times a
$$

Then? (what's the logic?)

$$
  \frac{1}{R(t)} \approx \int_0^t e^{-r(t) \cdot a} w(a) \,da
$$

E.g., if $w$ is a delta function, then $R(t) \approx e^{-Tr(t)}$.
