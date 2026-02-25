propositions

- law of contrapositive: $p \rarr q \iff \neg q \rarr p$
- definition of implication: $p \rarr q \iff \neg p \lor q$
- negation of implication: $\neg (p \rarr q) \iff p \lor q$
- definition of biconditional: $(p \leftrightarrow q) \iff (p \rarr q) \land (q \rarr p)$
- commutativity: $p \lor  q \iff q \lor  p$ and $p \land q \iff q \land q$
- associativity: $(p \lor q) \lor r \iff p \lor (q \lor r)$ and $(p \land q) \land r \iff p \land (q \land r)$
- distributivity: $(p \lor q) \land r \iff (p \land r) \lor (q \land r)$ and $(p \land q) \lor r \iff (p \lor r) \land (q \lor r)$
- identity: $p \land T \iff p$ and $p \lor  F \iff p$
- idempotency: $p \lor  p \iff p$ and $p \land p \iff p$
- domination: $p \lor  T \iff T$ and $p \land F \iff F$
- absurdity: $(F \rarr p) \iff T$
- contradiction: $p \land \neg p \iff F$
- excluded middle: $p \lor \neg p \iff T$
- double negation: $\neg \neg p \iff p$
- DeMorgan's laws: $\neg (p \land q) \iff (\neg p \lor  \neg q)$ and $\neg (p \lor  q) \iff (\neg p \land \neg q)$
- transitivity: $(p \rarr q) \land (q \rarr r) \implies (p \rarr r)$ and $(p \leftrightarrow q) \land (q \leftrightarrow r) \implies (p \leftrightarrow r)$
- Modus Ponens: $(p \rarr q) \land p \implies q$
- Modus Tollens: $(p \rarr q) \land \neg q \implies \neg p$
- or-introduction (and-elimination): $p \implies p \lor q$ ("I had dinner" logically implies "I had dinner or lunch") or $p \land q \implies p$ ("I had dinner & lunch" logically implies "I had dinner")
- or-elimination: $(p \lor q) \land (p \rarr r) \land (q \rarr r) \implies r$

predicates & quantifiers

- universal quantifier: has form $\forall x \in S$, where $S$ is a set of values. can be used to create a _universally quantified predicate_ e.g. $\forall x \in S.p$, where $S$ is a set & $p$ is a predicate involving $x$.
- existential quantifier: has form $\exist x \in S$, w/ predicate form $\exist x \in S.p$
- bounded quantifier: $\forall p.q$ means $\forall x.p \longrightarrow q$
  where $x$ appears in $p$ & $x$ is understood to be
  the variable we are quantifying over. similarly, $\exist p.q$ means $\exist x.p \land q$
  where $x$ appears in $p$ & $x$ is understood to be the variable we are quantifying over.
- predicate version of **DeMorgan's Law**: $\neg \forall x.p \iff (\exist  x.\neg p)$ & $(\neg \exist  x.p) \iff (\forall x.\neg p)$
- properness & satisfaction of quantified predicates: recall, a variable $v$ in some predicate is a _free occurrence_ of $v$ if it is not within the scope of a quantifier over $v$. that means, a variable $v$ is considered to be _**free**_ in predicate $p$ iff it has a free occurrence in $p$. conversely, $v$ is _**bound**_ in $p$ iff it has a bound occurrence in $p$.
- validity of predicates: $(\models p) \iff (\forall \sigma \in S.\sigma \models p)$ where $S \;\text{is the collection of all proper states for } p$

bottom

- divergence:
  1. in iterative statements (i.e. infinite loops) where evaluation yields some sequence $\lang W, \sigma_0 \rang \rarr^* \lang W, \sigma_1 \rang \rarr^* \lang W, \sigma_2 \rang \rarr \dots$ or $\neg \exist i.\sigma_i(e) = F \implies M(W,\sigma) = \{\bot_d\}$.
  2. when there is a cycle in the operational semantic evaluation (i.e. infinite recursion): given some sequence during evaluation $\lang S_0, \sigma_0 \rang \rarr^* \lang S_1, \sigma_1 \rang \rarr^* \lang S_2, \sigma_2 \rang \rarr \dots$, it diverges if $\exist i.\exist j.i \ne j \land S_i = S_j \land \sigma_i = \sigma_j \implies M(S_0,\sigma_0) = \{\bot_d\}$

> [!TODO]
>
> was missing items on...
>
> - validity of a triple
> - total correctness & partial correctness of triples
> - strength of predicates
> - operational & denotational semantics rules for lang statements (including
>   notions of bottom & nondeterministic statements!)
>
> also really need to review (redo by hand?) hw assignments & examples to
> practice
