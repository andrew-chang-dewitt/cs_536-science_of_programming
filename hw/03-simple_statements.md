:::hgroup{.titlegroup}

# assignment 3

Andrew Chang-DeWitt \
Feb. 13, 2026 \
CS 536

:::

## Question 1

:::{.question}

> Translate the following Java programs into statements in our programming language.

:::

<section>

### part (a)

:::{.question}

> `int x = 0; for (int i = 0; i < b.length; i++) { x += b[i]; }`

:::

$$
\begin{aligned}
x \coloneqq 0;\space
i \coloneqq 0;\space
\text{while}\space
i < \text{size}(b)
\space\text{do}\space
x \coloneqq x + b[i];\space
i \coloneqq i + 1
\space\text{od}\space
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> `while (x != 1) {if (x % 2 == 0) { x = x/2; } else { x++; }}`

<!--
   while B do if B' then S else S' fi od
-->

:::

$$
\begin{aligned}
\text{while}\space
x \neq 1 \space
\text{do}\space
\text{if}\space
x \% 2 = 0 \space
\text{then}\space
x \coloneqq x / 2 \space
\text{else}\space
x \coloneqq x + 1 \space
\text{fi}\space
\text{od}\space
\end{aligned}
$$

</section>
<section>

## Question 2

:::{.question}

> Evaluate each of the following configurations to completion (in other words,
> show operational semantics). Do not use →∗ or →𝑛 (but only → while
> evaluation) in your solutions.

:::

<section>

### part (a)

:::{.question}

> ⟨𝐢𝐟 𝑥 < 2 𝐭𝐡𝐞𝐧 𝑥 ≔ 𝑦 + 1; 𝑤 ≔ 𝑥 + 2 𝐟𝐢, 𝜎⟩, where 𝜎(𝑥) = 𝜎(𝑦) = 3 and 𝜎(𝑤) = 4

:::

$$
\begin{aligned}
&\lang
    \text{if}\space
        x < 2 \space
    \text{then}\space
        x \coloneqq y + 1; \space
        w \coloneqq x + 2 \space
    \text{fi}, \space
    \{ x = 3, y = 3, w = 4 \}
\rang \\
&\quad\quad\quad \longrightarrow \lang
    skip, \space
    \{ x = 3, y = 3, w = 4 \}
\rang &&
\htmlClass{hljs-comment}{\textit{// $\sigma$(x) = 3 > 2}} \\
&\quad\quad\quad \longrightarrow \lang
    E, \space
    \{ x = 3, y = 3, w = 4 \}
\rang
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> ⟨𝑥 ≔ 𝑦 + 1; 𝑦 ≔ 𝑥 + 1, 𝜎⟩. Here, variables 𝑥 and 𝑦 are both defined in state 𝜎

:::

$$
\begin{aligned}
&\lang
    x \coloneqq y + 1; \space
    y \coloneqq x + 1, \space
    \{ x = 3, y = 3, w = 4 \}
\rang \\
&\quad\quad\quad \longrightarrow \lang
    y \coloneqq x + 1, \space
    \{ x = 4, y = 3, w = 4 \}
\rang &&
\htmlClass{hljs-comment}{\textit{// $\sigma$[x $\mapsto$ $\sigma$(y + 1)]}} \\
&\quad\quad\quad \longrightarrow \lang
    E, \space
    \{ x = 4, y = 5, w = 4 \}
\rang &&
\htmlClass{hljs-comment}{\textit{// $\sigma$[y $\mapsto$ $\sigma$(x + 1)]}} \\
\end{aligned}
$$

</section>
</section>
<section>

## Question 3

:::{.question}

> Let 𝑊 ≡ 𝐰𝐡𝐢𝐥𝐞 𝑥 < 3 𝐝𝐨 𝑆 𝐨𝐝, where 𝑆 ≡ 𝑥 ≔ 𝑥 + 2; 𝑝 ≔ 𝑝 ∧ (𝑥 > 1). Calculate
> the following denotational semantics

:::

<section>

### part (a)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>1</sub>), where 𝜎<sub>1</sub>(𝑥) = 4 and 𝜎<sub>1</sub>(𝑝) = T

:::

$$
\begin{aligned}
M(W,\sigma_1) &\longrightarrow \{ \sigma_1 \} && \htmlClass{hljs-comment}{\textit{// B is false, $\sigma$(x) = 4 < 3}} \\
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>2</sub>), where 𝜎<sub>2</sub> ⊨ (𝑥 = 1) ∧ 𝑝

:::

$$
\begin{aligned}
\sigma_2 \models (x = 1) \land p &\iff (\sigma_2(x) = 1) \land \sigma_2(p) \\
                                 &\implies \{ x = 1, p = T \} \subseteq \sigma_2 \\
\\
M(W,\sigma_2)           &\longrightarrow^0 M(W,\{ x = 1, p = T \})
                             && \htmlClass{hljs-comment}{\textit{since $W$ is in terms of $x$ \& $p$, this}} \\
                        &    && \htmlClass{hljs-comment}{\textit{is a good enough definition of $\sigma_2$}} \\
                        &\longrightarrow M(S,\{ x = 1, p = T \})
                             && \htmlClass{hljs-comment}{\textit{// B is true, $\sigma_2$(x) = 1 < 3}} \\
                        &\longrightarrow M(p \coloneqq p \land (x > 1),\{ x = 3, p = T \})
                             && \htmlClass{hljs-comment}{\textit{// $\sigma_2$[x $\mapsto$ $\sigma_2$(x) + 2]}} \\
                        &\longrightarrow \{\{ x = 3, p = T \}\}
                             && \htmlClass{hljs-comment}{\textit{// $\sigma_2$[p $\mapsto$ T $\land$ (3 > 1)]}} \\
\end{aligned}
$$

</section>
</section>
<section>

## Question 4

:::{.question}

> Let 𝑊 ≡ 𝐰𝐡𝐢𝐥𝐞 𝑥 > 0 𝐝𝐨 𝑆 𝐨𝐝, where 𝑆 ≡ 𝐢𝐟 𝑥 < 𝑦 𝐭𝐡𝐞𝐧 𝑥 ≔ 𝑦/𝑥 𝐞𝐥𝐬𝐞 𝑥 ≔ 𝑥 − 1; 𝑦 ≔ 𝑏[𝑦] 𝐟𝐢.
> Calculate the following denotational semantics.

:::

<section>

### part (a)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>1</sub>), where 𝜎<sub>1</sub> = {𝑥 = 2, 𝑦 = 2, 𝑏 = (0,1,2)}.

:::

$$
\begin{aligned}
M(W,\sigma_1)
    &\longrightarrow^0 M(W,\{ x = 2, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(S;W,\{ x = 2, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(x \coloneqq x - 1; y \coloneqq b[y];W,\{ x = 2, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(y \coloneqq b[y];W,\{ x = 1, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(W,\{ x = 1, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(S;W,\{ x = 1, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(x \coloneqq y / x;W,\{ x = 1, y = 2, b = (0,1,2) \}) \\
    &\longrightarrow   M(W,\{ x = 2, y = 2, b = (0,1,2) \}) && \htmlClass{hljs-comment}{\textit{// back to where we started}} \\
    &\longrightarrow^* M(W,\sigma_1) && \htmlClass{hljs-comment}{\textit{// this is a cycle}} \\
    &\longrightarrow^* \{ \bot_d \} \space_\blacksquare && \htmlClass{hljs-comment}{\textit{// diverges}}
\end{aligned}
$$

</section>
<section>

### part (b)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>2</sub>), where 𝜎<sub>2</sub> = {𝑥 = 8, 𝑦 = 2, 𝑏 = (4,2,0)}

:::

$$
\begin{aligned}
M(W,\sigma_2)
    &\longrightarrow^0 M(W,\{ x = 8, y = 2, b = (4,2,0) \}) \\
    &\longrightarrow   M(S;W,\{ x = 8, y = 2, b = (4,2,0) \}) \\
    &\longrightarrow   M(x \coloneqq x - 1; y \coloneqq b[y];W,\{ x = 8, y = 2, b = (4,2,0) \}) \\
    &\longrightarrow   M(y \coloneqq b[y];W,\{ x = 7, y = 2, b = (4,2,0) \}) \\
    &\longrightarrow   M(W,\{ x = 7, y = 0, b = (4,2,0) \}) \\
    &\longrightarrow   M(S;W,\{ x = 7, y = 0, b = (4,2,0) \}) \\
    &\longrightarrow   M(x \coloneqq x - 1; y \coloneqq b[y];W,\{ x = 7, y = 0, b = (4,2,0) \}) \\
    &\longrightarrow   M(y \coloneqq b[y];W,\{ x = 6, y = 0, b = (4,2,0) \}) \\
    &\longrightarrow   M(W,\{ x = 6, y = 4, b = (4,2,0) \}) \\
    &\longrightarrow   M(S;W,\{ x = 6, y = 4, b = (4,2,0) \}) \\
    &\longrightarrow   M(x \coloneqq x - 1; y \coloneqq b[y];W,\{ x = 6, y = 4, b = (4,2,0) \}) \\
    &\longrightarrow   M(y \coloneqq b[y];W,\{ x = 5, y = 4, b = (4,2,0) \}) && \htmlClass{hljs-comment}{\textit{// $\sigma$(b[4]) -> out of bounds}} \\
    &\longrightarrow   \{ \bot_e \} \space_\blacksquare && \htmlClass{hljs-comment}{\textit{// hereditary failure}}\\
\end{aligned}
$$

</section>
</section>
