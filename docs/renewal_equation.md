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
