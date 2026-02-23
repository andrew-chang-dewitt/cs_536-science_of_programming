:::hgroup{.titlegroup}

# assignment 4

Andrew Chang-DeWitt \
Feb. 20, 2026 \
CS 536

:::

## Question 1

:::{.question}

> Let Σ be the collection of all well-formed states, and Σ<sub>⊥</sub> = Σ ∪ {⊥}. Decide
> true or false for each of the following statements, justify your answers
> briefly. Here, 𝜎 and 𝜏 are (possibly pseudo) states.

:::

<section>

### part (a)

:::{.question}

> Let 𝜏 ∈ Σ<sub>⊥</sub>, then 𝜏 ⊨ 𝑥 > 1 or 𝜏 ⊨ 𝑥 ≤ 1.

:::

False

$$
\begin{align}
\bot \not \models T &&
    \htmlClass{hljs-comment}{\textit{$\bot$ cannot satisfy any predicate}} \tag{1.a.1} \\
\notag \\
\bot \in \Sigma_\bot &\implies \tau \;\text{possibly is}\; \bot \notag \\
                                    &\implies \tau \not \models p, \;\text{where}\; p \;\text{is any predicate} \space_\blacksquare \notag \\
\end{align}
$$

</section>
<section>

### part (b)

:::{.question}

> Let Σ<sub>0</sub> ⊆ Σ<sub>⊥</sub>, then Σ<sub>0</sub> ⊨ 𝑇.

:::

False

$$
\begin{align}
&\Sigma_0 \models T \iff \sigma \models T \forall \sigma \in \Sigma_0 \tag{1.b.1} \\
\notag \\
&\quad\quad\;\; (\Sigma_0 \subseteq \Sigma_\bot) \land (\bot \in \Sigma_\bot) \notag \\
&\implies \bot \;\text{possibly}\; \in \Sigma_0 \notag \\
&\implies \neg (\sigma \models T \forall \sigma \in \Sigma_0) &&
    \htmlClass{hljs-comment}{\textit{by (1.a.1)}} \notag \\
&\implies \Sigma_0 \not \models T \space_\blacksquare &&
    \htmlClass{hljs-comment}{\textit{by (1.b.1)}} \notag \\
\end{align}
$$

</section>
<section>

### part (c)

:::{.question}

> Let Σ<sub>0</sub> ⊆ Σ and Σ<sub>0</sub> ⊨ 𝑥 > 1, also let 𝜏 ⊨ 𝑥 > 1; then Σ<sub>0</sub> ∪ {𝜏} ⊨ 𝑥 > 1.

:::

True

$$
\begin{aligned}
(\Sigma_0 \cup \{\tau\}) \models x > 1 = (\Sigma_0 \models x > 1) \land (\tau \models x > 1) \\
\end{aligned}
$$

</section>
<section>

### part (d)

:::{.question}

> Let Σ<sub>0</sub> ⊆ Σ, then Σ<sub>0</sub> ⊨ 𝑥 > 1 or Σ<sub>0</sub> ⊨ 𝑥 ≤ 1.

:::

True

$$
\begin{aligned}
\bot \not \in \Sigma \implies \bot \not \in \Sigma_0 \\
\neg (x > 1) = x \le 1 \\
(\Sigma_0 \models p) \lor (\Sigma_0 \models \neg p) \\
\\
p := x > 1 &\implies (\Sigma_0 \models x > 1) \lor (\Sigma_0 \models \not (x > 1)) \\
           &\implies (\Sigma_0 \models x > 1) \lor (\Sigma_0 \models x \le 1) \\
           &\implies True \space_\blacksquare \\
\end{aligned}
$$

</section>
<section>

### part (e)

:::{.question}

> Let 𝜎 ⊨ 𝑥 > 1 and let 𝜏 ⊨ 𝑥 < 1, then {𝜎,𝜏} ⊨ 𝑥 ≠ 1

:::

True

$$
\begin{aligned}
x > 1 \implies x \neq 1 &\implies \sigma \models x \neq 1 \\
x < 1 \implies x \neq 1 &\implies \tau \models x \neq 1 \\
\\
\{\sigma,\tau\} \models x \neq 1 &\iff           \sigma' \models x \neq 1 \forall \sigma' \in \{\sigma,\tau\} \\
                                 &\iff           (\sigma \models x \neq 1) \land (\tau \models x \neq 1) \\
                                 &\iff           T \space_\blacksquare \\
\end{aligned}
$$

</section>
<section>

## Question 2

:::{.question}

> Calculate denotational semantics for the following nondeterministic programs

:::

definitions of denotational semantics for `if - fi`

$$
\begin{align}
&\text{IF}' \equiv \text{if}\; B_1 \rarr S_1 \square
                              B_2 \rarr S_2 \square
                              \dotsb \square
                              B_n \rarr S_n \square
                \;\text{fi} \notag \\

&M(\text{IF}', \sigma') = \begin{cases}
                            \{\bot_e\},                           &\text{if}\; \sigma'(B_1 \lor B_2 \lor B_n) = F \\
                            \{M(S_i, \sigma') | \sigma'(B_i) = T\}, &otherwise
                        \end{cases} \tag{2.1}\\
\end{align}
$$

& `do - od`:

$$
\begin{align}
&\text{DO}' \equiv \text{do}\; B_1 \rarr S_1 \square
                              B_2 \rarr S_2 \square
                              \dotsb \square
                              B_n \rarr S_n \square
                \;\text{od} \notag \\

&M(\text{DO}', \sigma') =
    \begin{cases}
        \{\sigma'\},
            &\text{if}\; \sigma'(B_1 \lor B_2 \lor B_n) = F \\
        \{M(\text{DO}', M(S_i, \sigma')) | \sigma'(B_i) = T\},
            &otherwise
   \end{cases} \tag{2.2}\\
\end{align}
$$

### part (a)

:::{.question}

> Let 𝐷𝑂 ≡ 𝐝𝐨 𝑥 > 𝑦 → 𝑥 ≔ 𝑥 − 1 ◻ 𝑥 > 𝑦 → 𝑦 ≔ 𝑦 + 1 ◻ 𝑥 + 𝑦 = 4 → 𝑥 ≔ 𝑦/𝑥 ◻ 𝑥 + 𝑦 = 4 → 𝑥 ≔ 𝑥/𝑦 𝐨𝐝, \
> and let 𝜎<sub>1</sub> = {𝑥 = 3, 𝑦 = 1}. \
> Calculate 𝑀(𝐷𝑂,𝜎<sub>1</sub>) and show your work.

:::

conditions, $B_i$, & statements, $S_i$, from `DO`:

$$
\begin{aligned}
B_1 &\coloneqq x > y,     &S_1 &\coloneqq x \coloneqq x - 1, \\
B_2 &\coloneqq B_1,       &S_2 &\coloneqq y \coloneqq y + 1, \\
B_3 &\coloneqq x + y = 4, &S_3 &\coloneqq x \coloneqq y / x, \\
B_4 &\coloneqq B_3,       &S_4 &\coloneqq x \coloneqq x / y, \\
\end{aligned}
$$

denotational semantics, by iteration of `DO`:

$$
\begin{aligned}
    &     &M&(\text{DO}, \{x = 3, y = 1\})                \\
\\
    &=    &\{ &M(\text{DO}, \{x = 2, y = 1\}),           \\
    &\quad&   &M(\text{DO}, \{x = 3, y = 2\}),           \\
    &\quad&   &M(\text{DO}, \{x = \frac{1}{3}, y = 1\}), \\
    &\quad&   &M(\text{DO}, \{x = 3, y = 1\}) \}
  && \htmlClass{hljs-comment}{\textit{all guards true}}  \\
    &     &   &
  && \htmlClass{hljs-comment}{\textit{iteration 1 complete, by (2.2)}} \\
\\
    &=    &\{ &\{ \{x = 2, y = 1\} \},
      && \htmlClass{hljs-comment}{\textit{$\sigma(B_3 \lor B_4) = F$}} \\
    &\quad&   &\{ M(\text{DO},\{x = 1, y = 1\}),M(\text{DO},\{x = 2, y = 2\})\} \},
      && \htmlClass{hljs-comment}{\textit{$\sigma(B_1 \lor B_2) = T$}} \\
    &\quad&   &\{ \{x = 3, y = 2\} \},
      && \htmlClass{hljs-comment}{\textit{$\sigma(B_3 \lor B_4) = F$}} \\
    &\quad&   &\{ M(\text{DO},\{x = 2, y = 2\}),M(\text{DO},\{x = 3, y = 3\})\} \},
      && \htmlClass{hljs-comment}{\textit{$\sigma(B_1 \lor B_2) = T$}} \\
    &\quad&   &\{ \{x = \frac{1}{3}, y = 1\} \},
      && \htmlClass{hljs-comment}{\textit{$\sigma(B_1 \lor B_2 \lor B_3 \lor B_4) = F$}} \\
    &\quad&   &\{\bot_d\} \}

  && \htmlClass{hljs-comment}{\textit{$\{x = 3, y = 1\}$ is a cycle}}          \\
    &=    &\{ &\{x = 2, y = 1\}, \{x = 3, y = 2\}, \{ x = \frac{1}{3}, y = 1 \}, \bot_d
  && \htmlClass{hljs-comment}{\textit{flatten \& deduplicate}} \\
    &\quad&   &M(\text{DO},\{x = 1, y = 1\}), \\
    &\quad&   &M(\text{DO},\{x = 2, y = 2\}), \\
    &\quad&   &M(\text{DO},\{x = 3, y = 3\}) \}
  && \htmlClass{hljs-comment}{\textit{iteration 2 complete}} \\
\\
    &=    &\{ &\{x = 2, y = 1\}, \{x = 3, y = 2\}, \{ x = \frac{1}{3}, y = 1 \}, \bot_d \\
    &\quad&   &\{\{x = 1, y = 1\}\},
  && \htmlClass{hljs-comment}{\textit{all guards false for \{x = 1, y = 1\}}} \\
    &\quad&   &\{M(\text{DO},\{x = \frac{2}{2}, y = 2\}),M(\text{DO},\{x = \frac{2}{2}, y = 2\})\},
  && \htmlClass{hljs-comment}{\textit{$B_3 \land B_4 = T$}} \\
    &\quad&   &\{\{x = 3, y = 3\}\} \},
  && \htmlClass{hljs-comment}{\textit{all guards false for \{x = 3, y = 3\}}} \\

    &=    &\{ &\{x = 2, y = 1\}, \{x = 3, y = 2\}, \{ x = \frac{1}{3}, y = 1 \}, \bot_d
  && \htmlClass{hljs-comment}{\textit{flatten \& deduplicate}} \\
    &\quad&   &\{x = 1, y = 1\}, \{x = 3, y = 3\}, \\
    &\quad&   &M(\text{DO},\{x = 1, y = 2\}), \\
    &\quad&   &M(\text{DO},\{x = 1, y = 2\}) \}
  && \htmlClass{hljs-comment}{\textit{iteration 3 complete}} \\
\\
    &=    &\{ &\{x = 2, y = 1\}, \{x = 3, y = 2\}, \{ x = \frac{1}{3}, y = 1 \}, \bot_d \\
    &\quad&   &\{x = 1, y = 1\}, \{x = 3, y = 3\}, \\
    &\quad&   &\{x = 1, y = 2\} \} \space_\blacksquare
  && \htmlClass{hljs-comment}{\textit{all guards false for \{ x = 1, y =2 \}}} \\
\end{aligned}
$$

<section>

### part (b)

:::{.question}

> Let 𝐼𝐹 ≡ 𝐢𝐟 𝑥 > 𝑦 → 𝑥 ≔𝑥−1 ◻𝑥 >𝑦→𝑦≔𝑦+1 ◻𝑥+𝑦=4→𝑥≔𝑦/𝑥 ◻𝑥+𝑦=4→𝑥≔ 𝑥/𝑦 𝐟𝐢, \
> and let 𝜎<sub>2</sub>(𝑥) = 𝜎<sub>2</sub>(𝑦) = <sub>2</sub>. \
> Calculate 𝑀(𝐼𝐹,𝜎<sub>2</sub>) and show your work.

:::

$$
\begin{aligned}
&     &M&(\text{IF}, \{x = 2, y = 2\})                \\
\\
&=    &\{ &\{\bot_e\},                     && \htmlClass{hljs-comment}{\textit{$\sigma_2(B_1) = F$}} \\
&\quad&   &\{\bot_e\},                     && \htmlClass{hljs-comment}{\textit{$\sigma_2(B_2) = T$}} \\
&\quad&   &M(x:= y/x, \{x = 2, y = 2\}),   && \htmlClass{hljs-comment}{\textit{$\sigma_2(B_3) = T$}} \\
&\quad&   &M(x:= x/y, \{x = 2, y = 2\}) \} && \htmlClass{hljs-comment}{\textit{$\sigma_2(B_4) = T$}} \\
&     &   &
  && \htmlClass{hljs-comment}{\textit{by (2.1)}} \\
\\
&=    &\{ &\bot_e, \{x = 1, y = 2\} \} \space_\blacksquare
  && \htmlClass{hljs-comment}{\textit{flatten \& deduplicate}} \\
\end{aligned}
$$

</section>
</section>
<section>

## Question 3

:::{.question}

> Decide true or false for each of the following statements, justify your
> answers briefly.

:::

<section>

### part (a)

:::{.question}

> If 𝑀(𝑆,𝜎) contains exactly one state, then 𝑆 is a deterministic statement.

:::

False, `if - fi` can have 2 or more branches that can evaluate to the same state.

</section>
<section>

### part (b)

:::{.question}

> If 𝜎 ⊭ {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ 𝑝.

:::

False, while $\sigma \not \models_\text{tot} \{p\} S \{q\} \implies \sigma \models_\text{tot} p$,
this partially correct version has additional possible reasons that $\sigma$
does not satisfy the triple, including that the S terminates in $\bot$.

</section>
<section>

### part (c)

:::{.question}

> If 𝜎 ⊨<sub>𝑡𝑜𝑡</sub> {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ 𝑝.

:::

False, for example the
statement $\{x = -5\} \models_\text{tot} \{x > 0\} x\coloneqq x + 1 \{x > 0\}$
is True, because $\{x = -5\} \not \models \{x > 0\}$.

</section>
<section>

### part (d)

:::{.question}

> If 𝜎 ⊨ {𝑝} 𝑆 {𝑞}, then 𝑀(𝑆,𝜎) ⊨ 𝑞.

:::

False, if $\bot \in M(S,\sigma)$, then $M(S,\sigma) \not \models q$.

</section>
<section>

### part (e)

:::{.question}

> If 𝜎 ⊨<sub>𝑡𝑜𝑡</sub> {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ {𝑝} 𝑆 {𝑞}.

:::

True, because $(M(S,\sigma) - \bot) \subseteq M(S,\sigma)$.

</section>
</section>
<section>

## Question 4

:::{.question}

> Answer the following questions about possible values of variable 𝑥 in a
> state. Justify your answer briefly.

:::

<section>

### part (a)

:::{.question}

> Let ⊥<sub>𝑒</sub> ∉ 𝑀(𝑆,𝜎), where 𝑆 ≡ 𝑥 ∶= 𝑠𝑞𝑟𝑡(𝑥) / 𝑏[𝑥] and 𝜎(𝑏) = (3,0,−2,4). What are
> the possible values of 𝜎(𝑥)?

:::

- because any value for x below 0 or above 3 would cause the expression $b[x]$ to evaluate
  to $\bot_e$ for index out of bounds, we know $x \in [0,3]$.
- additionally, if $x = 1$, then $b[x] = 0$, which means that $\text{sqrt}(x) / b[x]$ would
  evaluate to $\bot_e$ as well for division by zero.

these two conditions mean that $\sigma(x) \in \{0, 2, 3\}$.

</section>
<section>

### part (b)

:::{.question}

> Let ⊥<sub>𝑒</sub> ∉ 𝑀(𝑆,𝜎), where 𝑆 ≡ 𝐢𝐟 𝑥 > 4 → 𝑦 ≔ 1/𝑥 □ 𝑥 < 1 → 𝑦 ≔ 𝑠𝑞𝑟𝑡(𝑥) 𝐟𝐢 . What
> are the possible values of 𝜎(𝑥)?

:::

assuming $\text{sqrt}(x)$ evaluates to $\bot_e$ for any $x < 0$, then the second branch of $S$ requires $x = 0$ as the only valid value for that branch. additionally, neither branch changes the value of $x$.

as such, the possible values are $x = 0 \land x > 1$.

</section>
<section>

### part (c)

:::{.question}

> Let 𝜎 ⊨ {𝑠𝑞𝑟𝑡(𝑥) ≠ 1} 𝑥 ≔ 1/𝑥 {𝐹}. What are the possible values of 𝜎(𝑥)?

:::

because this is only _partial_ correctness
, $M(x \coloneqq 1/x,\sigma) - \bot = \empty$ when $\sigma(x) = 0$, which
satisfies any postcondition (including `{F}`).

</section>
<section>

### part (d)

:::{.question}

> Let 𝜎 ⊨ {𝑥 ≠ 0} 𝐰𝐡𝐢𝐥𝐞 𝑥 ≠ 0 𝐝𝐨 𝑥 ≔ 𝑥−2 𝐨𝐝 {𝑥 < 0}, what are the possible
> values of 𝜎(𝑥)?

:::

- $\sigma(x) = 0$ means $\sigma$ satisfies because the precondition $\{x \neq 0\}$ is not satisfied
- additionally, $\sigma(x) < 0$ would give $M(S,\sigma) = \bot$, which satisfies the triple under
  partial correctness
- finally, $sigma(x) = 1$ would give an end state such that $\sigma(x) = -1$, satisfying the
  postcondition as well

these together mean $x \in (-\infin,1]$.

</section>
</section>
