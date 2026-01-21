:::hgroup{.titlegroup}

# assignment 1

Andrew Chang-DeWitt \
Jan. 21, 2026 \
CS 536

:::

## Question 1

1. Decide true or false for each of the following statements. Justify your answers briefly. Variables 𝑝 and 𝑞 used 
here are propositional variables. 
   a. {𝑥 = 2, 𝑝 = 𝑇} ⊨ 𝑥 > 2 ∨ 𝑝. 
   b. {𝑥 = 2, 𝑝 = 2, 𝑝 = 𝑇} is a well-formed state.
   c. Any state is proper for 𝐹 → 𝑝.
   d. ⊨ 𝑝 → 𝑝 → 𝑝 ∨ 𝑞
   e. ⊭ 𝑝 ∨ ¬𝑝

2. Let 𝑝1 and 𝑝2 be two propositions or predicates.
   a. Does 𝑝1 ⇔ 𝑝2 logically imply 𝑝₁ ≡ 𝑝₂? If yes, briefly justify your answer; if not, give a counterexample.
   b. Does 𝑝1 ↔ 𝑝2 ⇔ 𝐹 logically imply 𝑝1 ≢ 𝑝2? If yes, briefly justify your answer; if not, give a counterexample.

3. Prove the following logical equivalences. You can either use Truth Tables or the rules provided in Lecture 2 to 
prove them. 
   a. ¬(𝑝 ↔ 𝑞) ⇔ ¬𝑝 ↔ 𝑞
   b. (𝑝 → 𝑞) ∧ (¬𝑝 → 𝑞) ⇔ 𝑞

4. Define the following predicate functions.
   a. Define a predicate function 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 𝑛) which is 𝑇𝑟𝑢𝑒 if and only if the first 𝑛 elements of 
integer array 𝑏 is sorted in the reversed order, in other word, 𝑏[0] ≥ 𝑏[1] ≥ 𝑏[2] ≥ ⋯ ≥ 𝑏[𝑛 − 1]. You 
may assume that array 𝑏 has at least 𝑛 elements and 𝑛 is positive, so you don’t need to worry about the 
domain of 𝑛. For example, if 𝑏 = (4, 3, 4, 3), then 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 1) is 𝑇𝑟𝑢𝑒, 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 2)
is 𝑇𝑟𝑢𝑒 but 𝑅𝑒𝑣𝑒𝑟𝑠𝑒𝑑𝑆𝑜𝑟𝑡𝑒𝑑(𝑏, 3) is 𝐹𝑎𝑙𝑠𝑒.
   b. Define a predicate function 𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 𝑚) which is 𝑇𝑟𝑢𝑒 if and only if the first 𝑚 elements of integer 
array 𝑏 match the second 𝑚 elements of 𝑏, in other word, 𝑏[0] = 𝑏[𝑚], 𝑏[1] = 𝑏[𝑚 + 1],…, 𝑏[𝑚 − 1] =
𝑏[2 ∗ 𝑚 − 1]. You may assume that 𝑚 is positive and 2 ∗ 𝑚 − 1 is less than length array 𝑏, so you don’t 
need to worry about the domain of 𝑚. For example, if 𝑏 = (1, 3, 5, 1, 3, 5), then 𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 3) is 𝑇𝑟𝑢𝑒 but 
𝑅𝑒𝑝𝑒𝑎𝑡𝑠(𝑏, 2) is 𝐹𝑎𝑙𝑠