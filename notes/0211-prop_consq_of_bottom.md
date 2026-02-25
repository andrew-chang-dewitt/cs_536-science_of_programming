---
title: "Program verification: bottom $\\bot$"
description: "Not all programs terminate in a valid state, or terminate at all. In pl theory, this idea is called 'bottom', $\\bot$. Here we explore how it arises, as well as some properties & consequences of it."
keywords:
  - "bottom"
  - "divergence"
  - "runtime errors"
  - "predicate logic of bottom"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-06T10:40-06:00"
  updated: "2026-02-11T10:00-06:00"
---

## agenda

- divergence
- runtime errors
- properties & consequences of $\bot$
- predicate logic with $\bot$

## divergence

up until now, we've always discussed programs that _**converge**_ to some end state, $\tau$. e.g. $\lang S, \sigma \rang \rarr^* \lang E, \tau \rang$ & $M(S,\sigma) = \{\tau\}$.

however, not all programs will converge. when a prog runs w/out ever
reaching termination, it is said to _**diverge**_. in denotational
semantics this means that while the program doesn't end in a valid
state, it instead ends in a pseudo-state, "bottom"&mdash;notated
as $\bot_d$. e.g. $M(S,\sigma) = \{\bot_d\}$.

:::

two common ways that some program $S$ diverges in state $\sigma$ are:

1. in iterative statements (i.e. infinite loops):

   $$
   \begin{aligned}
   &W \equiv \text{while}\; e \;\text{do}\; s \;\text{od} &&
       \htmlClass{hljs-comment}{\textit{// some while loop of $e$ \& $s$}} \\
   &\lang W, \sigma_0 \rang \rarr^* \lang W, \sigma_1 \rang \rarr^* \lang W, \sigma_2 \rang \rarr \dots &&
       \htmlClass{hljs-comment}{\textit{// evaluation yields sequence}} \\
   \\
   &\neg \exist i.\sigma_i(e) = F &&
       \htmlClass{hljs-comment}{\textit{// $e$ never evaluates to False}} \\
   &\quad\quad \implies M(W,\sigma) = \{\bot_d\} &&
       \htmlClass{hljs-comment}{\textit{// then $W$ diverges in $\sigma$}}
   \end{aligned}
   $$

2. when there is a cycle in the operational semantic evaluation (i.e. infinite recursion):

   $$
   \begin{aligned}
   &\lang S_0, \sigma_0 \rang \rarr^* \lang S_1, \sigma_1 \rang \rarr^* \lang S_2, \sigma_2 \rang \rarr \dots &&
       \htmlClass{hljs-comment}{\textit{// for some sequence}} \\
   \\
   &\exist i.\exist j.i \ne j \land S_i = S_j \land \sigma_i = \sigma_j &&
       \htmlClass{hljs-comment}{\textit{// two configurations are equivalent}} \\
   &\quad\quad \implies M(S_0,\sigma_0) = \{\bot_d\} &&
       \htmlClass{hljs-comment}{\textit{// then $S_0$ diverges in $\sigma_0$}}
   \end{aligned}
   $$

:::

> [!ASIDE]
>
> ### practicing op semantics
>
> evaluate the configurations:
>
> <details>
>   <summary>
>
> evaluate $W \equiv \text{while}\; T \;\text{do skip od}$ in $\sigma$
>
>   </summary>
>
> $$
> \begin{aligned}
> &\forall \sigma . \sigma(T) = T \\
> &\lang W, \sigma \rang \rarr \lang \text{skip}; W, \sigma \rang \rarr \lang W, \sigma \rang \\
> &M(W,\sigma) = \{\bot_d\} \space_\blacksquare
> \end{aligned}
> $$
>
> </details>

## runtime errors

another way a program terminates in the bottom pseudo-state is by
encountering a runtime error & exiting w/out completing evaluation. for
this one, we use $\bot_e$. runtime errors can occur in evaluation of
expressions & statements.

there are two types of runtime errors arising from expressions:

1. _**primary failure**_&mdash;when a primative value —/or operation isn't
   supported or has exceptional behaviour, including:
   - array index out of bounds: $\sigma(b[e]) = \bot_e$ if $\sigma(e) < 0$
     or $\sigma(e) > size(b)$
   - division by zero
   - sqaure root of a negative number

2. _**hereditary failure**_&mdash;when evaluation of a subexpression fails,
   then the entire expression fails
   - for some unary operator $u$,
     then $\sigma(e) = \bot_e \implies \sigma(u e) = \bot_e$
   - for some binary operator $b$,
     then $\sigma(e_1) = \bot_e \lor \sigma(e_2) = \bot_e \implies \sigma(e_1 b e_2) = \bot_e$

runtime errors cause the statement they appear to halt unsuccessfully
&mdash;i.e. $\lang S, \sigma \rang \rarr \lang E, \bot_e \rang$.

### operational semantics rules

this means we can expand the rules of our language's operational
semantics (first defined in [a previous lecture](../0204-statements_simplified_lang/))
to the following:

- _**no-op**_: no change

  $$
  \begin{aligned}
  \lang \text{skip}, \sigma \rang \rarr \lang E, \sigma \rang
  \end{aligned}
  $$

- _**assignment**_: now fails if the value expression to assign to $v$ (or if
  expression giving array index) yields a runtime error

  $$
  \begin{aligned}
  &\htmlClass{hljs-comment}{\textit{// simple assignment}} \\
  &\lang v \coloneqq e, \sigma \rang \rarr
  \begin{cases}
      \lang E, \bot_e \rang, & \sigma(e) = \bot_e \\
      \lang E, \sigma[v \mapsto \sigma(e)] \rang, &otherwise \\
  \end{cases} \\
  &\htmlClass{hljs-comment}{\textit{// array element update}} \\
  &\lang b[e_1] \coloneqq e_2, \sigma \rang \rarr
  \begin{cases}
      \lang E, \bot_e \rang, & \sigma(e_1) = \bot_e \lor \sigma(e_2) = \bot_e \\
      \lang E, \sigma[b[\sigma(e_1)] \mapsto \sigma(e_2)] \rang, &otherwise \\
  \end{cases} \\
  \end{aligned}
  $$

- _**conditional**_: now fails if the guard expression yields a runtime error

  $$
  \begin{aligned}
  &\lang C, \sigma \rang
      \rarr \begin{cases}
                \lang E, \bot_e \rang,   &\sigma(e) = \bot_e \\
                \lang s_1, \sigma \rang, &\sigma(e) = T \\
                \lang s_2, \sigma \rang, &\text{otherwise}
            \end{cases} \\
  &\quad\text{where} \\
  &\quad\quad C \equiv \text{if}\; e \;\text{then}\; s_1 \;\text{else}\; s_2 \;\text{fi} \\
  \\
  &\htmlClass{hljs-comment}{\textit{// or if the else is elided}} \\
  \\
  &\lang C, \sigma \rang
      \rarr \begin{cases}
                \lang E, \bot_e \rang,   &\sigma(e) = \bot_e \\
                \lang s_1, \sigma \rang, &\sigma(e) = T \\
                \lang \text{skip}, \sigma \rang, &\text{otherwise}
            \end{cases} \\
  &\quad\text{where} \\
  &\quad\quad C \equiv \text{if}\; e \;\text{then}\; s_1 \;\text{fi} \\
  \end{aligned}
  $$

- _**iterative**_: now fails if the guard expression yields a runtime error

  $$
  \begin{aligned}
  &\lang W, \sigma \rang
      \rarr \begin{cases}
                \lang E, \bot_e \rang,   &\sigma(e) = \bot_e \\
                \lang s; W, \sigma \rang, &\sigma(e) = T \\
                \lang E, \sigma \rang, &\text{otherwise}
            \end{cases} \\
  &\quad\text{where} \\
  &\quad\quad W \equiv \text{while}\; e \;\text{do}\; s \;\text{od} \\
  \end{aligned}
  $$

- _**sequence**_: no change (runtime errors may still happen in evaluation
  other statements encountered while evaluating $s_1; s_2$)

  $$
  \begin{aligned}
  &\begin{cases}
      \lang s_1; s_2, \sigma \rang \rarr \lang U; s_2, \sigma_1 \rang, &\text{if}\; \lang s_1, \sigma \rang \rarr \lang U, \sigma_1 \rang \\
      \lang s_1; s_2, \sigma \rang \rarr \lang s_2, \sigma_1 \rang, &\text{if}\; \lang s_1, \sigma \rang \rarr \lang E, \sigma_1 \rang \\
  \end{cases}, \;\text{where} \\
  &\quad\quad U \;\text{represents an unknown statement} \\
  \end{aligned}
  $$

## properties & consequences of $\bot$

we use $\bot$ to refer to an actual memory state (just like any other non-error state, $\sigma$ ), thus we must think about any situation we can use a state & know how to use $\bot$ there as well.

> [!NOTE]
>
> the symbol $\bot$ (w/out subscripts) is used to generically refer to any
> failure to fully evaluate a program to termination, including both $\bot_d$
> & $\bot_e$. it can be used in place of either when it's not important which
> one occurred/will occur.

some rules that arise from this:

- $\bot$ is not a _well-formed_ state (i.e. it is always _ill-formed_ for any
  expression/statement)
- $\bot$ is excluded when referring to generalities such as "for all
  states" $\forall \sigma$, "for some state", "for all semantic values", or
  "for some semantic values"
- $\bot$ cannot be bound to any value (it is not a valid result of an
  expression!)
- evaluating any expression or statement in $\bot$ results in $\bot$
  &mdash;$\bot(e) = \bot$
- execution halts as soon as $\bot$ is generated

let's take a step back & look at booleans&mdash;a predicate & a boolean
expression have some similarities: both evaluate to booleans in proper states.
however, quantifiers cannot appear in boolean code expressions (not directly at
least, there's always while statements to give the same semantic meaning as a
quantifier...) while a predicate is used to describe a _property_ of some setof values.

evaluation of a predicate can end up in errors as well; yet when this happens
it is _**not**_ considered to be $\bot_e$. this is because while we understand
these errors arising from predicate quantifiers the same way we do runtime
errors, the predicates are not a part of the program & as such, cannot
be $\bot_e$. instead, we use the general $\bot$ to refer to them.

armed with this information, let's examine $\bot$ in the context of quantified predicates:

starting with this property of bottom: $\bot \not \models p\; \forall p$ _even if $p = T$!_

this means that there are 3 possible situations for a state attempting to
satisfy a predicate:

1. $\sigma(p) = T \iff \sigma \models p$
2. $\sigma(p) = F \implies \sigma \not \models p$
3. $\sigma(p) = \bot \implies \sigma \not \models p$

> [!IMPORTANT]
>
> note situations 2 & 3 both imply the same thing, while 1 is described w/ iff.
> this is because $\sigma \not \models p \not \implies \sigma \models \neg p$
> now as consequence of $\bot$ ; e.g. $\sigma \not \models p$ could be
> because $\sigma(p) = F$ **or** $\sigma(p) = \bot$.
