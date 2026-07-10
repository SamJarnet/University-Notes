2025-11-11 11:06

Status:

Tags: [[Artificial Intelligence]]


# Resolution Algorithm & First-Order Logic Notes

### 🔍 Resolution in Propositional Logic

#### What is Resolution?

- A single inference rule used for proof.
- **Complete** when paired with a complete search algorithm.
- Used to determine if:  
	$KB⊨ϕKB \models \phi KB⊨ϕ$

#### Resolution Rule

- Applies to **clauses** (disjunctions of literals).
- **Unit Resolution**: resolves a clause with a unit clause.
- **General Resolution**: resolves two clauses with complementary literals.
- **Factoring**: removes duplicate literals from clauses.

#### Conjunctive Normal Form (CNF)

- Every propositional formula can be converted to CNF.
- CNF = conjunction of disjunctions of literals.

#### Resolution Algorithm Steps

1. Convert $KB∧¬ϕKB \land \neg \phi KB∧¬ϕ$ to CNF.
2. Apply resolution to derive new clauses.
3. If empty clause is derived → contradiction → KB⊨ϕKB \models \phiKB⊨ϕ
4. If no new clauses → KB⊭ϕKB \not\models \phiKB⊨ϕ

---

### 🧠 Examples in Wumpus World

- Use resolution to infer facts like:
    - There is a pit in (3,1)
    - There is no pit in (1,2)
- Translate biconditional statements to CNF using logical equivalences.

---

### ✅ Resolution Examples

- Given KB:  
    ${A,¬A∨B,A∨¬B∨C,¬B∨C}$$\{A, \neg A \lor B, A \lor \neg B \lor C, \neg B \lor C\}$ {A,¬A∨B,A∨¬B∨C,¬B∨C}
    - Prove CCC: derive empty clause → contradiction $→ KB⊨CKB \models CKB⊨C$
    - Prove ¬B\neg B¬B: no empty clause $→ KB⊭¬BKB$ $\not\models \neg$ $BKB⊨¬B$

---

### 📉 Limitations of Propositional Logic

- Cannot represent:
    - Individuals (e.g., Mary, 3)
    - Properties or relations
    - Generalizations (e.g., “All triangles have 3 sides”)

---

### 🧬 First-Order Logic (FOL)

#### FOL Components

- **Objects**: entities with identity
- **Properties**: attributes of objects
- **Relations**: connections between objects
- **Functions**: mappings from objects to objects

#### Symbols

- **Constants**: Mary, 3
- **Functions**: father-of(Mary)
- **Predicates**: green(Grass), greater(5,3)

#### Syntax

- **Terms**: constants, variables, functions
- **Atomic Sentences**: predicates applied to terms
- **Complex Sentences**: built using logical connectives
- **Quantified Sentences**: use ∀ (universal) and ∃ (existential)

#### Quantifiers

- ∀x P(x): P holds for all x
- ∃x P(x): P holds for some x
- **De Morgan’s Laws** apply to quantifiers

---

### 🔄 Quantifier Rules

- **Universal Instantiation**: from ∀x P(x), infer P(c)
- **Existential Instantiation**: from ∃x P(x), infer P(c) with new constant
- **Existential Generalization**: from P(c), infer ∃x P(x)

---

### 🌐 Translating English to FOL

- “Every gardener likes the sun” → ∀x gardener(x) ⇒ likes(x, Sun)
- “There are exactly two purple mushrooms” → ∃x ∃y ... ∀z ...

---

### 👨‍👩‍👧 Genealogy KB in FOL

#### Predicates

- parent(x, y), child(x, y), spouse(x, y), ancestor(x, y), relative(x, y)

#### Rules

- parent(x, y) ⇔ child(y, x)
- father(x, y) ⇔ parent(x, y) ∧ male(x)
- ancestor(x, y) ⇐ parent(x, y)
- ancestor(x, y) ⇐ ∃z (parent(x, z) ∧ ancestor(z, y))
- relative(x, y) ⇐ ∃z (ancestor(z, x) ∧ ancestor(z, y))

#### Queries

- ancestor(Jack, Mark) → ✅
- relative(Liz, Joe) → ❌




# References