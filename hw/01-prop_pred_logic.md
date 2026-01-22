:::hgroup{.titlegroup}

# assignment 1

Andrew Chang-DeWitt \
Jan. 21, 2026 \
CS 536

:::

## Question 1

:::{.question}

> Decide true or false for each of the following statements. Justify your answers briefly. Variables 𝑝 and 𝑞 used
> here are propositional variables.

:::

### part (a)

:::{.question}

> {𝑥 = 2, 𝑝 = 𝑇} ⊨ 𝑥 > 2 ∨ 𝑝.

:::

True, because:

$$
\begin{aligned}
\sigma &\coloneqq \{ x = 2, p = T \} \\
\end{aligned}
\\
\begin{aligned}
\\
\sigma \models x &> 2 \lor p \\
                 &\implies \sigma(x) > 2 \lor T \\
                 &\iff 2 > 2 \lor T \\
                 &\iff F \lor T \\
                 &\iff T \space_\blacksquare
\end{aligned}
$$

### part (b)

:::{.question}

> {𝑥 = 2, 𝑝 = 2, 𝑝 = 𝑇} is a well-formed state.

:::

False, because $p$ is bound twice in $\{x = 2, p = 2, p = T \}$

### part (c)

:::{.question}

> Any state is proper for 𝐹 → 𝑝.

:::

False, because $p \not \in \empty$

### part (d)

:::{.question}

> ⊨ 𝑝 → 𝑝 → 𝑝 ∨ 𝑞

:::

True, because the expression is reducible to a tautology:

$$
\begin{aligned}
\models p &\longrightarrow p \longrightarrow p \lor q \\
          &\iff \models p \longrightarrow (p \longrightarrow (p \lor q))
              && \textit{parenthesization} \\
          &\iff \models p \longrightarrow (\neg p \lor (p \lor q))
              && \textit{definition of implication} \\
          &\iff \models p \longrightarrow ((\neg p \lor p) \lor q)
              && \textit{associativity of $\lor$} \\
          &\iff \models p \longrightarrow (T \lor q)
              && \textit{tautology} \\
          &\iff \models p \longrightarrow (q \lor T)
              && \textit{commutativity of $\lor$} \\
          &\iff \models p \longrightarrow T
              && \textit{domination} \\
          &\iff \models \neg p \lor T
              && \textit{definition of implication} \\
          &\iff \models T \space_\blacksquare
              && \textit{domination}
\end{aligned}
$$

### part (e)

:::{.question}

> ⊭ 𝑝 ∨ ¬𝑝

:::

False, because $p \lor \neg p$ is a tautology

## Question 2

:::{.question}

> Let 𝑝1 and 𝑝2 be two propositions or predicates.

:::

### part (a)

:::{.question}

> Does 𝑝1 ⇔ 𝑝2 logically imply 𝑝₁ ≡ 𝑝₂? If yes, briefly justify your answer; if not, give a counterexample.

:::

Given $\iff$ means _semantic_ equality while $\equiv$ means _syntactic_ equality, $p1 \iff p2$ does not logically imply $p1 \equiv p2$. This is because two expressions can be semantically equivalent while still being syntactically different. For example, given $p1$ & $p2$ as:

$$
\begin{aligned}
p1 \coloneqq &6 - 4 \\
p2 \coloneqq &1 + 1
\end{aligned}
$$

this holds

$$
\begin{aligned}
6 - 4 &\iff 1 + 1 \\
    2 &\iff 2 \\
   p1 &\iff p2
\end{aligned}
$$

however, $p1 \equiv p2$ does not.

### part (b)

:::{.question}

> Does 𝑝1 ↔ 𝑝2 ⇔ 𝐹 logically imply 𝑝1 ≢ 𝑝2? If yes, briefly justify your answer; if not, give a counterexample.

:::

Yes, because $p1 \longleftrightarrow p2 \iff F$ means that either $p1 \longrightarrow p2$ or $p2 \longrightarrow p1$ must be false, thus $p1$ & $p2$ must be semantically different. Consider that with the fact that if two propositions _are_ syntactically equal, then they are implied to be semantically equal, we can conclude that $p1 \not \equiv p2$ in this case.

## Question 3

:::{.question}

> Prove the following logical equivalences. You can either use Truth Tables or the rules provided in Lecture 2 to prove them.

:::

### part (a)

:::{.question}

> ¬(𝑝 ↔ 𝑞) ⇔ ¬𝑝 ↔ 𝑞

:::

| $p$ | $q$ | $p \longleftrightarrow q$ | $\neg (p \longleftrightarrow q)$ | $\neg p$ | $\neg p \longleftrightarrow q$ |
| --- | --- | ------------------------- | -------------------------------- | -------- | ------------------------------ |
| F   | F   | T                         | **F**                            | T        | **F**                          |
| F   | T   | F                         | **T**                            | T        | **T**                          |
| T   | F   | F                         | **T**                            | F        | **T**                          |
| T   | T   | T                         | **F**                            | F        | **F**                          |

<!--
not sure how to make this proof work...

$$
\begin{aligned}
\neg (p \longleftrightarrow q) &\iff \neg p \longleftrightarrow q \\
\neg ((p \longrightarrow q) \land (q \longrightarrow p)) &\iff \neg p \longleftrightarrow q
                                    && \textit{definition of biconditional} \\
\neg (p \longrightarrow q) \lor \neg (q \longrightarrow p) &\iff \neg p \longleftrightarrow q
                                    && \textit{DeMorgan's Law} \\
(p \lor q) \lor (q \lor p) &\iff \neg p \longleftrightarrow q
                                    && \textit{DeMorgan's Law} \\
(p \lor q) \lor (q \lor p) &\iff (\neg p \longrightarrow q) \land (q \longrightarrow \neg p)
                                    && \textit{definition of biconditional} \\
(p \lor q) \lor (q \lor p) &\iff (\neg \neg p \lor q) \land (\neg q \lor \neg p)
                                    && \textit{definition of implication} \\
\end{aligned}
$$
-->

### part (b)

:::{.question}

> (𝑝 → 𝑞) ∧ (¬𝑝 → 𝑞) ⇔ 𝑞

:::

| $p$ | $q$   | $p \longrightarrow q \quad (1)$ | $\neg p$ | $\neg p \longrightarrow q \quad (2)$ | $(1) \land (2)$ |
| --- | ----- | ------------------------------- | -------- | ------------------------------------ | --------------- |
| F   | **F** | T                               | T        | F                                    | **F**           |
| F   | **T** | T                               | T        | T                                    | **T**           |
| T   | **F** | F                               | F        | T                                    | **F**           |
| T   | **T** | T                               | F        | T                                    | **T**           |

## Question 4

:::{.question}

> Define the following predicate functions.

:::

> [!TODO]
>
> check these both w/ the test cases given! make sure to pay close attention to
> off by one errors in defining the range for $\forall i.i<?$

### part (a)

:::{.question}

> Define a predicate function 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 𝑛) which is 𝑇𝑟𝑢𝑒 if and only if
> the first 𝑛 elements of integer array 𝑏 is sorted in the reversed order, in
> other word, 𝑏[0] ≥ 𝑏[1] ≥ 𝑏[2] ≥ ⋯ ≥ 𝑏[𝑛 − 1]. You may assume that array 𝑏
> has at least 𝑛 elements and 𝑛 is positive, so you don’t need to worry about
> the domain of 𝑛. For example, if 𝑏 = (4, 3, 4, 3), then 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 1)
> is 𝑇𝑟𝑢𝑒, 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 2) is 𝑇𝑟𝑢𝑒 but 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 3) is 𝐹𝑎𝑙𝑠𝑒.

:::

$$
\begin{aligned}
\text{ReverseSorted}(b,n) \equiv \forall i.i < n - 1 \implies b[i] \ge b[i + 1]
\end{aligned}
$$

### part (b)

:::{.question}

> Define a predicate function 𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 𝑚) which is 𝑇𝑟𝑢𝑒 if and only if the
> first 𝑚 elements of integer array 𝑏 match the second 𝑚 elements of 𝑏, in
> other words, 𝑏[0] = 𝑏[𝑚], 𝑏[1] = 𝑏[𝑚 + 1],…, 𝑏[𝑚 − 1] = 𝑏[2 ∗ 𝑚 − 1]. You may
> assume that 𝑚 is positive and 2 ∗ 𝑚 − 1 is less than length array 𝑏, so you
> don’t need to worry about the domain of 𝑚. For example, if
> 𝑏 = (1, 3, 5, 1, 3, 5), then 𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 3) is 𝑇𝑟𝑢𝑒 but 𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 2) is 𝐹𝑎𝑙𝑠𝑒

:::

$$
\begin{aligned}
\text{Repeats}(b,m) \equiv \forall i.i < m - 1 \implies b[i] = b[i + m]
\end{aligned}
$$

