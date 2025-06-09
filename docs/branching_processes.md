# Branching processes

## Notation and basic definitions

### Space of all possible descendants

Every individual is the child of some parent. Every individual can be uniquely specified by the vector $(j_1, \ldots, j_n)$, meaning the $j_n$-th child of the $j_{n-1}$-th child of the ... $j_1$-th child of the ancestor. Note that these are vectors of natural numbers, i.e., $\mathbb{N}^n$.

The set of all possible members of the $n$-th generation of _descendants_ of an ancestor is denoted:

```math
\begin{align*}
I(0) &\equiv \{ 0 \} \\
I(n) &\equiv \{x | x \in \mathbb{N}^n\} \text{ for } n \geq 1
\end{align*}
```

where by convention the ancestor is denoted with $0$ and the zeroth generation is the ancestor.

The set of all possible descendants of an ancestor is denoted:

$$
I \equiv \bigcup_{n=0}^\infty I(n)
$$

The set of possible descendants of some descendent $x$ of an ancestor is denoted:

$$
I_x \equiv \{x\} \cup \bigcup_{n=1}^\infty \{(x,y) | y \in \mathbb{N}^n\}
$$

where $(x,y)$ denotes the concatenation of $x$ and $y$.

The _predecessors_ of an individual $x = (j_1, \ldots, j_{n-1}, j_n)$ are its parent $(j_1, \ldots, j_{n-1})$, and so forth through $j_1$ in the first generation, including the ancestor.

### Multi-type processes

If there are multiple _types_ of individuals, then we specify individuals with the vector:

$$
(\tau_0; j_1, \tau_1; \ldots; j_n, \tau_n)
$$

Reading this vector from left to right:

- The ancestor was of type $\tau_0$.
- Of the ancestor's children, consider those of type $\tau_1$. Consider the $j_1$-th child of that type.
- Iterate to the $n$-th generation.

Note that this space of all possible descendants is still countable.

In general, we will assume single-type processes.

### Numbers of children and realization

The _number of children_ of an individual $x$ is a random variable be denoted $\xi_x$. By definition, a _branching process_ has the $\xi_x$ i.i.d. for all $x$.

An individual is _realized_ (in contrast to merely _possible_) if its parent is realized. If the ancestor is realized, then a possible first-generation individual $j$ is realized if $\xi_0 \geq j$. More generally, $(j_1, \ldots, j_n, j_{n+1})$ is realized if (1) its parent $x = (j_1, \ldots, j_n)$ is and (2) $\xi_x \geq j_{n+1}$.

The number $z_n$ of realized individuals in each generation is also a random variable, and $\{z_n | n \in 0, 1, \ldots\}$ is a _Galton-Watson process_.

### Birth times and life lengths

Associate each individual $x$ with two further random variables: the birth time $\sigma_x$ and the life length $\lambda_x$. An individual $x$ is _alive_ at time $t$ if $\sigma_x \leq t < \sigma_x + \lambda_x$. We will study the random variables $z_t$, the number of individuals who are alive at time $t$ and also realized.

If we assume that $\lambda_x$ is always 1 and that births happen at the end of the parent's life, then we recover the Galton-Watson or "splitting" process.

If we assume that the $(\xi_x, \lambda_x)$ are i.i.d., then we have a _Bellman-Harris process_ (or, confusingly, an "age-dependent process"). In this case, we write drop the subscript and write simple $\xi$ and $\lambda$. Note that this is a strong assumption, because, for example, longer-lived individuals are not more likely to produce more children.

### Reproduction by age

We will also study $z_t^a$, the number of individuals who are alive at time $t$, younger than $a$ at time $t$, and realized. This requires defining the random variables $\xi_x(a_1, a_2)$, the number of births to individual $x$ between their ages $a_1$ and $a_2$. We will usually consider $\xi(t) \equiv \xi_0(0, a)$ because the $\xi_x(a_1, a_2)$ are distributed identically for all $x$, including the ancestor, for whom $a = t$.

## Survey of results

Assume a Bellman-Harris process (i.e., i.i.d. $\xi$ and $\lambda$) and that no children are born after the death of their parent, i.e., that $\mathbb{P}[\xi_x(\lambda_x, \infty) = 0] = 1$.

### Extinction and final size

Define the _reproduction function_ $\mu(t) \equiv \mathbb{E}[\xi(t)]$.

**Theorem (6.2.2)**. If $\mu(0) < 1$ and $\mu(t)$ is finite for some $t > 0$, then $\mathbb{P}[z_t \text{ is finite for all } t \geq 0] = 1$. (An extension to the theorem shows that this also holds for the $\mu(0) = 1$ case.)

Define the _reproduction generation function_ $f(s) \equiv \mathbb{E}[s^{\xi(\infty)}]$ for $0 \leq s \leq 1$. Define the _extinction probability_ $q = \mathbb{P}[z_t \to 0]$.

**Theorem (6.5.1)**. The extinction probability is the smallest non-negative root of the equation $f(s) = s$. If $\mathbb{P}[\xi(\infty)=1] < 1$, then $q = 1 \iff \mu(\infty) \leq 1$.

## Equivalence with ODEs
