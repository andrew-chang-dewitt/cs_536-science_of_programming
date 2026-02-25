---
title: "Program verification: proving truth & quantified predicates"
description: "Discussion of how to prove truth in propostions; plus a review of predicate (as compared to proposition) logic, covering quantified predicates & predicate functions."
keywords:
  - "proofs"
  - "predicate logic"
  - "quantified predicates"
  - "predicate functions"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-21T10:00-06:00"
---

## agenda

- proving truth
- review of predicate logic
- quantified predicates
- predicate functions

## proving truth

a formal proof of truth, i.e. that two propositions are provably logically equivalent if each follows from the other.

an example: show that $(p \longrightarrow q) \land p \longrightarrow q \iff T$

$$
\begin{aligned}
(p \longrightarrow q) \land p \longrightarrow q
  &\iff ((p \longrightarrow q) \land p) \longrightarrow q
&& \textit{parenthization} \\
  &\iff ((\neg p \lor q) \land p) \longrightarrow q
&& \textit{definition of implication} \\
  &\iff ((\neg p \land p) \lor (q \land p)) \longrightarrow q
&& \textit{distributivity of $\land$} \\
  &\iff (F \lor (q \land p)) \longrightarrow q
&& \textit{contradiction} \\
  &\iff (q \land p) \longrightarrow q
&& \textit{identity} \\
  &\iff (\neg (q \land p)) \lor q
&& \textit{definition of implication} \\
  &\iff (\neg q \lor \neg p) \lor q
&& \textit{DeMorgan's law} \\
  &\iff \neg q \lor q \lor \neg p
&& \textit{Commutativity \& Associativity of $\lor$} \\
  &\iff T \lor \neg p
&& \textit{excluded middle} \\
   &\iff T \space_\blacksquare
&& \textit{domination} \\
\end{aligned}
$$

while the above proof worked to make the rhs match the lhs, it could
have just as easily been the other way, or even worked both sides
until they had matching expressions.

we can also prove logical implication, in a similar fashion. useful when we don't need full equivalence; however, has more restrictions. can only work rhs to make it match lhs; can't touch the lhs at all.

an example: show that $(p \lor q) \land (p \longrightarrow r) \land (q \longrightarrow r) \implies r$ w/out using or-elimination immediately

$$
\begin{aligned}
(p \lor &q) \land (p \longrightarrow r) \land (q \longrightarrow r) \\
        &\iff (p \lor q) \land ((p \longrightarrow r) \land (q \longrightarrow r))
          && \textit{associativity of $\land$} \\
        &\iff (p \land ((p \longrightarrow r) \land (q \longrightarrow r))) \\
        &\qquad\qquad \lor (q \land ((p \longrightarrow r) \land (q \longrightarrow r)))
          && \textit{distributivity of $\land$} \\
        &\iff ((p \longrightarrow r) \land p \land (q \longrightarrow r)) \\
        &\qquad\qquad \lor ((q \longrightarrow r) \land q \land (p \longrightarrow r))
          && \textit{associativity of $\land$} \\
        &\implies (r \land (q \longrightarrow r)) \lor (r \land (p \longrightarrow r))
          && \textit{modus ponens} \\
        &\implies r \lor r
          && \textit{and-elimination} \\
        &\iff r \space_\blacksquare
          && \textit{idempotency} \\
\end{aligned}
$$

## review of predicate logic

_**def: predicate**_&mdash;a logical assertion (T or F) that describes
some property of values, e.g. $8 < 2.45$. used to assert truths about
values from some _**domain**_(s), a collection of values (e.g. real
numbers), typ. expressed blackboard notation, like $\mathbb{N}$. \*\*in

:::

predicate logic introduces arithmetic operators & comparison operators that are as we already know them from previous math courses. hierarchy of operators is:

1. arithmetic
2. comparison
3. logical

:::

> [!ASIDE]
>
> **practice**&mdash;True or False:
>
> 1. <details>
>      <summary>
>
>    $8 > 2 + 3 \land 8 \le 10$
>      </summary>
>
>    $$
>    \begin{aligned}
>    8 > 2 + 3 \land 8 \le 10 &\iff (8 > (2 + 3)) \land (8 \le 10) \\
>                             &\iff (8 > 5) \land (8 \le 10) \\
>                             &\iff T \land T \\
>                             &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
>    </details>
>
> 2. <details>
>      <summary>
>
>    $0 > 1 \longrightarrow 4 > 3$
>
>      </summary>
>
>    $$
>    \begin{aligned}
>    0 > 1 \longrightarrow 4 > 3 &\iff 0 > 1 \longrightarrow 4 > 3 \\
>                                &\iff (0 > 1) \longrightarrow (4 > 3) \\
>                                &\iff F \longrightarrow T \\
>                                &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
>    </details>
>
> 3. <details>
>      <summary>
>
>    $x = 1 \lor x = -1 \longrightarrow x^2 = 1$
>
>      </summary>
>
>    $$
>    \begin{aligned}
>    x = 1 \lor x = -1 \longrightarrow x^2 = 1
>        &\iff ((x = 1) \lor (x = -1)) \longrightarrow (x^2 = 1) \\
>        &\iff ((1)^2 = 1) \lor ((-1)^2 = 1)  \\
>        &\iff (1 = 1) \lor (1 = 1)  \\
>        &\iff T \lor T  \\
>        &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
>    </details>

A state is well-formed & proper for a predicate based on the same concepts as in propositional logic, the only difference being the type of variables bound. In addition to booleans, we can now bind values from our predicate's domain.
A state $\sigma$ **satisfies** a predicate $p$ if $\sigma(p) = T$,
[!ASIDE]

> **practice**&mdash;True or False:
>
> 1. <details>
>      <summary>
>
>    $\{x = y, y = 0\}$ is a well-formed state
>      </summary>
>
>    False
>
>    </details>
>
> 2. <details>
>      <summary>
>
>    $\{x = 5, x = 6, y = 2\}$ is a well-formed state
>
>      </summary>
>
>    False
>
>    </details>
>
> 3. <details>
>      <summary>
>
>    State $\sigma = \{x = 8, y = 2\}$ is proper for $x + y + z > 0$
>
>      </summary>
>
>    False
>
>    </details>
>
> 4. <details>
>      <summary>
>
>    State $\sigma = \{x = 8, y = 0\}$ is proper for $\frac{x}{y} > 0$
>
>      </summary>
>
>    True, but will give runtime error of Divide By Zero
>
>    </details>
>
> 5. <details>
>      <summary>
>
>    State $\sigma = \{b = 2\}$ is proper for $b[0] = 2$
>
>      </summary>
>
>    False, because in the predicate, $b$ is an array, but in $\sigma$ it is an integer
>
>    </details>

A state $\sigma$ **satisfies** a predicate $p$ if $\sigma(p) = T$,
which is denoted as $\sigma \models p$. Additionally,
given $\sigma(p) = F$, then $\sigma \not \models p$. We can
only discuss satisfaction when a state is proper for a predicate.

> [!ASIDE]
>
> **practice**&mdash;True or False:
>
> 1. <details>
>      <summary>
>
>    $\{x = 1, y = 3\} \models x + y \ge 4$
>
>      </summary>
>
>    $$
>    \begin{aligned}
>    \{x = 1, y = 3\} \models x + y \ge 4 &\iff 1 + 3 \ge 4 \\
>                                         &\iff 4 \ge 4 \\
>                                         &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
> 2. <details>
>      <summary>
>
>    $\{b = (3,5,9), x = 2\} \models b[x] = 9$
>
>      </summary>
>
>    $$
>    \begin{aligned}
>    \{b = (3,5,9), x = 2\} \models b[x] = 9
>        &\iff b[2] = 9 \\
>        &\iff 9 = 9 \\
>        &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
> 3. <details>
>      <summary>
>
>    $\{x = 1, y = 2\} \not \models (x^2 + 2 * y) % 5 = 1$
>
>      </summary>
>
>    $$
>    \begin{aligned}
>    \{x = 1, y = 2\} \not \models (x^2 + 2 * y) \% 5 = 1
>        &\iff \neg ((1^2 + 2 * 2) \% 5 = 1) \\
>        &\iff \neg ((1 + 4) \% 5 = 1) \\
>        &\iff \neg (5 \% 5 = 1) \\
>        &\iff \neg (0 = 1) \\
>        &\iff \neg F \\
>        &\iff T \space_\blacksquare
>    \end{aligned}
>    $$
>
>    </details>

## quantified predicates

a quantifier is a means of specifying a value (or values) for a
variable in a predicate; e.g. given predicate $x^2 \ge x$, a quantifier
for $x$ is $x \in \real$.

:::

some types of quantifiers:

- **universal quantifier**

  has form $\forall x \in S$, where $S$ is a set of values.

  can be used to create a **universally quantified predicate** (aka
  **universal**) w/ form $\forall x \in S.p$, where $S$ is a set & $p$
  is a predicate involving $x$.

  an example: $\forall x \in \mathbb{Z}.x > 1 \longrightarrow x < x^2$
  means "for all integer $x$, if it is greater than 1, then it is
  smaller than its square"

- **existential quantifier**

  has form $\exist x \in S$, w/ predicate form $\exist x \in S.p$

  ex: $\exist x \in \mathbb{Z}.x \not = 0 \land x = x^2$ means "here
  exists integer $x$ s.t. it is not equal to 0 and it is equal to its
  square"

- **bounded quantifier**

  used to shorten a quantifier w/ a condition in the body by moving the
  condition to the quantifier.
  i.e. $\forall p.q$ means $\forall x.p \longrightarrow q$
  where $x$ appears in $p$ & $x$ is understood to be
  the variable we are quantifying over. similarly, $\exist p.q$
  means $\exist x.p \land q$
  where $x$ appears in $p$ & $x$ is understood to
  be the variable we are quantifying over.

:::

> [!NOTE]
>
> we typically omit the set if it is understood by context, e.g. when
> we can know that $x \in \mathbb{Z}$, then we can just
> write $\forall x.x > 1 \longrightarrow x < x^2$

:::

predicate logic also has proof of truth, like we did for propositional
logic above. all the same rules at the end of the [last
lecture](./0116-more_prop_logic/) still apply, w/ the following change
to **DeMorgan's Law**:

$$
\begin{align}
(\neg \forall x.p) &\iff (\exist  x.\neg p) \\
(\neg \exist  x.p) &\iff (\forall x.\neg p)
\end{align}
$$

:::

> [!ASIDE]
>
> **practice**&mdash;show full parenthization of quantified predicates:
>
> 1. <details>
>      <summary>
>
>    $\forall x \in \mathbb{Z}.x > 1 \longrightarrow x < x^2$ is syntactically equivalent to...
>
>      </summary>
>
>    $(\forall x \in \mathbb{Z}.((x > 1) \longrightarrow (x < x^2)))$
>
>    </details>
>
> 2. <details>
>      <summary>
>
>    $\forall x \in \mathbb{Z}.\exist y \in \mathbb{Z}.y \le x^2$ is syntactically equivalent to...
>
>      </summary>
>
>    $\forall x \in \mathbb{Z}.\exist y \in \mathbb{Z}.y \le x^2$
>
>    </details>
>
> 3. <details>
>      <summary>
>
>    $???$ is syntactically equivalent to...
>
>      </summary>
>
>    $???$
>
>    </details>

## predicate functions

remembering/writing predicates repeatedly can get tedious & become
error prone. to alleviate that, we can give names to predicates by
writing them into a _**predicate function**_ mapping a set of variables
to a Boolean value.

some examples:

- define a function $isSorted(b,m,n)$ so that it returns $True$ if &
  only if subarray $b$ between indices $m$ to $n$ (inclusive) is
  sorted. assume $m$ & $n$ are valid for $b$ & that $n > m$.

  $$
  \begin{aligned}
  \text{isSorted}(b,m,n) \equiv \forall i.m \le i < n - 1 \implies b[i] \le b[i+1]
  \end{aligned}
  $$

- define a function $isZero(b,n)$ so that it returns $True$ if &
  only if the first $n$ numbers in array $b$ are all 0. assume $n$ is no larger than the length of $b$.

  $$
  \begin{aligned}
  \text{isZero}(b,n) \equiv \forall i.0 \le i < n \longrightarrow b[i] = 0
  \end{aligned}
  $$
