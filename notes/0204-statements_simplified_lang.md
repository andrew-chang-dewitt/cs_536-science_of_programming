---
title: "Program verification: statements & operational semantics"
description: "Defining some statements for a simplified language, then discussing how to prove they have the desired effect on a given state."
keywords:
  - "simple statements"
  - "operational semantics"
  - "program verification"
  - "cs 536"
  - "lecture notes"
  - "computer science"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-02-04T10:00-06:00"
---

## agenda

- statement definitions
- operational semantics of statements

## statement definitions

in class, the definitions were more long form w/ discussion, but here they're condensed to something close to BNF format:

```bnf
    program <p> ::= <s> | <s> ";" <p>  // a sequence of statements

  statement <s> ::= <k> | <a> | <i> | <w>

      no-op <k> ::= "skip"
 assignment <a> ::= <id> ":=" <e>  // some id bound to an expr
conditional <i> ::= "if" <e> "then" <s> "else" <s> "fi" | "if" <e> "then" <s> "fi"  // elide the else if statement is skip
  iteration <w> ::= "while" <e> "do" <s> "od"
```

## operational semantics of statements

more interesting for this course's purposes is proving that the above
statements work how they're expected to. one way to do this is using
_**operational semantics**_, wherin a _**configuration**_ (an ordered
pair $\lang S, \sigma \rang$ of statement & state) is executed to
compute each step of a program.

denoted as a relation on
configurations $\lang S, \sigma \rang \rarr \lang S_1, \sigma_1 \rang$,
meaning that executing $S$ in $\sigma$ yields the
configuration $\lang S_1, \sigma_1$ & $S_1$ is considered the
_**continuation**_ of $S$

if there is a sequence of
configurations $\lang S, \sigma \rang \rarr \dots \rarr \lang E, \tau \rang$
(where $E$ means "no statement"&mdash;i.e. end of program), we say

> execution of $S$ starting in state $\sigma$ _**converges**_ to (or
> terminates in) state $\tau$

:::

we define the operational semantics of our program statements by
starting with the axiomatic ones: skip, assignment, conditional, &
while statements. sequences, however, are slightly trickier, as we'll
see below.

- _**no-op**_:

  $$
  \begin{aligned}
  \lang \text{skip}, \sigma \rang \rarr \lang E, \sigma \rang
  \end{aligned}
  $$

- _**assignment**_:

  $$
  \begin{aligned}
  \lang v \coloneqq e, \sigma \rang \rarr \lang E, \sigma[v \mapsto \sigma(e)] \rang
  \end{aligned}
  $$

- _**conditional**_:

  $$
  \begin{aligned}
  &\lang \text{if}\; e \;\text{then}\; s_1 \;\text{else}\; s_2 \;\text{fi}, \sigma \rang
      \rarr \begin{cases}
                \lang s_1, \sigma \rang, &\sigma(e) = T \\
                \lang s_2, \sigma \rang, &\text{otherwise}
            \end{cases} \\
  \\
  &\textit{or if the else is elided} \\
  \\
  &\lang \text{if}\; e \;\text{then}\; s_1 \;\text{fi}, \sigma \rang
      \rarr \begin{cases}
                \lang s_1, \sigma \rang, &\sigma(e) = T \\
                \lang \text{skip}, \sigma \rang, &\text{otherwise}
            \end{cases} \\
  \end{aligned}
  $$

- _**iterative**_:

  $$
  \begin{aligned}
  &\lang W, \sigma \rang
      \rarr \begin{cases}
                \lang s; W, \sigma \rang, &\sigma(e) = T \\
                \lang E, \sigma \rang, &\text{otherwise}
            \end{cases}, \;\text{where} \\
  &\quad\quad W \equiv \text{while}\; e \;\text{do}\; s \;\text{od} \\
  \end{aligned}
  $$

- _**sequence**_:
  takes a little more work. since the evaluation of some statement can result
  in any of the other statements (i.e. by sequence or while loop) or $E$, &
  because the first statement in a chain of statements can be any arbitrary
  statement, it is not possible to know what that first statement evaluates to.
  to get around this, a sequence statement of two arbitrary statements can be
  evaluated in one of two ways:

  $$
  \begin{aligned}
  &\begin{cases}
      \lang s_1; s_2, \sigma \rang \rarr \lang U; s_2, \sigma_1 \rang, &\text{if}\; \lang s_1, \sigma \rang \rarr \lang U, \sigma_1 \rang \\
      \lang s_1; s_2, \sigma \rang \rarr \lang s_2, \sigma_1 \rang, &\text{if}\; \lang s_1, \sigma \rang \rarr \lang E, \sigma_1 \rang \\
  \end{cases}, \;\text{where} \\
  &\quad\quad U \;\text{represents an unknown statement} \\
  \end{aligned}
  $$

:::

> [!ASIDE]
>
> ### practicing op semantics
>
> evaluate the configurations:
>
> - <details>
>     <summary>
>
>   $\lang x \coloneqq 5 * x + 6, \{x = 1,y = 2\} \rang$
>
>     </summary>
>
>   $$
>   \begin{aligned}
>   \lang x \coloneqq 5 * x + 6, \{x = 1,y = 2\} \rang \rarr \lang E, \{ x=11,y=2 \}\rang
>   \end{aligned}
>   $$
>
>   </details>
>
> - <details>
>     <summary>
>
>   with $\sigma(x) = 8$, $\lang b[x + 1] \coloneqq x * 5, \sigma \rang$
>
>     </summary>
>
>   $$
>   \begin{aligned}
>   \lang b[x + 1] \coloneqq x * 5, \sigma \rang \rarr \lang E, \sigma[b[9] \mapsto 40]\rang
>   \end{aligned}
>   $$
>
>   </details>
>
> - <details>
>     <summary>
>
>   let $S \equiv \;\text{if}\; x > 0 \;\text{then}\; y \coloneqq 0$, then:
>   1. evaluate $S$ in $\sigma$, where $\sigma(x) = 5$
>   2. evaluate $S$ in $\sigma'$, where $\sigma'(x) < -2$
>
>     </summary>
>   1. $\lang S, \sigma \rang \rarr \lang , \sigma' \rang \rarr \lang E, \sigma[y \mapsto 0] \rang$
>   2. $\lang S, \sigma' \rang \rarr \lang \text{skip}, \sigma' \rang \rarr \lang E, \sigma' \rang$
>
>   </details>
>
> - <details>
>     <summary>
>
>   for the following definitions of $S$, $S_1$, & $W$, evaluate $S$ in
>   state $\sigma$, with $\sigma(n) = 1$:
>
>   $$
>   \begin{aligned}
>     S &\equiv s \coloneqq 0; k \coloneqq 0; W \\
>     W &\equiv \text{while}\; k < n \;\text{do}\ S_1 \;\text{od} \\
>   S_1 &\equiv s \coloneqq s + k + 1; k\coloneqq k + 1 \\
>   \end{aligned}
>   $$
>
>     </summary>
>
>   $$
>   \begin{aligned}
>         &\lang S, \sigma \rang \\
>   =     &\lang s \coloneqq 0; k \coloneqq 0; W, \sigma \rang \\
>   \rarr &\lang k \coloneqq 0; W, \sigma[s \mapsto 0] \rang \\
>   \rarr &\lang W, \sigma[s \mapsto 0][k \mapsto 0] \rang \\
>   =     &\lang \text{while}\; k < n \;\text{do}\ S_1 \;\text{od}, \\
>         &\quad\quad \sigma[s \mapsto 0][k \mapsto 0] \rang \\
>         &\htmlClass{hljs-comment}{\textit{// $\sigma(k < n) = 0 < 1 = T$}} \\
>   \rarr &\lang S_1; W, \sigma[s \mapsto 0][k \mapsto 0] \rang \\
>   =     &\lang s \coloneqq s + k + 1; k\coloneqq k + 1; W, \\
>         &\quad\quad \sigma[s \mapsto 0][k \mapsto 0] \rang \\
>         &\htmlClass{hljs-comment}{\textit{// $s \coloneqq \sigma(s + k + 1) = 1$}} \\
>   \rarr &\lang k\coloneqq k + 1; W, \sigma[s \mapsto 1][k \mapsto 0] \rang \\
>         &\htmlClass{hljs-comment}{\textit{// $k \coloneqq \sigma(k + 1) = 1$}} \\
>   \rarr &\lang W, \sigma[s \mapsto 1][k \mapsto 1] \rang \\
>   =     &\lang \text{while}\; k < n \;\text{do}\ S_1 \;\text{od}, \\
>         &\quad\quad \sigma[s \mapsto 1][k \mapsto 1] \rang \\
>         &\htmlClass{hljs-comment}{\textit{// $\sigma(k < n) = 1 < 1 = F$}} \\
>   \rarr &\lang E, \sigma[s \mapsto 1][k \mapsto 1] \rang \\
>   \end{aligned}
>   $$
>
>   </details>
