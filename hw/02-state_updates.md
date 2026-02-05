:::hgroup{.titlegroup}

# assignment 2

Andrew Chang-DeWitt \
Feb. 5, 2026 \
CS 536

:::

## Question 1

:::{.question}

> Let 𝑢 and 𝑣 be some primitive type variables and 𝛼 and 𝛽 be some
> values that match the types of 𝑢 and 𝑣 (𝑢 and 𝑣 might be the same
> variable, 𝛼 and 𝛽 might be the same value). When does 𝜎[𝑢 ↦ 𝛼][𝑣 ↦ 𝛽]
> = 𝜎[𝑣 ↦ 𝛽][𝑢 ↦ 𝛼] and when does 𝜎[𝑢 ↦ 𝛼][𝑣 ↦𝛽] ≡ 𝜎[𝑣 ↦𝛽][𝑢 ↦𝛼]?
> Discuss the four different cases depending on whether 𝑢 ≡ 𝑣 and
> whether 𝛼 = 𝛽.

:::

first, let's simplify things a little:

$$
\begin{aligned}
\sigma[u \mapsto \alpha][v \mapsto \beta] \setminus \sigma
        &= \sigma[v \mapsto \beta][u \mapsto \alpha] \setminus \sigma && \textit{because $\sigma = \sigma$, remove it} \\
\empty[u \mapsto \alpha][v \mapsto \beta]
        &= \empty[v \mapsto \beta][u \mapsto \alpha] \tag{1.1} \\
\end{aligned}
$$

now, let's examine each case:

$$
\begin{alignedat}{4}
u \equiv v \land \alpha = \beta
        &\implies& \empty[u \mapsto \alpha][u \mapsto \alpha]
                &\stackrel{?}{=} \empty[u \mapsto \alpha][u \mapsto \alpha] &&
                    \quad\textit{(1.1)} \\
        &\implies& \{u = \alpha\}[u \mapsto \alpha]
                &\stackrel{?}{=} \{ u = \alpha\}[u \mapsto \alpha] && \\
        &\implies& \{u = \alpha\}
                &= \{ u = \alpha\} &&
                    \quad\textit{end states syntactically equivalent} \\
        &\implies& \{u = \alpha\}
                &\equiv \{ u = \alpha\}
                    \space_\blacksquare &&
                    \quad\textit{\& semantically equivalent as well} \\
\\
u \equiv v \land \alpha \ne \beta
        &\implies& \empty[u \mapsto \alpha][u \mapsto \beta]
                &\stackrel{?}{=} \empty[u \mapsto \beta][u \mapsto \alpha] &&
                    \quad\textit{(1.1)} \\
        &\implies& \{ u = \alpha \}[u \mapsto \beta]
                &\stackrel{?}{=} \{ u \mapsto \beta \}[u \mapsto \alpha] && \\
        &\implies& \{ u = \beta \}
                &\ne \{ u = \alpha \} &&
                    \quad\textit{end states \textbf{not} semantically equivalent} \\
        &\implies& \{ u = \beta \}
                &\not \equiv \{ u = \alpha \}
                    \space_\blacksquare &&
                    \quad\textit{\& \textbf{not} semantically equivalent} \\
\\
u \not \equiv v \land \alpha = \beta
        &\implies& \empty[u \mapsto \beta][v \mapsto \beta]
                &\stackrel{?}{=} \empty[v \mapsto \beta][u \mapsto \beta] &&
                    \quad\textit{(1.1)} \\
        &\implies& \{ u = \beta \}[v \mapsto \beta]
                &\stackrel{?}{=} \{ v \mapsto \beta \}[u \mapsto \beta] && \\
        &\implies& \{ u = \beta, v = \beta \}
                &= \{ v = \beta, u = \beta \} &&
                    \quad\textit{end states semantically equivalent} \\
        &\implies& \{ u = \beta, v = \beta \}
                &\not \equiv \{ v = \beta, u = \beta \}
                    \space_\blacksquare &&
                    \quad\textit{but, \textbf{not} semantically equivalent} \\
\\
u \not \equiv v \land \alpha \ne \beta
        &\implies& \empty[u \mapsto \alpha][v \mapsto \beta]
                &\stackrel{?}{=} \empty[v \mapsto \beta][u \mapsto \alpha] &&
                    \quad\textit{(1.1)} \\
        &\implies& \{ u = \alpha \}[v \mapsto \beta]
                &\stackrel{?}{=} \{ v \mapsto \beta \}[u \mapsto \alpha] && \\
        &\implies& \{ u = \alpha, v = \beta \}
                &= \{ v = \beta, u = \alpha \} &&
                    \quad\textit{end states semantically equivalent} \\
        &\implies& \{ u = \alpha, v = \beta \}
                &\not \equiv \{ v = \beta, u = \alpha \}
                    \space_\blacksquare &&
                    \quad\textit{but, \textbf{not} semantically equivalent} \\
\end{alignedat}
$$

with this, we can populate the provided table as a truth table:

|              | 𝜎[𝑢 ↦ 𝛼][𝑣 ↦ 𝛽] = 𝜎[𝑣 ↦ 𝛽][𝑢 ↦ 𝛼]? | 𝜎[𝑢 ↦ 𝛼][𝑣 ↦ 𝛽] ≡ 𝜎[𝑣 ↦ 𝛽][𝑢 ↦ 𝛼]? |
| ------------ | ---------------------------------- | ---------------------------------- |
| 𝑢 ≡ 𝑣, 𝛼 = 𝛽 | T                                  | T                                  |
| 𝑢 ≡ 𝑣, 𝛼 ≠ 𝛽 | F                                  | F                                  |
| 𝑢 ≢ 𝑣, 𝛼 = 𝛽 | T                                  | F                                  |
| 𝑢 ≢ 𝑣, 𝛼 ≠ 𝛽 | T                                  | F                                  |

## Question 2

:::{.question}

> Consider state 𝜎 = {𝑥 = 1, 𝑦 = 2, 𝑝 =𝑇, 𝑏 =(2,5,4,8)}. Answer the
> following questions and justify your answers briefly.

:::

<section>

### part a

:::{.question}

> What is the evaluation of expression 𝐢𝐟 𝑏[𝑥]> 𝑦 𝐭𝐡𝐞𝐧 𝑝 𝐞𝐥𝐬𝐞 𝑥 < 𝑦 𝐟𝐢
> in state 𝜎?

:::

$$
\begin{aligned}
\because
  &&         e_a &\equiv \text{if } b[x] > y \text{ then } p \text{ else } x < y \text{ fi } \\
\\
  && \sigma(e_a) &=      \text{if } b[1] > 2 \text{ then } T \text{ else } 1 < 2 \text{ fi } \\
  &&             &=      \text{if } 5 > 2 \text{ then } T \text{ else } 1 < 2 \text{ fi } \\
  &&             &=      \text{if } T \text{ then } T \text{ else } 1 < 2 \text{ fi } \\
  &&             &=      T \space_\blacksquare \\
\end{aligned}
$$

</section>
<section>

### part b

:::{.question}

> What is state 𝜎[𝑥 ↦ 𝜎(𝑦−2)][𝑝 ↦ 𝜎(𝑦 < 𝑥)]?

:::

$$
\begin{aligned}
\sigma[x \mapsto \sigma(y - 2)][p \mapsto \sigma(y < x)]
    &= \{ x = 1, y = 2, p = T, b = (2,5,4,8) \}[x \mapsto (2 - 2)][p \mapsto \sigma(y < x)] \\
    &= \{ x = 1, y = 2, p = T, b = (2,5,4,8) \}[x \mapsto 0][p \mapsto \sigma(y < x)] \\
    &= \{ x = 0, y = 2, p = T, b = (2,5,4,8) \}[p \mapsto (2 < 0)] \\
    &= \{ x = 0, y = 2, p = T, b = (2,5,4,8) \}[p \mapsto F] \\
    &= \{ x = 0, y = 2, p = F, b = (2,5,4,8) \} \space_\blacksquare \\
\end{aligned}
$$

</section>
<section>

### part c

:::{.question}

> Let 𝜏 = 𝜎[𝑥 ↦ 𝜎(𝑏[𝑦])], and 𝛾 = 𝜏[𝑦 ↦ 𝜏(𝑥)∗3]. What is state 𝛾?

:::

$$
\begin{aligned}
\gamma &= \tau[y \mapsto \tau(x)\cdot 3] \\
       &= \sigma[x \mapsto \sigma(b[y])][y \mapsto \tau(x)\cdot 3] \\
       &= \{ x = 1, y = 2, p = T, b = (2,5,4,8) \}[x \mapsto (2,5,4,8)[2]][y \mapsto \tau(x)\cdot 3] \\
       &= \{ x = 1, y = 2, p = T, b = (2,5,4,8) \}[x \mapsto 4][y \mapsto \tau(x)\cdot 3] \\
       &= \{ x = 4, y = 2, p = T, b = (2,5,4,8) \}[y \mapsto (4 \cdot 3)] \\
       &= \{ x = 4, y = 2, p = T, b = (2,5,4,8) \}[y \mapsto 12] \\
\gamma &= \{ x = 4, y = 12, p = T, b = (2,5,4,8) \} \space_\blacksquare \\
\end{aligned}
$$

</section>
<section>

### part d

:::{.question}

> Is it true that 𝜎 ⊨ ∀𝑥.𝑥 < 3 → 𝑦 ≥ 2 ?

:::

first, recall the definition of a bounded quantifier:

$$
\begin{aligned}
&(\forall x.p \longrightarrow q) \equiv (\forall p.q)
\tag{2.d.1}
\end{aligned}
$$

and the definition of some state modeling some predicate quantified over all values in some domain:

$$
\begin{aligned}
\sigma \models \forall x \in S.p
    \iff \forall \alpha \in S.\sigma[x \mapsto \alpha] \models p
        \tag{2.d.2}
\end{aligned}
$$

with this, the predicate above can be rewritten in terms of $x$, $p$, & $q$:

$$
\begin{aligned}
&\forall x.p \longrightarrow q \equiv \forall p.q && \textit{by (2.d.1)}\\
&\quad\quad  \begin{aligned} \text{where} \\
                p &\equiv x < 3 \\
                q &\equiv y \ge 2
            \end{aligned} \\
\tag{2.d.3}
\end{aligned}
$$

to see if $\sigma \models \forall x.x < 3 \longrightarrow y \ge 2$ holds, it must be shown that $q$ (2.d.3) is modeled by $\sigma[x \mapsto \alpha]$ for all $\alpha$ in the domain defined by $p$. because updating $x$ in $\sigma$ has no effect on the value of $\sigma(y)$, $\sigma \models \forall p.q$ can be rewritten as $\sigma \models q$, which can then be proven true as follows:

$$
\begin{aligned}
\sigma \models q &\iff \sigma(q) \\
                 &\iff \sigma(y \ge 2) &&
                        \textit{$q$ bound in (2.d.3)} \\
                 &\iff 2 \ge 2 \\
                 &\iff T \space_\blacksquare
\end{aligned}
$$

</section>
<section>

### part e

:::{.question}

> Is it true that 𝜎 ⊨ 𝑥 ≥ 1 ∧ ∃ 0 ≤ 𝑥 < 4.𝑏[𝑥] < 3 ?

:::

similar for the universal above (2.d.1), the existential can be bounded in $p$ & rewritten:

$$
\begin{aligned}
\exists x.p \land q \equiv \exists p.q
\tag{2.e.1}
\end{aligned}
$$

thus, with the definition of a state satisfying an existential:

$$
\begin{aligned}
\sigma \models \exists x \in S.p \iff \exists \alpha \in S \text{ s.t. } \sigma[x \mapsto \alpha] \models p
\tag{2.e.2}
\end{aligned}
$$

it can be proven that:

$$
\begin{aligned}
&\sigma \models x \ge 1 \land \exists 0 \le x < 4.b[x] < 3 \\
&\quad\quad  \begin{aligned}
                \iff && (\sigma \models x \ge 1) &\land (\sigma \models \exists 0 \le x < 4.b[x] < 3) \\
                \iff &&     (\sigma(x) \ge 1)    &\land (\exists 0 \le \alpha < 4 \text{ s.t. } \sigma[x \mapsto \alpha](b[x] < 3)) &&
                    \textit{by (2.e.1) \& (2.e.2)}\\
                \iff &&          (1 \ge 1)       &\land (\sigma[x \mapsto 0](b[x] < 3)) \\
                \iff &&              T           &\land (\{ x = 0, y = 2, p = T, b = (2,5,4,8) \}(b[x] < 3)) \\
                \iff &&              T           &\land ((2,5,4,8)[0] < 3) \\
                \iff &&              T           &\land (2 < 3) \\
                \iff &&              T           &\land T \\
                \iff &&                            &\;T \space_\blacksquare
            \end{aligned} \\
\end{aligned}
$$

</section>
