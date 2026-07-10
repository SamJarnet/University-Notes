2025-12-03 14:24

Status:

Tags: [[Artificial Intelligence]] [[Heuristic Search]]


# Minimax Search

#### Adversarial Games
- Must take account of the opponent 

#### The game of Nim
- Start with a single pile of seven matches 
- Each player takes it in turn to take a pile of matches and split into two differently sized piles of matches 
- The last player who is able to make a move is the winner 

- Very small game:
	- Few legal states
	- Few legal moves from each state
	- Game doesn't last long (few turns)
- Player who plays second has an (unfair) advantage
- Possible to construct a tree representing all the states of the game
	![[Pasted image 20251203182744.png]]

#### Game Tree Search 
- Initial state: Initial board state
- Goal state: Winning positions 
- Actions: One for each legal move 
- Expand function: generate legal moves
- Evaluation function: assigns score to each board state
- Game tree: all possible games

#### Minimax Search
- View of search in adversarial games
- MAX is traditionally the computer player, and picks the moves whose heuristic value is the best (maximum)
- MIN is the opponent and, and picks moves that minimise MAX's advantage

- Search to a given ply (depth-limited search)
- Evaluate heuristic for leaf nodes
- Internal nodes propagate heuristic values towards tree root
	- MAX nodes take the maximum of their child values (we make the best move we can)
	- MIN odes take the minimum of their child values (we assume our adversary makes the move that is worst for us)
- Pick action with best guaranteed score 

#### Properties of Minimax 
- Complete if tree is finite
- Optimal against an optimal agent
- TC = $O(b^m)$ 
- SC = $O(bm)$ (depth first)
- For chess, b roughly 35 and m roughly 100

#### Evaluation Functions 
- Typically a linear function in which coefficients are sued to weight game features 
- Unlikely to be perfect, computable evaluation function for most games
- Games with uncertainty add notions of expectation 

#### The Horizon Effect
- Cannot exhaustively search most game trees 
- Significant events may exist just beyond that part of the tree we have just searched
- The further we look ahead, the better our evaluation of a position 
- If we're searching the game tree to a depth of $n$ ply, what happens if our opponent is looking $n+1$ moves ahead 

#### Quiescent Search
- Bad evaluation functions can lead to wild swings in behaviour
	- Consider just material in chess (queen capture)
- Look for stable (quiescent) positions
- Can expand nodes in non-quiescent positions to a deeper ply, until a relatively stable situation is reached.

#### Branching Factor
- The branching factor of a game is the number of actions which can be chosen
- With game length (tree depth), affects complexity of decision making 





# References