2025-11-10 20:28

Status:

Tags: [[Artificial Intelligence]]


# Logic


### 📚 References

- **Main Text**: Russell & Norvig, _Artificial Intelligence: A Modern Approach_, Ch. 7
- **Supplementary**: Mendelson, _Introduction to Mathematical Logic_, Ch. 1

---

### 🤖 Logical Agents

- Agents use a **Knowledge Base (KB)** to store facts.
- KB is queried and updated via **inference**.
- Inference must be **truth-preserving** and independent of implementation.

---

### 🕸️ Wumpus World

- 4×4 grid cave with:
    - **Wumpus** (dangerous)
    - **Gold** (goal)
    - **Pits** (deadly)
- Agent actions: move, turn, shoot, grab, climb.
- Sensors:
    - **Stench**: near Wumpus
    - **Breeze**: near Pit
    - **Glitter**: on Gold
    - **Bump**: hits wall
    - **Scream**: Wumpus killed

---

### 📐 Propositional Logic

#### Language

- **Symbols**: P, Q, R...
- **Connectives**:
    - ¬ (not)
    - ∧ (and)
    - ∨ (or)
    - ⇒ (implies)
    - ⇔ (iff)

#### Formulas

- **Atomic**: single variables
- **Compound**: built using connectives

#### Semantics

- **Valuation**: assigns truth values (0 or 1)
- Truth tables define semantics of connectives.

#### Key Concepts

- **Satisfiable**: true in some model
- **Tautology**: true in all models
- **Contradiction**: false in all models
- **Logical Equivalence**: same truth table
- **Model of KB**: valuation making all KB formulas true

---

### ⊨ Semantic Consequence

- KB ⊨ ϕ ⇔ every model of KB is a model of ϕ

---

### ⊢ Syntactic Proof

- Axioms:
    - A1: ϕ ⇒ (ψ ⇒ ϕ)
    - A2: (ϕ ⇒ (ψ ⇒ γ)) ⇒ ((ϕ ⇒ ψ) ⇒ (ϕ ⇒ γ))
    - A3: (¬ϕ ⇒ ¬ψ) ⇒ (ψ ⇒ ϕ)
- Rule: **Modus Ponens**: from ϕ and ϕ ⇒ ψ, infer ψ
- **Theorem**: derivable from axioms using rules

---

### ✅ Soundness & Completeness

- **Soundness**: KB ⊢ ϕ ⇒ KB ⊨ ϕ
- **Completeness**: KB ⊨ ϕ ⇒ KB ⊢ ϕ

---

### 🔍 Inference in Wumpus World

- Use propositional variables like:
    - Px,y: pit at (x,y)
    - Wx,y: wumpus at (x,y)
    - Bx,y: breeze at (x,y)
    - Sx,y: stench at (x,y)
- Example KB:
    - ¬P₁,₁
    - B₁,₁ ⇔ (P₁,₂ ∨ P₂,₁)
    - B₂,₁ ⇔ (P₁,₁ ∨ P₂,₂ ∨ P₃,₁)
    - ¬B₁,₁
    - B₂,₁

#### Semantic Inference

- Check if KB ⊨ ¬P₁,₂ and KB ⊨ ¬P₂,₂ via truth tables

#### Syntactic Inference

- Use axioms, rules, and equivalences to prove KB ⊢ ¬P₁,₂

---

### 🔎 Proof Search

- Define proof as a search problem:
    - **Initial State**: KB
    - **Actions**: inference rules
    - **Goal**: derive target formula
- Efficient vs. truth-table enumeration



# References