<!-- solve-problem:5dabcbef-2a5d-4c33-ba55-b2c5d4e50078 -->
# Polynomial-length constant-query locally decodable codes

A [Tangle Solve problem](https://solve.tangle.tools/problems/5dabcbef-2a5d-4c33-ba55-b2c5d4e50078).

## What is the problem?

A **locally decodable code (LDC)** is an encoding map C: {0,1}^k → Σ^n, together with a decoding algorithm that, given an index i ∈ [k] and oracle access to a received word y ∈ Σ^n with y differing from C(x) in at most δ·n positions (for constant adversarial error rate δ, e.g., δ = 0.01), recovers x_i using at most q queries to y, with success probability ≥ 2/3.

The open problem: **construct, for some constant q ≥ 3 and constant alphabet |Σ|, an LDC with n = poly(k) that tolerates a constant adversarial error rate δ.** Equivalently, decide whether L(k, q) = poly(k) is achievable for fixed q, constant alphabet, and constant δ.

The precise tension: the number of queries q, the alphabet size, and the error tolerance must all be constants independent of k, while block length is polynomial in message length. Ambiguities in the informal statement worth noting: (1) whether δ must be "large" or any fixed positive constant suffices (standard LDC definitions allow any constant δ > 0, and typically one can boost δ at polynomial cost, but for constant query counts the achievable δ matters); (2) whether a constant-factor blowup in q (e.g., from 3 to some larger fixed q) is acceptable — the problem as stated permits any fixed q ≥ 3.

## Why does it matter?

LDCs are the information-theoretic backbone of private information retrieval (PIR) schemes with low communication; polynomial-length constant-query LDCs would yield 2-server PIR with O(polylog k) communication per bit and dramatically improved concrete costs for private database access. They are central to the theory of fault-tolerant data storage — a server storing data encoded with such a code can answer queries about individual symbols while provably tolerating corruption — and to derandomization, where LDCs relate to rigidity and matrix rigidity questions. Currently no one knows whether the "sweet spot" (constant queries, constant alphabet, polynomial length) exists; resolving this either way would settle a basic question about the local decodability of information.

## What's already known?

- **q = 2 is closed, negatively.** Katz–Trevisan and later Dvir–Gopalan–Yekhanin proved any 2-query LDC (binary or constant alphabet) requires exponential length n = exp(Ω(k)). So q ≥ 3 is genuinely necessary.
- **q = 3 with large alphabet:** Yekhanin (2007) gave 3-query LDCs of subexponential length n = exp(exp(O(√log k · log log k))) assuming infinitely many Mersenne primes; Efremenko (2009) removed the assumption and improved parameters, using matching vector constructions over Z_m^n. These tolerate only small error rates and use constant alphabet, with subexponential — not polynomial — length.
- **Lower bounds:** For constant q, Woodruff and others proved superpolynomial lower bounds for certain regimes — specifically, for 2-query and for constant-query codes with specific decoding structure or over constant alphabet, bounds of the form exp(Ω(log^2 k / log log k)) or similar are known for restricted classes (verify exact statements). The known lower bounds do not rule out poly(k) length for q = 3 and general (smooth) decoders.
- **Upper bound trichotomy:** With growing alphabet or growing q, polynomial length is easy (e.g., Reed–Muller with q = O(√(log k)) or constant-query over polynomial-size alphabet via combinatorial designs). The open case is constant-constant-constant.

Why approaches fall short: matching vector / Reed–Muller-based constructions all bottom out at subexponential length for constant q; lower-bound techniques (matrix-incidence, spectral) capture only 2 queries or restricted decoder forms.

## What would count as solving it?

Any of the following, per variant:

1. **Upper bound (construction):** An explicit family of encodings C_k: {0,1}^k → Σ^{n}, |Σ| = O(1), n ≤ k^c, with a decoder making at most q = O(1) queries, correcting a constant fraction δ > 0 of errors with success probability ≥ 2/3. Referee standard: full proof of correctness and parameters, plus ideally an efficient (polytime) encoder and decoder.
2. **Lower bound (impossibility):** A proof that for some fixed q and |Σ|, every q-query constant-alphabet LDC tolerating constant δ requires n superpolynomial in k. Even n = k^{ω(1)} for q = 3 would be a landmark.
3. **Intermediate:** superpolynomial lower bounds for any fixed q ≥ 3 unconditionally, or polynomial-length constructions with q = 3 but sub-constant δ — either advances the frontier meaningfully, though neither alone resolves the census statement.

## How to start

1. **Read first:** Yekhanin's survey chapter ("Locally Decodable Codes," now a book, Springer 2010) Chapters 1–3 for definitions and the matching-vector machinery; then Efremenko (2009) for the cleanest matching-vector presentation.
2. **Understand the matching vector framework:** it reduces LDC construction to families of vectors in Z_m^n with restricted dot-product patterns; understand precisely why polynomial length is blocked (the combinatorics of restricted dot products over composite moduli).
3. **Lower-bound angle:** study the Katz–Trevisan smooth-code reduction and the Dvir–Gopalan–Yekhanin 2-query proof, and the Woodruff line of constant-query lower bounds, to see exactly which decoder properties the techniques exploit and where they fail at q = 3.
4. **Main obstacle:** every known construction is either high-query (Reed–Muller) or subexponential-length (matching vectors); every known lower-bound technique caps out at q = 2 or restricted decoders. Expect the solution to need a genuinely new construction idea or a new lower-bound invariant (e.g., quantum-inspired: note the census flags a quantum-complexity connection — constant-query LDCs relate to quantum one-way communication and PIR lower bounds via the quantum-information-theoretic route of e.g. Nayak and others (verify)).

## Key references

- **Sergey Yekhanin, "Towards 3-query locally decodable codes of subexponential length," STOC 2007. DOI: 10.1145/1250790.1250830.** Constructs 3-query LDCs of subexponential length from matching vector families, conditional on Mersenne primes.
- **Klimet Efremenko, "3-query locally decodable codes of subexponential length," STOC 2009.** Gives an unconditional 3-query LDC of length exp(exp(O(√log k log log k))) using matching vectors over composite moduli.
- **Sergey Yekhanin, *Locally Decodable Codes and Private Information Retrieval Schemes*, Springer (2010, extended from EATCS survey).** The standard reference for definitions, the LDC–PIR connection, and lower-bound techniques.
- **Zeev Dvir, Parikshit Gopalan, Sergey Yekhanin, "Matching vector codes," SIAM J. Comput. 2011 (preliminary FOCS 2010).** Generalizes the matching-vector framework and proves lower bounds on matching vector families limiting this approach.
- **David Woodruff, "A quadratic lower bound for three-query linear locally decodable codes over any field," J. Computer & System Sciences 2012 (verify venue/year).** Superlinear-to-quadratic lower bounds for restricted (linear) 3-query decoders, showing where current lower-bound technology stops.
- **Jonathan Katz, Luca Trevisan, "On the efficiency of local decoding procedures for error-correcting codes," STOC 2000.** The foundational paper defining LDCs, the smooth-code reduction, and proving early lower bounds.

## Warnings

- **Do not pursue q = 2:** exponential lower bounds are tight and closed; any effort there is wasted.
- **Hidden constraint — error rate:** Yekhanin/Efremenko constructions tolerate only very small δ (inverse subexponential in some parameters); the census demands **constant δ**. Boosting δ via repetition of coordinates multiplies query count or length — check carefully that any claimed solution preserves *constant* q, *constant* alphabet, and *constant* δ simultaneously.
- **Alphabet subtlety:** allowing even logarithmic alphabet size trivializes the problem (Hadamard-like or combinatorial constructions); the census explicitly requires constant alphabet.
- **Decoder model:** some lower bounds apply only to *adaptive*, *non-adaptive*, or *linear* decoders; the open problem is over general randomized decoders, so a negative result must cover all of them.
- **Quantum connection is a lead, not a result:** no known proof transfers quantum PIR lower bounds to rule out constant-query classical LDCs of polynomial length; treat it as a possible tool, not established lore.

---
*`ALGO-000193` · unverified*

## Acceptance guidance

Any of the following, per variant:

1. **Upper bound (construction):** An explicit family of encodings C_k: {0,1}^k → Σ^{n}, |Σ| = O(1), n ≤ k^c, with a decoder making at most q = O(1) queries, correcting a constant fraction δ > 0 of errors with success probability ≥ 2/3. Referee standard: full proof of correctness and parameters, plus ideally an efficient (polytime) encoder and decoder.
2. **Lower bound (impossibility):** A proof that for some fixed q and |Σ|, every q-query constant-alphabet LDC tolerating constant δ requires n superpolynomial in k. Even n = k^{ω(1)} for q = 3 would be a landmark.
3. **Intermediate:** superpolynomial lower bounds for any fixed q ≥ 3 unconditionally, or polynomial-length constructions with q = 3 but sub-constant δ — either advances the frontier meaningfully, though neither alone resolves the census statement.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/5dabcbef-2a5d-4c33-ba55-b2c5d4e50078?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000193.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000193)
