---
title: "Program verification: expressions in a simplified programming language"
description: "Lecture on representing expressions (& associated data types) in a simplified language for the purpose of reasoning about using propositional & predicate logic. Covers evaluating expressions in context of a state as well as rules for updating a state's bindings."
keywords:
  - "state"
  - "evaluation"
  - "expressions"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-28T10:00-06:00"
---

## agenda

- data types
- expressions
  - operations
  - arrays
  - conditional
- evaluating expressions
- updating state

## data types

one of two things:

1. primitive&mdash;ints, bools
2. composite&mdash;arrays (of 1+ dimensions) of primitive values w/ integer indices

## expressions

_**def**_&mdash;"a piece of code that can be evaluated to some value." values will always be of a primitive type.

### operators

expressions can be operated upon:

- on integers:
  - arithmetic: `+`, `-`, `*`, `/`, `%`, `sqrt()`, & `^`

    > [!NOTE]
    >
    > `/` & `sqrt()` round towards 0, e.g. `13/3 = 4`,
    > `13 / (-3) = (-4)`, & `sqrt(17) = 4`

  - relational: `=`, `!=`, `<`, `<=`, & `>=`

- on booleans: - $\neg$, $\land$, $\lor$, $\longrightarrow$, & $\longleftrightarrow$

- on arrays: `size()` & `a[INT]` where `a` is some array

### arrays

- `b[e]` is array element selection (0-indexed), where `b` is an array & `e` is an expression evaluating to an integer.
- `size(b)` gives the length of array `b`
- in multi-dimensional array, $b[e_0][e_1]...[e_{n-1}]$ selects element $e_0$ in first dimension, $e_1$ in second dim, ..., $e_{n-1}$ in nth dimension where $n$ is the number of dimensions

> [!NOTE]
>
> we can never have array appear by itself; instead always wrapped in some fn; why?

### conditionals

looks like $if B then e_1 else e_2 fi$ &mdash;can nest to add more branches,
like $if B_1 then e_1 else B_2 then e_2 else e_3 fi$, where $B_i$ & $B$
are boolean expressions & $e_i$ are expressions of either type (but all
must be same type) & type of $e_i$ determines type of the entire
conditional expression.

### some notes on expressions

when working w/ variables, we don't explicitly declare their type; instead we always infer from context. e.g. for $p \lor x > 0$ we can assignment like $x \coloneqq 5$ to start using $x$.

additionally, an expression must evaluate to some primitive value; thus
it cannot evaluate to an array. e.g. given $a$ & $b$ as
arrays, $if B then a else b fi$ is illegal,
but $if B then a[0] else b[0] fi$ is legal.

also, functions who return primitive types are allowed in an expression, but an expression cannot yield a function (i.e. functions aren't first class!). e.g. ...

finally, notation ...

> [!TODO]
>
> finish above notes

### language spec

> [!TODO]
>
> use above to complete below specification

```bnf
expression <e> ::= <c> | <v> | <f>
constant   <c> ::= INT | BOOL
variable   <v> ::= ID
function   <f> ::= ???
```

## evaluating expressions

since an expression represents a value, to evaluate an expression is to
"calculate what a piece of text equals to"; e.g. convert syntactic
meaning to semantic meaning.

evaluation is done in the context of a state, $\sigma$. given a proper
state, the expression can be evaluated to a value of the primitive type
it represents. for example, given state $\sigma = \{x = 5, y = 2 \}$ , then $\sigma(x * y) = 10$

value of $\sigma(e)$ depends on type of value $e$ represents. we recurse on the structure of $e$ to to find this:

- ...

> [!TODO]
>
> add examples here...

> [!ASIDE]
>
> when we evaluate an expression, how does something syntacitic actually become something semantic (e.g. how is it compiled from tokens to value)? some examples here can shed some light on this process:
>
> 1. let $z \equiv 2 + 3$ ; evaluating it in an arbitrary state $\sigma$ looks like:
>
> $$
> \begin{aligned}
> ...
> \end{aligned}
> $$
>
> 2. let $\sigma = \{x = 1\}$ & $\tau = \sigma \cup \{y = 1\}$ & $e \equiv (x = if y > 0 then 17 else y fi)$ ; evaluate $e$ in state of $\tau$:
>
> $$
> \begin{alignedat}{2}
> \tau(e) &=   \tau(x &= if y > 0 then 17 else y fi)       \\
>         &= (\tau(x) &= \tau(if y > 0 then 17 else y fi)) \\
>         &= (      1 &= \tau(if y > 0 then 17 else y fi)) \\
> \end{alignedat}
> $$

representing array states requires a little more work. given $\tau$ as

```no-linenums
...
```

how to represent it?

- ...some options

> [!ASIDE]
>
> ...
>
> let $\sigma = \{x = 1\}$ ; ...
>
> $$
> \begin{aligned}
> ...
> \end{aligned}
> $$

> [!TODO]
>
> finish examples!

## updating state

when workign with some state, $\sigma$, a variable, $x$, & a
value $\alpha$, we update $\sigma$ at $x$ with $\alpha$ (written
as $\sigma[x \mapsto \alpha]$ ) by copying $\sigma$ and binding $x$ in
it to $\alpha$ & saving this as a new state.

the state update notation is read left-to-right;
e.g. $\sigma[x \mapsto \alpha](v)$ means evaluate $v$ in the new state
created by updating $x$ in $\sigma$ to $\alpha$.

> [!ASIDE]
>
> ...
>
> let $\sigma = \{x = 1, y = 2\}$ & answer the following about state $\tau$:
>
> let $\tau = \sigma[x \mapsto 3]$, then $\tau = \{...\}
>
> $$
> \begin{aligned}
> ...
> \end{aligned}
> $$

> [!TODO]
>
> finish examples on updating state above!
