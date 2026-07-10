02-10-2024 11:32

Status:

Tags: [[Mathematics I]], [[Sets]]


# Operations on sets

#### Elementary operations on sets:
Union of sets: A ∪ B 

- X ∪ Y = {z | z ∈ X or z ∈ Y}
- Associative: (X ∪ (Y ∪ Z) = (X ∪ Y) ∪ Z)
- Commutative: (X ∪ Y = Y ∪ X)

Intersection of points: A ∩ B
- X ∩ Y = {z | z ∈ X and z ∈ Y}
- Associative
- Commutative

Difference of points: B - A  (removes (A ∩ B) and elements only in A)
- X - Y = {z | z ∈ X and z ∉ Y}
- Not associative 
- Not commutative

Cartesian product: A x B (the set of all ordered pairs)
- X x Y = {(x, y) | x ∈ X & y ∈ Y}
- |X x Y| = |X| x |Y|
- Not associative 
- Not commutative

Sum (disjoint union): A + B
- X + Y = {(x, 0) | x ∈ X} ∪ {(y, 1) | y ∈ Y}
- |X + Y| = |X| + |Y|
- |X + Y| = |X ∪ Y| when |X ∩ Y| = ∅
- Associative 
- Not commutative

Powersets:
- Given a set X, a powerset P(X) or 2^x is the set of all subsets of X
- Examples:
	- P({0, 1}) = {∅, {0}, {1}, {0, 1}}
	- P({a, b, c}) = {∅, {a}, {b}, {c}, {a, b}, {a, c}, {b, c}, {a, b, c}}
	- P(∅) = {∅}
	- PP(∅) = {∅, {∅}}
	- |P(X)| = 2^|x|**
# References