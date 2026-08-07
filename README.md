TUFT-Complex-Hopf

Verification artifacts for "The Topological Unified Field Theory on the Complex Hopf Fibration" by J. L. Nielsen, Center for Topological Physics.

The paper proves that any unified gauge theory with quantized charge must live on the universal complex Hopf fibration, derives its unique action (the Beltrami Lagrangian), and extracts the full particle spectrum and fundamental constants from the bundle's spectral geometry — zero free parameters, one empirical input (v = 246,220 MeV).

This repository contains two independent verification layers.

Lean 4 formalization (lean/). The structural forcing chain of Part I is machine-checked in Lean 4.32.2. The file TUFT_Forcing_Core.lean is self-contained, requires no external library, and compiles with zero errors and zero sorry placeholders. Five kernels are verified: charge quantization forces nontrivial holonomy, a domain admits no product splitting (so Z[c1] is indecomposable), any two classifying objects are homotopy equivalent, the complete U(1) base is CP-infinity, and affine absorption cannot move second differences. The compiler's axiom audit shows only Lean's built-in axioms (propext, Quot.sound). To verify: cd lean && lean TUFT_Forcing_Core.lean

Python numerical suite (python/). tuft_verification.py recomputes every derived quantity from the paper's boxed formulas at 40-digit precision using mpmath. It regenerates the charged-lepton mass ratios to nine significant figures, all six quark masses, three neutrino masses with both mass-squared splittings, the W/Z/Higgs masses, alpha to six figures, Newton's constant, the cosmological constant, the Weinberg angle, and the electron g-2 to nine figures. Section 11 of the script honestly tracks two open items where the printed formulas do not yet close the loop. To run: cd python && pip install mpmath && python tuft_verification.py

CI runs both checks on every push.

Connes-Rigidity

Lean 4 formalization for "Connes' Rigidity Conjecture: Disproof of the Counterexamples and Proof of the Theorem" by J. L. Nielsen, Center for Topological Physics.

The paper has two parts. Part I disproves three independent claimed counterexamples to Connes' rigidity conjecture (OpenAI, Anthropic, and Zhou). Part II proves the conjecture itself. The disproof and the proof are the same argument.

The primary argument is a reductio ad absurdum. Assume the claimed algebra isomorphism L(Γ₀) ≅ L(Γτ). Equip both groups with Bernoulli actions (chosen by us, not inherited from either counterexample). The twisted comultiplication Θ(fuₘ) = fuₘ ⊗ Φ(uₘ) and Ioana's classification (Theorem 8.2, JAMS 2011) produce an injective group homomorphism δ₂ : Γ₀ → Γτ. The Borel density theorem forces δ₂ to preserve the fiber Z⁴. Margulis superrigidity forces an inner automorphism on the quotient Sp₄(Z). Schur's lemma forces a scalar map on the fiber. The resulting cohomological identity α*[τ] = [τ] = 0 contradicts the non-vanishing of the Bockstein class. By reductio, L(Γ₀) ≇ L(Γτ). The only inputs are the group-theoretic structure of the groups and the published theorems of Ioana, Borel, Margulis, and Schur.

The reductio does not rely on any semantic mismatch between code labels and mathematical objects, on whether the ICC or property-(T) certificates in the Lean code are valid, or on any code-level observation whatsoever. It is purely mathematical.

The OpenAI formalization additionally exhibits three code-internal failures, each independently fatal: (i) a specification gap (cocycle extension verified as semidirect product), (ii) nontrivial centre destroying ICC, (iii) infinite abelian quotient destroying property (T). The Zhou construction falls to the same reductio: the unique maximal abelian normal subgroup must be preserved by any injective homomorphism, and Zhou's own non-isomorphism proof (Section 6) provides the contradiction.

Part II proves the conjecture: every countable discrete ICC group with Kazhdan's property (T) is W*-superrigid. The proof is the same reductio applied universally. Assume L(G) ≅ L(H). The twisted comultiplication and Ioana's classification produce an injective δ₂ : G → H. Injectivity follows from factoriality. Finite index follows from countability of subfactor conjugacy classes for property-(T) factors. Surjectivity follows from the finite-depth theorem for amenable property-(T) standard invariants. Therefore G ≅ H. No shared subgroups, no semidirect-product structure, no special features beyond ICC and property (T) are required. The verification of the non-intertwining conditions is uniform in Φ because αₜ fixes Θ(uₘ) pointwise for every Φ (it acts on L∞(X), not on group unitaries) and Θ(L∞(X)) = L∞(X) ⊗ 1 independently of Φ. The argument is universal.

ConnesAppendix.lean compiles against a bare Lean 4.22.0 toolchain with no Mathlib and no other package, with zero errors and zero sorry placeholders. Part A formalizes the code-level obstructions unconditionally — central elements in products, failure of ICC, infinite abelian quotients — depending on no axioms whatsoever. Part B formalizes the deductive skeleton of Part II: the case elimination (Cases I and II ruled out, Case III yields group morphisms), the injectivity and surjectivity of δ₂, and the final theorem connes_rigidity producing a bijective group homomorphism. Every analytic input is a named axiom corresponding to a cited theorem. Two design choices prevent vacuity: IsICC and HasPropertyT are opaque predicates (not trivially satisfiable classes), and bijectivity is asserted of the specific morphism the classification returns (not of an arbitrary homomorphism).

The compiler's axiom audit confirms Part A depends on nothing, Part B depends on exactly the ten declared axioms, and neither list contains sorryAx. check.sh is a five-level guard script verifying compilation, no sorry in source, no compiler sorry warning, no sorryAx in axiom lists, and no native_decide/unsafe/admit. The Makefile gates the LaTeX build on this check — a broken appendix cannot reach the document.

To verify: cd lean && lean ConnesAppendix.lean

CI runs the full check on every push.

Contact: JennyLorraineNielsen@gmail.com, Center for Topological Physics, Lawrence, Kansas.
