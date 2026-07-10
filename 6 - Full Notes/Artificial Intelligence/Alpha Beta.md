2025-12-03 21:42

Status:

Tags: [[Minimax Search]] [[Artificial Intelligence]]


# Alpha Beta

#### Alpha-beta pruning
- Minimax explores entire tree to a given ply depth (and evaluates the leaves, and then propagates the values back up the tree)
- Alpha-beta pruning performs DFS but allows us to disregard certain branches of the tree

- Alpha represents the lower bound on node value (the worst we can do)
	- Associated with MAX nodes
	- Never decreases 
- Beta represents the upper bound on node value (the best we can do)
	- Associated with MIN nodes 
	- Never increases 
- If the best we can do on the current branch is $\leq$ the worst we can do elsewhere, there's no point continuing on this branch.
	![[Pasted image 20251203214606.png]]

#### Directionality  
- Note that Alpha-beta pruning will remove different sub-trees depending on the direction in which the tree is reversed
- Ordering the sub-trees has a large effect on the amount of pruning 

#### Alpha-beta and Minimax
- Alpha-beta is guaranteed to give the same values as Minimax
- If the tree is ordered (best moves examined first), complexity is $O(b^{d/2})$ 
	- Minimax is $O(b^d)$
	- Search twice as deep for the same effort
- Perfect ordering not possible
	- If it was, we wouldn't need alpha beta
	- In practice, running close to optimistic estimate 

#### Cost of Game-Playing 
- Move generation (EXPAND) - 50%
- Evaluation - 40%
- Search control - 10%

- Search techniques typically used for mid-game
- Openings and endings taken from database
# References