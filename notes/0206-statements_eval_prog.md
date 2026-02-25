---
title: "Program verification: denotational semantics"
description: "Operational semantics can be very verbose. An alternative logical notation can be denotional semantics, which focuses on end states for a given program. Here we introduce the notation & work through some examples."
keywords:
  - "denotational semantics"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-06T10:00-06:00"
---

## agenda

- denotional semantics

## denotional semantics

specifying every step of a program as an evaluation of one configuration to the
next, as we did in [last lecture on operational
semantics](../0204-statements_simplified_lang/), can get tedious. some tedium
can be alleviated by skipping steps using $\rarr^n$ (where $n$ is some number
of steps to skip) or $\rarr^*$.

e.g. the last practice problem in that lecture, where:

$$
\begin{aligned}
  S &\equiv s \coloneqq 0; k \coloneqq 0; W \\
  W &\equiv \text{while}\; k < n \;\text{do}\ S_1 \;\text{od} \\
S_1 &\equiv s \coloneqq s + k + 1; k\coloneqq k + 1 \\
\end{aligned}
$$

evaluation of $S$ in $\sigma$ where $\sigma(n) = 3$ can be simplified to:

$$
\begin{aligned}
\lang S, \sigma \rang &\rarr^0 \lang s \coloneqq 0; k \coloneqq 0; W, \sigma \rang \\
                      &\rarr^2 \lang W, \sigma[s \mapsto 0][k \mapsto 0] \rang \\
                      &\rarr^* \lang W, \sigma[s \mapsto 1][k \mapsto 1] \rang &&
                          \htmlClass{hljs-comment}{\textit{// after each iteration of $W$}} \\
                      &\rarr^* \lang W, \sigma[s \mapsto 3][k \mapsto 2] \rang \\
                      &\rarr^* \lang W, \sigma[s \mapsto 6][k \mapsto 3] \rang \\
                      &\rarr   \lang E, \sigma[s \mapsto 0][k \mapsto 0] \rang \\
\end{aligned}
$$

this can be expressed another way, in terms of _**denotational semantics**_. that is, for any configuration of $S$ & $\sigma$ that eventually evaluates to $\lang E, \tau \rang$ (e.g. program $S$ in state $\sigma$ terminates in $\tau$ ), then "we say $\tau$ is the _denotational semantics_ of $S$ in $\sigma$". this is written as

$$
\begin{aligned}
M(S,\sigma) = \{\tau\}
\end{aligned}
$$

### simplified lang denotational semantics rules

:::

- _**no-op**_:

  $$
  \begin{aligned}
  M(\text{skip},\sigma) = \{\sigma\}
  \end{aligned}
  $$

- _**assignment**_:

  $$
  \begin{aligned}
  &M(v \coloneqq e,\sigma) = \{\sigma[v \mapsto \sigma(e)]\} \\
  &M(b[e_1] \coloneqq e,\sigma) = \{\sigma[b[\sigma(e_1)] \mapsto \sigma(e)]\}
  \end{aligned}
  $$

- _**conditional**_:

  $$
  \begin{aligned}
  &M(\text{if}\; e \;\text{then}\; s_1 \;\text{else}\; s_2 \;\text{fi},\sigma)
      = \begin{cases}
            M(s_1, \sigma), &\sigma(e) = T \\
            M(s_2, \sigma), &\text{otherwise}
        \end{cases} \\
  \\
  &\textit{or if the else is elided} \\
  \\
  &M(\text{if}\; e \;\text{then}\; s_1 \;\text{fi},\sigma)
      = \begin{cases}
            M(s_1, \sigma), &\sigma(e) = T \\
            M(\text{skip}, \sigma), &\text{otherwise}
        \end{cases} \\
  \end{aligned}
  $$

- _**iterative**_:

  $$
  \begin{aligned}
  &M(W,\sigma)
      = \begin{cases}
            M(s; W, \sigma) = M(W, M(s, \sigma)) \rang, &\sigma(e) = T \\
            \{\sigma\}, &\text{otherwise}
        \end{cases}, \;\text{where} \\
  &\quad\quad W \equiv \text{while}\; e \;\text{do}\; s \;\text{od} \\
  \end{aligned}
  $$

- _**sequence**_:
  this one becomes much simpler in denotation semantics; represented as just a
  recursive evalution

  $$
  \begin{aligned}
  M(s_1;s_2,\sigma) = M(s_2,M(s_1,\sigma))
  \end{aligned}
  $$

:::

> [!ASIDE]
>
> an example problem
>
> <details>
>   <summary>
>
> for
>
> $$
> \begin{aligned}
> IF &\equiv \;\text{if}\; n < 0 \;\text{then}\; y \coloneqq 0 \;\text{else}\; x \coloneqq 0; y \coloneqq 1; W \;\text{fi} \\
>  W &\equiv \;\text{while}\; x < n \;\text{do}\; x \coloneqq x + 1; y \coloneqq y + y \;\text{od}
> \end{aligned}
> $$
>
> find $M(\text{IF}, \sigma)$, where $\sigma = \{n = 1\}$:
>
>   </summary>
>
> $$
> \begin{aligned}
> M(\text{IF}, \sigma) &= M(y \coloneqq 1; W, \{n = 1, x = 0\}) \\
>                      &= M(W, \{n = 1, x = 0, y = 1\}) \\
>                      &= M(W, M(x \coloneqq x + 1; y \coloneqq y + y, \{n = 1, x = 0, y = 1\})) \\
>                      &= M(W, \{n = 1, x = 1, y = 2\}) \\
>                      &= \{ \{n = 1, x = 1, y = 2\} \} \space_\blacksquare \\
> \end{aligned}
> $$
>
> </details>
