# isProg: WHILE-Computable Program Verification



This repository contains a step-by-step reconstruction of the proof that the function `isProg` is WHILE-computable, following the encoding techniques from the Theory of Computation lectures.



## What is `isProg`?



`isProg : ℕ ⇀ ℕ` decides whether a natural number encodes a valid **GOTO program** (as defined in the WHILE computation model).  

It returns `1` if the input is a valid encoding, `0` otherwise.



A GOTO program is encoded as:



```

enc((k, m, enc(S₁), enc(S₂), …, enc(Sₙ)))

```



using Cantor pairing and list encoding, with metadata:

- `k` – number of input variables

- `m` – largest variable index used

- `enc(Sᵢ)` – encoded statements (inc, dec, GOTO, IF … GOTO, HALT)



## Repository Structure



```

.
├─ isprog.pdf
├─ pseudocode-isprog.txt
└─ README.md

```



## Slides – Checkpoint Breakdown



The presentation rebuilds `isProg` in **9 checkpoints**, each focused on a specific part of the program encoding:



| Checkpoint | Focus Area | Verification Task |
| :---: | :--- | :--- |
| **1** | Entire list | Ensure `isList(x1)` is true and `len ≥ 2` |
| **2** | Metadata (**`k`**, **`m`**) | Extract and check variable metadata bounds |
| **3** | `enc(S₁) … enc(Sₙ)` | Compute total statements: `n = len(statements)` |
| **4** | Loop setup | Initialize countdown loop over all statements |
| **5** | **`enc(Sᵢ)`** | Fetch current statement and verify `isList` |
| **6** | Decoded statement | Extract statement type (1‑5) and parameters |
| **7** | Type dispatch | Execute guarded blocks per type; check lengths & bounds |
| **8** | Advance pointer | Apply `snd` and decrement the loop counter |
| **9** | Final result | Ensure output register `x0` contains `1` or `0` |



The slides include a **comparison table** for the five statement types and the WHILE‑code fragments for each checkpoint.



## Full Pseudocode



The file `pseudocode/isProg.whi` contains the complete WHILE program with all checkpoints implemented using only:

- `x := 0`, `x := y`, `x := y + 1`, `x := y - 1`

- `IF x != 0 THEN … ELSE … END`

- `WHILE x != 0 DO … END`

- and the previously proved helpers `isList`, `len`, `fst`, `snd`.



Bound checks (`i ≤ m`, `j ≤ n`) are performed by repeated subtraction (monus) inside a WHILE loop.



## Why this matters



This construction shows how **any GOTO program can be verified syntactically** inside the WHILE language itself. It is a crucial step towards:

- Building a **universal interpreter** (a WHILE program that simulates any GOTO program)

- Proving the **halting problem** undecidability via diagonalisation

- Demonstrating that WHILE captures the full power of general recursion



## References



- Lecture notes: Theory of Computation, *Encoding* (Cantor pairing, list encoding, GOTO programs)

- N. D. Jones, *Computability and Complexity: From a Programming Perspective*

- B. Reus, *Limits of Computation: From a Programming Perspective*



---



*Built to accompany the Theory of Computation course. Contributions and corrections are welcome.*

```
