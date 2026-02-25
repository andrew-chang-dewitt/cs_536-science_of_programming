---
title: "Program verification: more propositional logic & state"
description: "Day 2 continues the review of propositional logic then begins discussions of state (as well as semantic & syntactic equality)."
keywords:
  - "program verification"
  - "propositional logic"
  - "lecture notes"
  - "computer science"
  - "cs 536"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-16T10:00-06:00"
  updated: "2026-01-21T09:00-06:00"
---

## agenda

- propositional logic
  - operator precedence
  - operator associativity
  - truth tables
- semantic equality & syntactic equality
- state

## prop logic, cont.

### operator precedence

:::

logical operators have a precedence that determines how to combine terms. in order from highest to lowest:

- not ( $\neg$ )
- and ( $\land$ )
- or ( $\lor$ )
- implication ( $\longrightarrow$ )
- biconditional ( $\longleftrightarrow$ )

:::

> [!ASIDE]
>
> let's practice&mdash;remove the redundant parenthesis:
>
> 1. <details>
>      <summary>
>
>    $(p \longrightarrow ((\neg q) \land r))$
>
>      </summary>
>
>    $p \longrightarrow \neg q \land r$
>
>    </details>
>
> 2. <details>
>      <summary>
>
>    $((p \lor q) \land r) \longrightarrow (\neg (s \lor p))$
>
>      </summary>
>
>    $(p \lor q) \land r \longrightarrow \neg (s \lor p)$
>
>    </details>

### operator associativity

:::

- $\land$ & $\lor$ are fully associative, meaning $p \land q$ is equivalent to $q \land p$
  - formally, they are considered **left** associative, meaning $p \lor q \lor r$ is equivalent to $(p \lor q) \lor r$
- $\longrightarrow$ is left associative, meaning $p \longrightarrow q \longrightarrow r$ is equivalent to $p \longrightarrow (q \longrightarrow r)$

:::

> [!ASIDE]
>
> <details>
>   <summary>
>
> let's practice: what is the truth value of $T \longleftrightarrow F \longleftrightarrow F$ ?
>
>   </summary>
>
> it means $T \longleftrightarrow (F \longleftrightarrow F)$, which is semantically equivalent to $T \longleftrightarrow T$, which evaluates to $T$.
>
> </details>

### truth tables

:::

used to capture truth values of a _compound proposition_.

an example showing the values of $\land$, $\lor$, $\longrightarrow$, & $\longleftrightarrow$:

| $p$ | $q$ | $p \land q$ | $p \lor q$ | $p \longrightarrow q$ | $p \longleftrightarrow q$ |
| --- | --- | ----------- | ---------- | --------------------- | ------------------------- |
| F   | F   | F           | F          | T                     | T                         |
| F   | T   | F           | T          | T                     | F                         |
| T   | F   | F           | T          | F                     | F                         |
| T   | T   | T           | T          | T                     | T                         |

an example showing the values of $\neg$:

| $p$ | $\neq p$ |
| --- | -------- |
| F   | T        |
| T   | F        |

:::

> [!ASIDE]
>
> <details>
>   <summary>
>
> let's practice&mdash;create a truth table
> for $\neg p \lor q$ & $p \longrightarrow q$
>
>   </summary>
>
> | $p$ | $q$ | $\neg p$ | $\neg p \lor q$ | $p \longrightarrow q$ |
> | --- | --- | -------- | --------------- | --------------------- |
> | F   | F   | T        | T               | T                     |
> | F   | T   | T        | T               | T                     |
> | T   | F   | F        | F               | F                     |
> | T   | T   | F        | T               | T                     |
>
> as we can see here, $\neg p \lor q$ is equivalent to $p \longrightarrow q$
>
> </details>

:[semantic & syntactic equality]h2{style="padding-top: 1rem"}

let's start w/ two questions that might seem very similar:

> true or false?
>
> 1. $2 + 2 = 4$
> 2. $2 + 2 \equiv 4$

this question is really asking the difference between _**semantic quality**_ &
_**syntactic equality**_.

for two expressions to be _syntactically_ equal, they must be textually
identical. in this class, we'll use $\equiv$ to denote _syntactic_
equality. meanwhile, for two expressions to be _semantically_ equal, they must
be logically equivalent. in this class we'll use $\iff$ (instead of $=$ ) to
denote semantic equality.

we can use syntactic equality to imply semantic equality&mdash;given
two textually identical expressions, we can know that they will
evaluate to the same result. however; just because two statments are
logically equivalent does **not** mean they are textually
identical&mdash;meaning that semantic equality does **not** imply
syntactic equality.

we can express this _logical implication_ (vs. a propositional
implication) using $\implies$, similar to using $\iff$ for _logical
equivalence_. thus, we can say $p \longleftrightarrow q \iff T$ tells
us that $p$ logically implies $q$, or $p \implies q$.

## state

:::

_**def: state**_&mdash;is a collection of variables with their current
values, typically expressed as a set of _bindings_: $\{p, q, r, ...\}$.
usually, $\sigma$ is used to represent a state.

since each variable is mapped 1:1 to a value, we can consider state to be a
function:

$$
\begin{aligned}
\because   && \sigma &= { x = 5, p = T } \\
\therefore && \sigma(x) &= 5 \land \sigma(p) = T \space_\blacksquare \\
\end{aligned}
$$

a state is _**ill-formed**_ if:

- variables are not mapped 1:1 to values
- or multiple variables (e.g. an expression such as $p \land q$ or $p \lor \neg p$ ) are used in a single binding

from all this, we can say that a proposition $p$ is satisfied by a
state $\sigma$ if $p$ evaluates to $True$ in $\sigma$, denoted
as $\sigma \models p$. for our purposes in the beginning of this class,
we can also say that $\sigma \not \models p$ tells us
that $\sigma(p) = False$.

:::

> [!ASIDE]
>
> let's practice&mdash;determine if each of the following is true or false:
>
> 1. <details>
>      <summary>
>
>    $\{p = F\} \models \neg p$
>
>      </summary>
>
>    True, because
>
>    $$
>    \begin{aligned}
>    \sigma &\coloneqq \{p = F\} \\
>    \end{aligned}
>    \\
>    \begin{aligned}
>    \sigma \models \neg p &\iff \neg \sigma(p) \\
>                          &\iff \neg F \\
>                          &\iff T \space_\blacksquare \\
>    \end{aligned}
>    $$
>
>    </details>
>
> 2. <details>
>      <summary>
>
>    $\{p = T, q = T, r = F\} \not \models p \land \neg q$
>
>      </summary>
>
>    True because
>
>    $$
>    \begin{aligned}
>    \sigma &\coloneqq \{p = T, q = T, r = F\} \\
>    \end{aligned}
>    \\
>    \begin{aligned}
>    \sigma \not \models p \land \neq q &\iff \neg (\sigma(p) \land \neg \sigma(q)) \\
>                                       &\iff \neg (T \land \neg T) \\
>                                       &\iff \neg (T \land F) \\
>                                       &\iff \neg F \\
>                                       &\iff T \space_\blacksquare \\
>    \end{aligned}
>    $$
>
>    </details>
>
> 3. <details>
>      <summary>
>
>    $\empty \models T \land (F \longrightarrow T)$
>
>      </summary>
>
>    True, because
>
>    $$
>    \begin{aligned}
>    \empty \models T \land (F \longrightarrow T) &\iff T \land (F \longrightarrow T) \\
>                                                 &\iff T \land (\neg F \lor T) \\
>                                                 &\iff T \land T \\
>                                                 &\iff T \space_\blacksquare \\
>    \end{aligned}
>    $$
>
>    </details>
>
> 4. <details>
>      <summary>
>
>    If $\sigma \models \neg p$, then $\sigma \not \models p$
>
>      </summary>
>
>    True, because
>
>    $$
>    \begin{aligned}
>    \sigma \models \neg p &\iff \sigma \not \models p \\
>           \neg \sigma(p) &\iff \neg (\sigma(p)) \space_\blacksquare \\
>    \end{aligned}
>    $$
>
>    </details>
>
> 5. <details>
>      <summary>
>
>    Let $\sigma$ & $\tau$ be two states, if $\sigma \models p$ and $\sigma \subset \tau$, then $\tau \models p$
>
>      </summary>
>
>    True, because
>
>    $$
>    \begin{align}
>           \sigma &\subset \tau \tag{a} \\
>           \sigma &\models p \tag{b} \\
>    \notag \\
>              (a) &\implies x \in \tau \forall x \in \sigma \tag{c} \\
>              (b) &\implies p \in \sigma \tag{d} \\
>    (c) \land (d) &\implies p \in \tau \space_\blacksquare \notag
>    \end{align}
>    $$
>
>    </details>
>
> 6. <details>
>      <summary>
>
>    $\{p = T\} \models p \land q$
>
>      </summary>
>        ???
>    </details>

## some prop logic rules

- **law of contrapositive**

  $$
  \begin{align}
  p \longrightarrow q \iff \neg q \longrightarrow p
  \end{align}
  $$

- **definition of implication**

  $$
  \begin{align}
  p \longrightarrow q \iff \neg p \lor q
  \end{align}
  $$

- **negation of implication**

  $$
  \begin{align}
  \neg (p \longrightarrow q) \iff p \lor q
  \end{align}
  $$

- **definition of biconditional**

  $$
  \begin{align}
  (p \longleftrightarrow q) \iff (p \longrightarrow q) \land (q \longrightarrow p)
  \end{align}
  $$

- **commutativity**

  $$
  \begin{align}
  p \lor  q &\iff q \lor  p \\
  p \land q &\iff q \land q
  \end{align}
  $$

- **associativity**

  $$
  \begin{align}
  (p \lor q) \lor r &\iff p \lor (q \lor r) \\
  (p \land q) \land r &\iff p \land (q \land r)
  \end{align}
  $$

- **distributivity**

  $$
  \begin{align}
  (p \lor q) \land r &\iff (p \land r) \lor (q \land r) \\
  (p \land q) \lor r &\iff (p \lor r) \land (q \lor r)
  \end{align}
  $$

- **identity**

  $$
  \begin{align}
  p \land T &\iff p \\
  p \lor  F &\iff p
  \end{align}
  $$

- **idempotency**

  $$
  \begin{align}
  p \lor  p &\iff p \\
  p \land p &\iff p
  \end{align}
  $$

- **domination**

  $$
  \begin{align}
  p \lor  T &\iff T \\
  p \land F &\iff F \\
  \end{align}
  $$

- **absurdity**

  $$
  \begin{align}
  (F \longrightarrow p) \iff T
  \end{align}
  $$

- **contradiction**

  $$
  \begin{align}
  p \land \neg p \iff F
  \end{align}
  $$

- **excluded middle**

  $$
  \begin{align}
  p \lor \neg p \iff T
  \end{align}
  $$

- **double negation**

  $$
  \begin{align}
  \neg \neg p \iff p
  \end{align}
  $$

- **DeMorgan's laws**

  $$
  \begin{align}
  \neg (p \land q) &\iff (\neg p \lor  \neg q) \\
  \neg (p \lor  q) &\iff (\neg p \land \neg q)
  \end{align}
  $$

- **transitivity**

  $$
  \begin{align}
  (p \longrightarrow q) \land (q \longrightarrow r) &\implies (p \longrightarrow r) \\
  (p \longleftrightarrow q) \land (q \longleftrightarrow r) &\implies (p \longleftrightarrow r)
  \end{align}
  $$

- **Modus Ponens**

  $$
  \begin{align}
  (p \longrightarrow q) \land p \implies q
  \end{align}
  $$

- **Modus Tollens**

  $$
  \begin{align}
  (p \longrightarrow q) \land \neg q \implies \neg p
  \end{align}
  $$

- **or-introduction (and-elimination)**

  $$
  \begin{align}
  & \textit{"I had dinner" logically implies "I had dinner or lunch"} \nonumber \\
  &\qquad p         \implies p \lor q \\
  & \textit{"I had dinner \& lunch" logically implies "I had dinner"} \nonumber \\
  &\qquad p \land q \implies p
  \end{align}
  $$

- **or-elimination**

  $$
  \begin{align}
  (p \lor q) \land (p \longrightarrow r) \land (q \longrightarrow r) \implies r
  \end{align}
  $$
