---
title: 'Langevin diffusion'
date: 2026-02-06
permalink: /posts/2025/01/blog-post-18-1/
tags:
  - theory
  - ml
---

Recall that a stochastic process $X_t$ is called a diffusion process if it satisfies

$$
\begin{align*}
    dX_t = \mu(t, X_t)dt + \sigma(t, X_t)dW_t.
\end{align*}
$$

In other words, from the Markov property, the movement of the stochastic process only depends on the time $t$ and its current location. In particular, we study time-homogeneous processes, in which the functions $\mu$ and $\sigma$ do not depend on $t$. \cite{chewi25logconcave}.

**Definition**: Let $V: \mathbb R^d \to \mathbb R$ be a potential in $C^2$ and strongly convex function. The Langevin diffusion is the stochastic process taking values in $\mathbb R^d$ and satisfies

$$
    \begin{align*}
        dX_t = -\nabla V(X_t)dt + \sqrt{2}dW_t,
    \end{align*}
$$

where $B_t$ is the Brownian motion. 

Then, we already have that $X_0 \sim \rho_0$ is a random variable distributed according to $\rho_0$, then we calculate the infinitesimal generator of the Langevin Diffusion. Firstly, apply the Theorem \ref{Theorem:ito_formula}, we have the It\^o formula for the Langevin diffusion as:

$$
\begin{align*}
    f(X_t) - f(X_0) = \int_0^t -\langle \nabla f(X_s), \nabla V(X_s) \rangle + \mathrm{Tr}(\nabla^2 f(X_s))ds + \sqrt{2}\int_0^t \langle \nabla f(X_s), dW_s \rangle.
\end{align*}
$$


Since $W_t$ is the Brownian motion in $\mathbb R^d$, hence $dW_t$ is mean-zero. Moreover, it is also independent from $X_t$ and $\nabla f(X_t)$, then taking the expected value, we have

$$
\begin{align*}
    \mathbb E [\langle \nabla f(X_s), dW_s \rangle] = 0,
\end{align*}
$$


or

$$
\begin{align*}
    \mathbb E \left[ \sqrt{2}\int_0^t\langle \nabla f(X_s), dW_s \rangle \right] = 0.
\end{align*}
$$


Write down the remaining term as Taylor expansion, and take the expected value of both side, we also have

$$
\mathbb E [ f ( X_t ) | X_0 = x] - f(x) = t[-\langle \nabla f(x), \nabla V(x) \rangle + \mathrm{Tr}(\nabla^2 f(x))] + o(t)
$$

$$
\frac{P_t f(x) - f(x)}{t} = -\langle \nabla f(x), \nabla V(x) \rangle + \Delta f(x) + \frac{o(t)}{t},
$$

When $t \to 0$, we have

$$
\begin{align*}
    Lf(x) = \lim_{t\searrow 0} \frac{P_t f(x) - f(x)}{t} = -\langle \nabla f(x), \nabla V(x) \rangle + \Delta f(x).
\end{align*}
$$

Moreover, from the Theorem \ref{theorem: ito_chain_rule}, we also have

$$
\begin{align*}
    df(X_t) = Lf(X_t)dt + \sqrt{2}\nabla f(X_t) dW_t.
\end{align*}
$$

Take the expectation of both sides, we have

$$
\begin{align*}
    \frac{d}{dt}\mathbb E[f(X_t)] = \mathbb E[Lf(X_t)].
\end{align*}
$$

As $\rho_t$ has the law of $X_t$, then

$$
\begin{align*}
    \mathbb E[f(X_t)] = \int_{\mathbb R^d} f(x)\rho_t(x)dx.
\end{align*}
$$


Therefore,

$$
\begin{align*}
    \frac{d}{dt} \int_{\mathbb R^d} f(x)\rho_t(x)dx &= \int_{\mathbb R^d} Lf(x)\rho_t(x)dx \\
    &= \int_{\mathbb R^d} [\Delta f(x) -\langle \nabla f(x), \nabla V(x) \rangle ] \rho_t(x)dx.
\end{align*}
$$


From the divergence theorem, we imply that

$$
\begin{align*}
    \nabla f\cdot\nabla V\rho_t = \nabla f \cdot (\rho_t\nabla V) = f \nabla \cdot (\rho_t \nabla V),
\end{align*}
$$

and we rewrite as 

$$
\begin{align*}
    \frac{d}{dt}\int f\rho_t = \int f (\Delta \rho_t - \nabla \cdot (\rho_t \nabla V)).
\end{align*}
$$

Using the definition of weak derivative, we imply that

$$
\begin{align*}
    \partial_t \rho_t = \Delta \rho_t - \nabla \cdot (\rho_t \nabla V).
\end{align*}
$$