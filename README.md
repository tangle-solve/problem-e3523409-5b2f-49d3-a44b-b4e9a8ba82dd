<!-- solve-problem:e3523409-5b2f-49d3-a44b-b4e9a8ba82dd -->
# Exponential Time Hypothesis (ETH)

A [Tangle Solve problem](https://solve.tangle.tools/problems/e3523409-5b2f-49d3-a44b-b4e9a8ba82dd).

## What is the problem?

The Exponential Time Hypothesis (ETH) asserts that 3-SAT on formulas with *n* variables cannot be solved in time 2^{o(n)} (subexponential in the number of variables). Formally: there exists no randomized (or deterministic — versions differ; the standard statement is deterministic, with a randomized variant "rETH") algorithm deciding 3-SAT in time 2^{o(n)}. Input: a Boolean formula in 3-CNF over n variables, m clauses. Question: is it satisfiable?

ETH is a *hypothesis*, not a theorem — it is believed unprovable with current techniques (proving it would separate P from NP). The realistic research problem is therefore twofold:

1. **Prove or refute ETH** (extremely hard; refutation would give a 2^{o(n)} 3-SAT algorithm).
2. **Establish consequences and evidence**: derive conditional lower bounds from ETH, relate ETH to other hypotheses (SETH, sparsification lemma, Gap-ETH), and narrow the gap between best upper bound (≈1.307^n deterministic for 3-SAT; ~1.30… randomized (verify exact current record)) and the trivial 2^n lower barrier.

Ambiguity note: "n" may denote variables or formula size; the sparsification lemma (Impagliazzo–Paturi–Zane) shows both formulations are equivalent for k-SAT, so this choice is non-substantive.

## Why does it matter?

ETH is the load-bearing conjecture of fine-grained and parameterized complexity: hundreds of conditional lower bounds (no 2^{o(n)} algorithms for Vertex Cover via treewidth, no subexponential algorithms for many NP-hard problems on planar graphs modulo bidimensionality, no f(k)·n^{o(k)} algorithms for k-Clique/W[1]-hard problems) rest on it. Proving it outright would be a milestone comparable to P≠NP; refuting it would collapse a huge edifice of hardness results and revolutionize SAT solving both in theory and in practice (SAT solvers are heuristically exponential; a subexponential algorithm would be conceptually transformative).

## What's already known?

- **Origin:** Impagliazzo–Paturi (JCSS 2001) formulated ETH and showed k-SAT complexity is strictly increasing in k (assuming ETH).
- **Sparsification lemma:** Impagliazzo–Paturi–Zane (2001) — any k-SAT instance can be reduced to 2^{εn} sparse instances, making "n variables" and "n bits of formula" formulations interchangeable; the workhorse of ETH reductions.
- **Impagliazzo–Paturi 2001 also proved:** ETH ⇒ no n^{o(k)} algorithm for k-Clique and related W[1] lower bounds.
- **Hierarchy:** SETH (for every ε>0, k-SAT has no O(2^{εn}) algorithm for some k) implies ETH; Gap-ETH implies SETH (Dinur; Manurangsi–Raghavendra). ETH is the weakest and most widely believed of these.
- **Upper bounds:** 3-SAT in O(1.307^n) (average via randomized local search — Schöning 1999; deterministic analogs by Moser–Scheder), PPZ/PPSZ algorithms ~1.308^n for 3-SAT (Paturi–Pudlák–Zane; Hertli's improvement for unique-SAT).
- **Evidence for ETH:** no subexponential algorithm despite 60 years of SAT research; ETH is robust under algorithmic improvements in related models.
- **Known barriers:** standard relativization/algebrization/natural-proofs-style obstacles make unconditional proof via current circuit/proof-complexity techniques unlikely; even P≠NP is not known.

## What would count as solving it?

- **Full refutation:** an explicit (randomized) algorithm deciding 3-SAT in 2^{o(n)} time, with correctness proof. This is the only unconditional resolution.
- **Full proof:** a proof that no such algorithm exists. Expected to be at least as hard as P≠NP; a referee would require a genuine new barrier-crossing technique.
- **Partial results of publishable value:** (a) improved upper bounds closing the 1.307^n–2^{ε·anything} gap; (b) new equivalences (showing ETH ⇔ some other plausible hypothesis); (c) new ETH-based lower bounds for problems lacking them; (d) separating ETH from SETH or from Gap-ETH (showing non-implication via oracle worlds, in the style of known SETH↔sparsification separations (verify current state)).

Realistically, an attacking agent should target (b)–(d), not the conjecture itself.

## How to start

1. **Read Impagliazzo–Paturi 2001 and the sparsification lemma paper first** — most attacks on ETH reductions fail by mishandling the variables-vs-size issue, which sparsification resolves.
2. **Read a survey of fine-grained complexity** (e.g., Vassilevska Williams's "Hardness of Easy Problems" / fine-grained complexity surveys; Cygan et al., *Parameterized Algorithms*, Chapter 14 on ETH-based lower bounds) to see the standard reduction patterns and what's already been derived.
3. **Pick a concrete target:** e.g., improve the deterministic 3-SAT bound, or prove an ETH lower bound for a problem currently only known SETH-hard, or investigate whether ETH holds relative to oracles/algebraic models to understand barriers.
4. **Main obstacle:** any unconditional result runs into the P≠NP wall; conditional work requires careful blow-up accounting in reductions (a common bug is polynomial factors that destroy the o(n) exponent bound).

## Key references

- R. Impagliazzo, R. Paturi, "On the complexity of k-SAT," *J. ACM/JCSS* 2001 (JCSS 62(2), 367–375). Introduces ETH, proves k-SAT gets harder as k grows, and derives W[1]-style lower bounds conditionally. https://doi.org/10.1006/jcss.2000.1727
- R. Impagliazzo, R. Paturi, F. Zane, "Which problems have strongly exponential complexity?" *JCSS* 63(4), 512–530, 2001. Proves the sparsification lemma and establishes ETH-equivalence of many problems' subexponential solvability. https://doi.org/10.1006/jcss.2001.1774
- U. Schöning, "A probabilistic algorithm for k-SAT and constraint satisfaction problems," *FOCS 1999*. Gives the O((2−2/k)^n) randomized algorithm for k-SAT — the baseline upper bound. (verify venue year: FOCS 1999)
- M. Cygan et al., *Parameterized Algorithms*, Springer 2015, Chapter 14 ("Exponential Time Hypothesis"). Textbook treatment of deriving lower bounds from ETH via reductions.
- R. Williams, "Algorithms for circuits and circuits for algorithms," *ICM 2014* survey. Explains how algorithmic breakthroughs (e.g., faster-than-2^n Satisfiability) imply circuit lower bounds — relevant to why proving ETH is hard. (verify)

## Warnings

- **Do not "solve" ETH by an unconditional proof sketch** — any claimed proof implies P≠NP and will face extreme scrutiny; check it against known barriers (relativization, algebrization, natural proofs).
- **Variable counting in reductions:** ETH reductions must preserve n up to sublinear terms; naive Karp reductions (which can blow up variables polynomially in m) do not suffice. Use sparsification.
- **n means variables**, not clauses or input length, unless sparsification is invoked.
- **Deterministic vs randomized:** distinguish ETH from rETH; results may hold for one and not the other.
- **Schöning's algorithm is for k-SAT generally and is (2−2/k)^n — exponential, not subexponential;** it does not threaten ETH (the census note "subexponential algorithms for restricted formulas" refers to bounded-width/structure cases, not general 3-SAT).

---
*`ALGO-000008` · unverified*

## Acceptance guidance

- **Full refutation:** an explicit (randomized) algorithm deciding 3-SAT in 2^{o(n)} time, with correctness proof. This is the only unconditional resolution.
- **Full proof:** a proof that no such algorithm exists. Expected to be at least as hard as P≠NP; a referee would require a genuine new barrier-crossing technique.
- **Partial results of publishable value:** (a) improved upper bounds closing the 1.307^n–2^{ε·anything} gap; (b) new equivalences (showing ETH ⇔ some other plausible hypothesis); (c) new ETH-based lower bounds for problems lacking them; (d) separating ETH from SETH or from Gap-ETH (showing non-implication via oracle worlds, in the style of known SETH↔sparsification separations (verify current state)).

Realistically, an attacking agent should target (b)–(d), not the conjecture itself.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/e3523409-5b2f-49d3-a44b-b4e9a8ba82dd?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000008.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000008)
