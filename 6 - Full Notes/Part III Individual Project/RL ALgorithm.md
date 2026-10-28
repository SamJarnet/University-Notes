2026-10-28 13:23

Status:

Tags: 


# RL ALgorithm

#### Defintitions
- PPO (Proximal Policy Optimisation)
	- Policy-gradient RL algorithm that learns a policy matching states to actions
	- Uses a clipped objective to limit excessively large policy updates
	- Maxmises expected cumulative reward
	- Simple, widely used. Supports both discrete and continuous actions (mine would be probably be continuous)
	- Limitation: may sacrifice safety if collision penalties are outweighed by other rewards
- P3O (Penalised Proximal Policy Optimisation)
	- Extension of PPO designed for constrained / safe RL
	- Separates reward optimisation from explicit cost constraints 
	- Example: maximise mission performance subject to a limit on collision related cost
	- Uses an exact-penalty formulation with a PPO-style objective
	- Limitation: does not guarantee every trajectory is collision free

#### P3O (Penalised Proximal Policy Optimisation)
- Made for RL systems with safety requirements
- Existing solutions can be computationaly expensive and cumbersome to obtain an analytical solution without an extra inner-loop optimisation.
- Two techniques:
	- Empy exact penalty functions to derive an equivalent unconstrained optimisation problem that is compatible with multiple and constraints and arbitrary initial policies.
	- Extend the clipped surrogate obective in PPO to CMDPs (Constrained Markov Decision Process), which eliminates the trust-region constrain on both reward term and cost term.
- P30:
	- High accuracy and sample efficient 
	- Feasibility: P3O could admit arbitrary initialisation with a consistent objective function and doesn't need additional recovery methods for infeasible policies
	- Scalability: P3O is naturally scalable to multiple constraints or agents without increasing complexity.

#### P30 Example for Satellites (Autonomous spacecraft collision avoidance with a variable number of space debris based on safe reinforcement learning)
- 




