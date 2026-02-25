---
title: "Program verification: updating state & judging predicates"
description: "How state update operations are expressed."
keywords:
  - "updating state"
  - "program state"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-28T10:45-06:00"
  updated: "2026-01-30T10:00-06:00"
---

## agenda

- updating state
- properness & satisfaction of quantified predicates
- validity of predicates

<section>

## updating state

:::

when working with some state, $\sigma$, a variable, $x$, & a
value $\alpha$, we update $\sigma$ at $x$ with $\alpha$ (written
as $\sigma[x \mapsto \alpha]$ ) by copying $\sigma$ and binding $x$ in
it to $\alpha$ & saving this as a new state.

the state update notation is read left-to-right;
e.g. $\sigma[x \mapsto \alpha](v)$ means evaluate $v$ in the new state
created by updating $x$ in $\sigma$ to $\alpha$.

:::

> [!ASIDE]
>
> #### practice updating
>
> let $\sigma = \{x = 1, y = 2\}$ & answer the following about state $\tau$:
>
> <details>
>   <summary>
>
> **a.** let $\tau = \sigma[x \mapsto 3]$, then $\tau = \{...\}$
>
>   </summary>
>
> $$
> \begin{aligned}
> \tau = \{x = 3, y = 2\}
> \end{aligned}
> $$
>
> </details>
>
> <details>
>   <summary>
>
> **b.** let $\tau = \sigma[z \mapsto 3]$, then $\tau = \{...\}$
>
>   </summary>
>
> $$
> \begin{aligned}
> \tau = \{x = 1, y = 2, z = 3\}
> \end{aligned}
> $$
>
> </details>
>
> <details>
>   <summary>
>
> **c.** let $\tau = \sigma[x \mapsto 1]$, then ...
>
>   </summary>
>
> $$
> \begin{aligned}
> &\tau = \{x = 1, y = 2\} \\
> &\text{however} \\
> &\tau \not \equiv \sigma
> \end{aligned}
> $$
>
> </details>

:::

### sequencing updates

state update operations can be sequenced, like curried functions (or
methods that return self): $\sigma[x \mapsto 0][y \mapsto 8]$. as
above, these updates are read & applied from left to right&mdash;e.g.
if $\sigma = \{x = 2, y = 6\}$, the previous sequence of updates is
executed as follows:

$$
\begin{aligned}
  &\{x = 2, y = 6\}[x \mapsto 0][y \mapsto 8] \\
= &\{x = 0, y = 6\}[y \mapsto 8] \\
= &\{x = 0, y = 8\}
\end{aligned}
$$

:::

> [!ASIDE]
>
> #### practice sequencing
>
> True or False:
>
> <details>
>   <summary>
>
> **a.** let $x \not \equiv y$, then $\sigma[x \mapsto 0][y \mapsto 8] = \sigma[y \mapsto 8][x \mapsto 0]$
>
>   </summary>
>
> True, updating $x$ has no effect on $y$ & vice versa.
>
> </details>
>
> <details>
>   <summary>
>
> **b.** let $x \not \equiv y$, then $\sigma[x \mapsto 0][y \mapsto 8] \equiv \sigma[x \mapsto 0][y \mapsto 8]$
>
>   </summary>
>
> True. In this case the are syntactically equivalent because the
> updates are applied in the same order.
>
> </details>
>
> <details>
>   <summary>
>
> **c.** let $x \not \equiv y$, then $\sigma[x \mapsto 0][y \mapsto 8] \equiv \sigma[y \mapsto 8][x \mapsto 0]$
>
>   </summary>
>
> False. Recall updates applied in different orders that result in
> semantically equivalent sets; however they are not syntactically
> equivalent.
>
> </details>
>
> <details>
>   <summary>
>
> **d.** $\sigma[x \mapsto 0][x \mapsto 8] = \sigma[x \mapsto 8]$
>
>   </summary>
>
> True, the second update on the LHS gives a set that is semantically
> equivalent to the first update not happening at all.
>
> </details>
>
> <details>
>   <summary>
>
> **e.** $\sigma[x \mapsto 0][x \mapsto 8] \equiv \sigma[x \mapsto 8]$
>
>   </summary>
>
> False. While they "look the same" (are semantically equivalent), they
> are composed of different updates & thus are syntactically
> inequivalent.
>
> </details>
>
> and a more complicated one:
>
> </details>
>
> <details>
>   <summary>
>
> > let $\sigma = \{x = 1, z = 2\}$, find state $\sigma[x \mapsto 2][z \mapsto \sigma[z \mapsto 3](x + z) + 10]$:
>
>   </summary>
>
> $$
> \begin{aligned}
>   &\sigma[x \mapsto 2][z \mapsto \sigma[z \mapsto 3](x + z) + 10] \\
> = &\{x = 1, z = 2\}[x \mapsto 2][z \mapsto \sigma[z \mapsto 3](x + z) + 10] \\
> = &\{x = 2, z = 2\}[z \mapsto \{x = 1, z = 2\}[z \mapsto 3](x + z) + 10] \\
> = &\{x = 2, z = 2\}[z \mapsto \{x = 1, z = 3\}(x + z) + 10] \\
> = &\{x = 2, z = 2\}[z \mapsto ((1 + 3) + 10)] \\
> = &\{x = 2, z = 2\}[z \mapsto 14] \\
> = &\{x = 2, z = 14\} \space_\blacksquare
> \end{aligned}
> $$
>
> </details>

### updating arrays

to update the value $b[0]$, where $b$ is an array, it's helpful to remember that updating a state is updating a function.

> if $\delta$ is a function & $\alpha$ & $\beta$ are valid elements of
> the domain & range of $\delta$ respectively, then the update
> of $\delta$ at $\alpha$ with $\beta$, written
> as $\delta[\alpha \mapsto \beta]$, is the function defined
> by $\delta[\alpha \mapsto \beta](\gamma) = \beta$ if $\gamma = \alpha$
> & $\delta[\alpha \mapsto \beta](\gamma) = \delta(\gamma)$
> if $\gamma \neq \alpha$.

thus, this update of the array, $\delta$ works:

$$
\begin{aligned}
&\delta \coloneqq \{(4,6),(3,7),(2,5)\} \\
\\
&\delta[2 \mapsto 3] = \{(4,6),(3,7),(2,3)\} &&
    \htmlClass{hljs-comment}{\textit{// }} \\
\end{aligned}
$$

this works because $\delta(2)$ is updated from 5 to 3

</section>
<section>

## properness & satisfaction of quantified predicates

:::

a state is considered to be _**proper**_ for a given predicate if the state contains all _free_ variables to decide the value of the predicate.

> [!IMPORTANT]
>
> recall, a variable $v$ in some predicate is a _free occurrence_
> of $v$ if it is not within the scope of a quantifier over $v$
>
> that means, a variable $v$ is considered to be _**free**_ in
> predicate $p$ iff it has a free occurrence in $p$. conversely, $v$ is
> _**bound**_ in $p$ iff it has a bound occurrence in $p$.

an example to help clarify this:

<details>
<summary>

decide if each of the following variables is free or bound in $p$,
where

$$
\begin{aligned}
p \equiv x > z \land \exists x.\exists y.y \le f(x,y)
\end{aligned}
$$

</summary>

- $x$: free at term $x > z$ & bound in the quantifier $\exists x. \dots$ of $p$
- $y$: bound in the quantifier $\exists y. \dots$ of $p$
- $z$: free at the term $x > z$ in $p$
- $u$: neither free nor bound in $p$

</details>

:::

> [!ASIDE]
>
> #### practice on predicates
>
> True or False?
>
> <details>
>   <summary>
>
> **a.** $\{x = 1\}$ is proper for
> predicate $\forall y \in \Z.y > 1 \mapsto y > 0$
>
>   </summary>
>
> True, $y$ is bound in quantifier $\forall y \in \Z. \dots$.
>
> </details>
>
> <details>
>   <summary>
>
> **b.** $\{x = 1\}$ is proper for
> predicate $(\forall y \in \Z.y > 1 \mapsto y > 0) \land y > 5$
>
>   </summary>
>
> False. While $y$ is bound in quantifier $\forall y \in \Z. \dots$, it
> is free in the term $y > 5$ & $y \not \in \{x = 1\}$.
>
> </details>
>
> <details>
>   <summary>
>
> **c.** $(\forall y \in \Z.y > 1 \mapsto y > 0) \equiv (\forall x \in \Z.x > 1 \mapsto x > 0)$
>
>   </summary>
>
> True, the identifier of a bound variable has no semantic or syntactic
> meaning & thus doesn't effect equivalence.
>
> </details>

</section>
<section>

## validity of predicates

a proposition or predicate, $p$ is said to be _**valid**_ if is
satisfied by all proper states $\sigma$. this is denoted as $\models
p$.

> [!IMPORTANT]
>
> formally this is defined as
>
> $$
> \begin{aligned}
> &(\models p) \iff (\forall \sigma \in S.\sigma \models p), \;\text{where} \\
> &\quad\quad S \;\text{is the collection of all proper states for } p \\
> \end{aligned}
> $$

conversely, $\not \models p$ means that for at least one proper
state, $\sigma$, predicate/proposition $p$ is _**invalid**_;
e.g. "p is not always true".

also of note: if $p$ is a predicate about $x$ & $x$ is not a variable bound in $p$, then $(\models p) \iff (\models \forall x.p)$

</section>
