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

|              | 𝜎[𝑢 ↦𝛼][𝑣 ↦𝛽] = 𝜎[𝑣 ↦𝛽][𝑢↦𝛼]? | 𝜎[𝑢 ↦𝛼][𝑣 ↦𝛽] ≡ 𝜎[𝑣 ↦𝛽][𝑢↦𝛼]? |
| ------------ | ----------------------------- | ----------------------------- |
| 𝑢 ≡ 𝑣, 𝛼 = 𝛽 |                               |                               |
| 𝑢 ≡ 𝑣, 𝛼 ≠ 𝛽 |                               |                               |
| 𝑢 ≢ 𝑣, 𝛼 = 𝛽 |                               |                               |
| 𝑢 ≢ 𝑣, 𝛼 ≠ 𝛽 |                               |                               |

:::

## Question 2

:::{.question}

> Consider state 𝜎 = {𝑥 = 1, 𝑦 = 2, 𝑝 =𝑇, 𝑏 =(2,5,4,8)}. Answer the
> following questions and justify your answers briefly.

:::

### part a

:::{.question}

> What is the evaluation of expression 𝐢𝐟 𝑏[𝑥]> 𝑦 𝐭𝐡𝐞𝐧 𝑝 𝐞𝐥𝐬𝐞 𝑥 < 𝑦 𝐟𝐢
> in state 𝜎?

:::

### part b

:::{.question}

> What is state 𝜎[𝑥 ↦ 𝜎(𝑦−2)][𝑝↦ 𝜎(𝑦 < 𝑥)]?

:::

### part c

:::{.question}

> Let 𝜏 = 𝜎[𝑥 ↦𝜎(𝑏[𝑦])], and 𝛾 = 𝜏[𝑦 ↦ 𝜏(𝑥)∗3]. What is state 𝛾?

:::

### part d

:::{.question}

> Is it true that 𝜎 ⊨ ∀𝑥.𝑥 < 3 →𝑦 ≥2 ?

:::

### part e

:::{.question}

> Is it true that 𝜎 ⊨ 𝑥 ≥ 1∧∃0 ≤ 𝑥 <4.𝑏[𝑥] <3 ?

:::
