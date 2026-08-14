TUFT.zip contains the paper, figures, data, etc

Verification artifacts for "The Topological Unified Field Theory on the Complex Hopf Fibration" by J. L. Nielsen, Center for Topological Physics.

The paper proves that any unified gauge theory with quantized charge must live on the universal complex Hopf fibration, derives its unique action (the Beltrami Lagrangian), and extracts the full particle spectrum and fundamental constants from the bundle's spectral geometry — zero free parameters, one empirical input (v = 246,220 MeV).

This repository contains two independent verification layers.

Lean 4 formalization (lean/). The structural forcing chain of Part I is machine-checked in Lean 4.32.2. The file TUFT_Forcing_Core.lean is self-contained, requires no external library, and compiles with zero errors and zero sorry placeholders. Five kernels are verified: charge quantization forces nontrivial holonomy, a domain admits no product splitting (so Z[c1] is indecomposable), any two classifying objects are homotopy equivalent, the complete U(1) base is CP-infinity, and affine absorption cannot move second differences. The compiler's axiom audit shows only Lean's built-in axioms (propext, Quot.sound). To verify: cd lean && lean TUFT_Forcing_Core.lean

Python numerical suite (python/). tuft_verification.py recomputes every derived quantity from the paper's boxed formulas at 40-digit precision using mpmath. It regenerates the charged-lepton mass ratios to nine significant figures, all six quark masses, three neutrino masses with both mass-squared splittings, the W/Z/Higgs masses, alpha to six figures, Newton's constant, the cosmological constant, the Weinberg angle, and the electron g-2 to nine figures. Section 11 of the script honestly tracks two open items where the printed formulas do not yet close the loop. To run: cd python && pip install mpmath && python tuft_verification.py

