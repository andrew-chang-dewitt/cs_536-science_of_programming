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

<section>

### part (a)

:::{.question}

> Let 𝐷𝑂 ≡ 𝐝𝐨 𝑥 >𝑦 →𝑥 ≔𝑥−1 ◻𝑥>𝑦→𝑦≔𝑦+1 ◻𝑥+𝑦=4→𝑥≔𝑦/𝑥 ◻𝑥+𝑦=4→𝑥≔ 𝑥/𝑦 𝐨𝐝, and let
> 𝜎<sub>1</sub> = {𝑥 = 3, 𝑦 = 1}. Calculate 𝑀(𝐷𝑂,𝜎<sub>1</sub>) and show your
> work.

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> Let 𝐼𝐹 ≡ 𝐢𝐟 𝑥 > 𝑦 → 𝑥 ≔𝑥−1 ◻𝑥 >𝑦→𝑦≔𝑦+1 ◻𝑥+𝑦=4→𝑥≔𝑦/𝑥 ◻𝑥+𝑦=4→𝑥≔ 𝑥/𝑦 𝐟𝐢, and let
> 𝜎2(𝑥) = 𝜎2(𝑦) = 2. Calculate 𝑀(𝐼𝐹,𝜎2) and show your work.

:::

$$
\begin{aligned}
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

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> If 𝜎 ⊭ {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ 𝑝.

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (c)

:::{.question}

> If 𝜎 ⊨𝑡𝑜𝑡 {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ 𝑝.

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (d)

:::{.question}

> If 𝜎 ⊨ {𝑝} 𝑆 {𝑞}, then 𝑀(𝑆,𝜎) ⊨ 𝑞.

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (e)

:::{.question}

> If 𝜎 ⊨𝑡𝑜𝑡 {𝑝} 𝑆 {𝑞}, then 𝜎 ⊨ {𝑝} 𝑆 {𝑞}.

:::

$$
\begin{aligned}
\end{aligned}
$$

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

> Let ⊥𝑒∉ 𝑀(𝑆,𝜎), where 𝑆 ≡ 𝑥 ∶= 𝑠𝑞𝑟𝑡(𝑥) / 𝑏[𝑥] and 𝜎(𝑏) = (3,0,−2,4). What are
> the possible values of 𝜎(𝑥)?

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> Let ⊥𝑒∉ 𝑀(𝑆,𝜎), where 𝑆 ≡ 𝐢𝐟 𝑥 > 4 → 𝑦 ≔ 1/𝑥 □ 𝑥 < 1 → 𝑦 ≔ 𝑠𝑞𝑟𝑡(𝑥) 𝐟𝐢 . What
> are the possible values of 𝜎(𝑥)?

:::

$$
\begin{aligned}
\end{aligned}
$$

</section>
<section>

### part (c)

:::{.question}

> Let 𝜎 ⊨ {𝑠𝑞𝑟𝑡(𝑥) ≠ 1} 𝑥 ≔ 1/𝑥 {𝐹}. What are the possible values of 𝜎(𝑥)?
>
> :::

$$
\begin{aligned}
\end{aligned}


$$

</section>
<section>

### part (d)

:::{.question}

> Let 𝜎 ⊨ {𝑥 ≠ 0} 𝐰𝐡𝐢𝐥𝐞 𝑥 ≠ 0 𝐝𝐨 𝑥 ≔ 𝑥−2 𝐨𝐝 {𝑥 <0}, what are the possible
> values of 𝜎(𝑥)?

:::

$$

\begin{aligned}
\end{aligned}


$$

</section>
</section>
$$
