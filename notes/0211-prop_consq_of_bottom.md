---
title: "Program verification: bottom"
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

there are two types of runtime errors:

1. _**primary failure**_&mdash;when a primative value —/or operation isn't supported or has exceptional behaviour, including:
   - array index out of bounds: $\sigma(b[e]) = \bot_e$ if $\sigma(e) < 0$
     or $\sigma(e) > size(b)$
   - division by zero
   - sqaure root of a negative number

2. _**hereditary failure**_&mdash;when evaluation of a subexpression fails, then the entire expression fails

## properties & consequences of $\bot$

## predicate logic with $\bot$
