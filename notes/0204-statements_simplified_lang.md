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
program     <p> ::= <s> | <s> ";" <p>  // a sequence of statements

statement   <s> ::= <k> | <a> | <i> | <w>

no-op       <k> ::= "skip"
assignment  <a> ::= <id> ":=" <e>  // some id bound to an expr
conditional <i> ::= "if" <e> "then" <s> "else" <s> "fi" | "if" <e> "then" <s> "fi"  // elide the else if statement is skip
iteration   <w> ::= "while" <e> "do" <s> "od"
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

if there is a sequence of configurations $\lang S, \sigma \rang \rarr \dots \rarr \lang E, \tau \rang$ (where $E$ means end of program), we say

> execution of $S$ starting in state $\sigma$ _**converges**_ to (or
> terminates in) state $\tau$

we define the operational semantics of our program statements by
starting with the axiomatic ones: skip, assignment, conditional, &
while statements. sequences, however, are slightly trickier, as we'll
see below.
