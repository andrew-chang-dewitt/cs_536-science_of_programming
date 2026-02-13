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

### part (a)

:::{.question}

> `int x = 0; for (int i = 0; i < b.length; i++) { x += b[i]; }`

:::

$$
\begin{aligned}
\end{aligned}
$$

### part (b)

:::{.question}

> `while (x != 1) {if (x % 2 == 0) { x = x/2; } else { x++; }}`

:::

$$
\begin{aligned}
\end{aligned}
$$

## Question 2

:::{.question}

> Evaluate each of the following configurations to completion (in other words,
> show operational semantics). Do not use →∗ or →𝑛 (but only → while
> evaluation) in your solutions.

:::

### part (a)

:::{.question}

> ⟨𝐢𝐟 𝑥 < 2 𝐭𝐡𝐞𝐧 𝑥 ≔ 𝑦 + 1; 𝑤 ≔ 𝑥 + 2 𝐟𝐢, 𝜎⟩, where 𝜎(𝑥) = 𝜎(𝑦) = 3 and 𝜎(𝑤) = 4

:::

$$
\begin{aligned}
\end{aligned}
$$

### part (b)

:::{.question}

> ⟨𝑥 ≔ 𝑦 + 1; 𝑦 ≔ 𝑥 + 1, 𝜎⟩. Here, variables 𝑥 and 𝑦 are both defined in state 𝜎

:::

$$
\begin{aligned}
\end{aligned}
$$

## Question 3

:::{.question}

> Let 𝑊 ≡ 𝐰𝐡𝐢𝐥𝐞 𝑥 < 3 𝐝𝐨 𝑆 𝐨𝐝, where 𝑆 ≡ 𝑥 ≔ 𝑥 + 2; 𝑝 ≔ 𝑝 ∧ (𝑥 > 1). Calculate
> the following denotational semantics

:::

### part (a)

:::{.question}

> Calculate 𝑀(𝑊,𝜎1), where 𝜎1(𝑥) = 4 and 𝜎1(𝑝) = T

:::

$$
\begin{aligned}
\end{aligned}
$$

### part (b)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>2</sub>), where 𝜎<sub>2</sub> ⊨ (𝑥 = 1) ∧ 𝑝

:::

$$
\begin{aligned}
\end{aligned}
$$

## Question 4

:::{.question}

> Let 𝑊 ≡ 𝐰𝐡𝐢𝐥𝐞 𝑥 > 0 𝐝𝐨 𝑆 𝐨𝐝, where 𝑆 ≡ 𝐢𝐟 𝑥 < 𝑦 𝐭𝐡𝐞𝐧 𝑥 ≔ 𝑦/𝑥 𝐞𝐥𝐬𝐞 𝑥 ≔ 𝑥 − 1; 𝑦 ≔ 𝑏[𝑦] 𝐟𝐢.
> Calculate the following denotational semantics.

:::

### part (a)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>1</sub>), where 𝜎<sub>1</sub> = {𝑥 = 2, 𝑦 = 2, 𝑏 = (0,1,2)}.

:::

$$
\begin{aligned}
\end{aligned}
$$

### part (b)

:::{.question}

> Calculate 𝑀(𝑊,𝜎<sub>2</sub>), where 𝜎<sub>2</sub> = {𝑥 = 8, 𝑦 = 2, 𝑏 = (4,2,0)}

:::

$$
\begin{aligned}
\end{aligned}
$$
