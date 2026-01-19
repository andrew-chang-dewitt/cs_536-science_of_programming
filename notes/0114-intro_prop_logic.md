---
title: "Program verification: intro & review of propositional logic"
description: "Day 1 lecture notes covering logistics, expectations, & a brief review of propositional logic."
keywords:
  - "program verification"
  - "propositional logic"
  - "lecture notes"
  - "computer science"
  - "cs 536"
  - "illinois tech"
meta:
  byline: Andrew Chang-DeWitt
  published: "2026-01-14T10:00-06:00"
---

> [!NOTE]
>
> for my purposes, I'll be collecting all course materials (including
> these notes) at a single git repository, made available on GitHub at
> [https://github.com/andrew-chang-dewitt/cs_536-science_of_programming](https://github.com/andrew-chang-dewitt/cs_536-science_of_programming).

## agenda

- administrivia
  - outcomes
  - grading
  - policies
- what we'll cover
  - difference between verification & testing/debugging
  - a simple example
- review of propositional logic
  - definitions
  - operators
  - some examples

## administrivia

### outcomes

at the end of the course, should be able to answer the following questions:

> 1. How does verification differ from testing?
> 2. How do we understand the semantics of programs?
> 3. How do semantics affect the way we understand the correctness of
>    the program?
> 4. What rules of reasoning can we use to discuss the correctness of
>    the program?
> 5. How is the correctness of parallel programs different?
> 6. What if program execution is not deterministic?

### grading

scale:

while a grading scale is not set in stone, it is set so as to allow for
the top 25% of scores to achieve an A. typically, it looks like the
following & sometimes it ends up w/ bottoms of each grade letter
getting lowered (almost never higher):

- 80% A
- 65% B

historically, students only fail the course if they cheat or otherwise
violate academic integrity policies.

categories:

- 40% assignments (10 @ 4% each)
- 34% midterms exam (2 @ 17% each)
- 26% final exam

#### assignments

there will be 12 assignments w/ the lowest 2 grades dropped. questions
asked on the assignments will be similar to those asked later on exams.

to be submitted on Canvas before deadline.

#### exams

in-person, closed-book, closed-notes, & no electronic devices. 1 A4-sized, double-sided cheat sheet is allowed for each midterm. 3 double-sided sheets are allowed for the final.

exams will be composed of multiple choice & short answer questions similar to class examples & assignments.

### policies

#### late policy

20% penalty per day for each day after the deadline. it is _highly_
recommended to reach out to prof _before_ the deadline to discuss
extensions.

## what we'll cover

this course is titled _Science of Programming_, which boils down to one
core topic: **program verification**. _**def:**_ use logical reasoning
to prove that a program does what is intended using properties of the
program & its environment.

we'll use a simplified programming language w/ very simple syntax to
allow us to focus our efforts on the reasoning about program semantics
& less about proram syntax.

### difference between verification & testing/debugging

software testing is often used to achieve similar goals, but it has
some key differences from program verification:

- testing/debugging is done _after_ program creation/writing/compiling; program verification can happen even _before_ any code is written as a way of helping to write your code
- testing/debugging can be very time consuming
- testing can only prove correctness if there are test cases covering all possible situations; this can be an impossibly large set & it is very easy to miss edge cases
- program verification can miss edge cases when the rules/reasoning used are too strict & don't align w/ the reality the program executes in

### a simple example

given the program statement "add integer `x` to `z`, if `x` is positive" & the knowledge that the variable `z` is greater than or equal to some constant `c` before this statement, what can we expect of `z` after the statement? how to test this?

after execution, `z` should still be greater than or equal to `c`.

we can prove this by reasoning about the possible values for `z` & `x` relative to `c` & `0` at each stage of the program:

$$
\begin{aligned}
(1) && \because   && z_i &\geq c && \textit{z starts as $\geq$ c} \\
    && \\
    &&            && x_l &\leq 0 && \textit{two ranges of possible values} \\
    &&            && x_g &> 0 \\
    && \\
    &&            && x_l &\longrightarrow \text{if skipped} \\
(2) &&            && z_f &\equiv z_i \\
    && \\
    &&            && x_g &\longrightarrow z_f = z_i + x_g \\
    &&            && z_f &= z_i + \text{value $\geq$ 0} \\
(3) &&            && z_f &\geq zi \\
\\
    &&            && (2) &\land (3) \longrightarrow z_f \geq z_i && \textit{z can only increase or not change} \\
    && \therefore && (1) &\longrightarrow z_f \geq c \space\blacksquare \\
\end{aligned}
$$

## review of propositional logic

### definitions

- _**logic**_&mdash;the study of formal or valid reasoning
- _**propostion**_&mdash;a declarative sentence that is either true or false
- _**propostional logic**_&mdash;logic over _**propositional variables**_ (expressed as letters `p`, `q`, `r`, ...) which represent propositions

### operators

logic is formed w/ _**propositional operators**_, or conjunctions:

- and ( $\land$ )
- or ( $\lor$ )
- not ( $\neg$ )
- implication ( $\longrightarrow$ )
- biconditional ( $\longleftrightarrow$ )

### some examples

#### ex: what is a propostion

:::{.question}

> which of the following are propositions?
>
> 1. IIT was founded in 1940
> 2. Do you have any siblings?
> 3. Please log on to myIIT with your hawk credentials

only (1) is a propostion; (2) is a question (propositions must be assertions) & (3) is not an assertion

:::

#### ex: translating prose to logic

:::{.question}

> with the propositions
> &Tab;`p`: it is below freezing&Tab;`q`: it is snowing
> represent the following propositions using `p`, `q`, & logical connectives
>
> 1. It is below freezeing & snowing
> 2. it is below freezing but not snowing
> 3. It is not below freezing, and it is not snowing
> 4. It is either snowing or below freezing (or both)

1. $p \land q$
2. $p \land \neg q$
3. $\neg p \land \neg q$
4. $p \lor q$

:::

#### ex: translating conditionals to implications

:::{.question}

> translate each of the following to either $p \longrightarrow q$ or $q \longrightarrow p$:
>
> 1. if `p` then `q`
> 2. `p` is suffient for `q`
> 3. `p` if `q`
> 4. `p` is necessary for `q`
> 5. `p` only if `q`

:::

1. $p \longrightarrow q$
2. $p \longrightarrow q$
3. $q \longrightarrow p$
4. $q \longrightarrow p$
5. $p \longrightarrow q$
