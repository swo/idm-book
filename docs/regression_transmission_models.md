# Regression transmission models

[Asher (2018)](https://doi.org/10.1016/j.epidem.2017.02.009) introduced a conceptual and mathematical framework, called _regression transmission modeling_, that treats diverse disease modeling concepts, including depletion of susceptibles, behavioral changes, and public health interventions, as terms in a regression:

> "[R]egression transmission models" [attempt] to consider outbreak forecasting as a problem of fitting an appropriate statistical model to the time-series of the reproductive number as a function of time.

## Motivation

### Dynamics as regression

Consider a simple infectious disease model that treats the growth rate $r(t)$ of infections as a random walk in a discrete time space:

$$
\log r(t) = \log r(t-1) + \sigma Z(t)
$$

where $\sigma$ is the dispersion of the random walk and $Z(t) \overset{\mathrm{iid}}{\sim} \mathcal{N}(0, 1)$.

To make the model more descriptive, we might add more features. For example, we might want to add a public health intervention that reduces the transmission rate by some amount $a$ starting on some date $t_\mathrm{start}$. Then we would add a term:

$$
\log r(t) = \log r(t-1) + \sigma Z(t) - a \, h(t - t_\mathrm{start})
$$

where $h(\cdot)$ is a [step function](https://en.wikipedia.org/wiki/Heaviside_step_function).

Alternatively, or in addition, we might suspect that behavior changes reduce the transmission rate in proportion to the number of infections. For example, more people might stay home and avoid contact with others when the outbreak is larger. We could model this feature by adding a term:

$$
\log r(t) = \log r(t-1) + \sigma Z(t) - \alpha I(t)
$$

Note that these added features manifest as terms in a regression of $(\log r)'(t) = \log r(t) - \log r(t-1)$ against constant terms like $h(t - t_\mathrm{start})$, $I(t)$, and $Z(t)$.

### Depletion of susceptibles

More complex dynamics, including the depletion of susceptibles, can also manifest as terms in this regression. In a traditional ODE SIR model, the dynamics are driven by the depletion of susceptibles:

$$
S'(t) = -\frac{\beta}{N} S(t) I(t)
$$

Thus, the growth rate of the number of infections is

$$
r(t) = -\frac{S'(t)}{I(t)} = -\frac{\beta}{N} S(t)
$$

The rate of change in the logarithm of the growth rate is proportional to the number of infections:

$$
(\log r)'(t) = \frac{r'(t)}{r(t)} = \frac{S'(t)}{S(t)} = -\frac{\beta}{N} I(t)
$$

In this way, the depletion of susceptibles manifests as a contribution to the $I(t)$ term in a regression of $(\log r)'(t)$. In fact, this formulation shows that, in this model, we could not separately infer the transmission constant $\beta$ and and the behavior effect $\alpha$ because the depletion of susceptibles is itself a reduction in $(\log r)'(t)$ proportional to $I(t)$, just as our proposed behavioral change was.

## Regression transmission model with EI compartments

Asher (2018) models a hypothetical West African Ebola outbreak using a regression transmission model with latent and infectious compartments:

```math
\begin{align*}
\log r(t) &= \log r(t-1) + \sigma Z(t) - \alpha I(t) \text{ for } t > 0 \\
Z(t) &\sim \mathcal{N}(0, 1) \\
E(t) &= E_+(t-1) - I_+(t-1) \\
I(t) &= I_+(t-1) - I_-(t-1) \\
E_+(t) &\sim \mathrm{Poisson}(r(t) I(t)) \text{ for } t > 0 \\
I_+(t) &\sim \mathrm{Binom}(E(t), 1/T_E) \\
I_-(t) &\sim \mathrm{Binom}(I(t), 1/T_I)
\end{align*}
```

where the parameters were given priors:

- $E(0)$, $I(0)$, $r(0)$: initial conditions
- $T_E$: mean duration of the latent period in units of the time step
- $T_I$: mean duration of the infectious period
- $\sigma$ and $\alpha$: regression coefficients
