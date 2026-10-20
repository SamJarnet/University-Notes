2026-10-18 15:13

Status:

Tags: [[Foundation of Machine Learning]]


# Classification - Nonparametric Methods

#### k-Nearest Neighbours (kNN): The Concept
- The idea:
	- To classify a new data point, look at its neighbours in the feature space.
- The kNN Algorithm for Classification
	- To classify a new query point $x_q$: 
		- 1. Find the $k$ points in the training data closest to $x_q$.
		- 2. Let these $k$ neighbours "vote" on the class of $x_q$.
		- 3. Assign the majority class to $x_q$ 
	- The only training is storing the dataset. The real work is at prediction time
	
	![[Pasted image 20261018151920.png]]

#### The Curse of Dimensionality
- The problem: Local Neighbourhoods Vanish
	- In high-dimensional space, the concept of a "local neighbourhood" breaks down.
	- To capture even a small fraction of the data volume, the neighbourhood must stretch over a large fraction of the range of each feature.
- Side of a hypercube needed to capture 10% of the data:
	![[Pasted image 20261018152201.png]]
- Implication:
	- In a 10-dimensional space, our "local" neighbourhood must span nearly 80% of the range of each feature.
	- The neighbours are no longer meaningfully local


#### Revisiting Model Assumptions
- Parametric Models
	- Assume a fixed functional form
	- The model is defined by a small, fixed number of parameters
	- Pros:
		- Fast, efficient, less prone to overfitting if assumptions are correct
	- Cons:
		- High bias (underfitting) if assumptions are wrong
- Non-Parametric Models
	- Do not assume a fixed functional form
	- Model complexity grows with the size of the dataset
	- Pros:
		- Highly flexible, can fit complex patterns. Low bias.
	- Cons:
		- Slower, needs more data, high risk of overfitting (high variance)

#### Decision Trees
- Also called Classification and Regression Trees (CART). A model that makes predictions by asking a series of simple questions about the features.
- The idea:
	- Recursively partition the feature space into disjoint regions.
	- Assign a simple model (like a constant class label) to each region.
		![[Pasted image 20261018215257.png]]
- Visualising Tree Partitions 
	- Each split corresponds to an axis-aligned cut in the feature space
		![[Pasted image 20261018215416.png]]

#### How to Build a Tree: Recursive Splitting
- Trees are built top-down using a greedy algorithm like CART
- The Algorithm
	- 1. Start with all data in the root node.
	- 2. Find the best possible split $(j, t)$ across all features $j$ and all thresholds $t$. "Best" means the split that results in the "purest" child nodes
	- 3. Create two child nodes and move the data into them based off the split. 
	- 4. Repeat this process on each child node recursively 
	- 5. Stop when a node is perfectly pure, contains too few samples, or a max depth is reached.

#### Measuring Node Impurity
- We want to choose the split that maximally reduces impurity
- Common Impurity Measures
	- For a region with class proportions $p_c$:
		- Gini Impurity:
			- $I_G = 1-\sum_cp_c^2$
		- Entropy:
			- $I_H = -\sum_cp_c\log_2(p_c)$
	- Both are 0 for a pure node and maximised for a uniform distribution
	
	![[Pasted image 20261018220034.png]]

#### Decision Trees - Pros and Cons
- Pros:
	- Interpretable ("white box")
	- Handles mixed data types and doesn't require feature scaling
- Cons:
	- High Variance: Very prone to overfitting
	- Greedy approach may not be globally optimal

#### Ensemble Learning and Bagging
- Decision Trees are very sensitive to the specific training data they see. This is the definition of high variance.
	![[Pasted image 20261018220345.png]]
- The Core Idea: If we average many different, unstable models, can we get one stable, accurate model? This is ensemble learning.
- Bagging = Bootstrap Aggregating is a general technique to reduce the variance of any high-variance model.
- The Idea:
	- Bootstrap: Create $B$ new datasets by sampling with replacement from the original data
	- Train: Train one base model $f_b(X)$ (e.g. a deep decision tree ) on each bootstrap sample
	- Aggregate: The final prediction is the majority vote (classification) or average (regression) of all $B$ models.

#### Visualising the Bootstrap Process
- Bootstrap Process. "Pull oneself up by one's bootstraps".
	- Metaphor: You're trying to "lift" your statistical estimates from the sample data alone, without any outside help - just like pulling yourself up by your own bootstraps
	![[Pasted image 20261018220953.png]]
- Sampling with replacement
	- Each bootstrap sample has the same size as the original
	- Due to sampling with replacement, some points are duplicated while others are omitted entirely.

#### Random Forests
- Random Forests improve on Bagging by further decorrelating the trees.
- The Random Forest Algorithm
	- 1. Create $B$ bootstrap samples of the data (like Bagging)
	- 2. For each sample, grow a decision tree.
	- 3. Key Difference:
		- At each node, do not search all $D$ features for the best split. Instead, randomly select a small subset of $m < D$ features and find the best split only among those features. 
	- 4. Aggregate predictions by majority vote.
- Why it helps:
	- This forces the trees to be more diverse. Even if one feature is very powerful, it won't be selected for every split in every tree, giving other features a chance. More diversity leads to a better ensemble. 

#### Out-of-Bag (OOB) Error: What is it?
- The "leftover" Data
	- When creating a bootstrap sample of size $N$ from data of size $N$:
		- The probability of a specific data point not being picked in a single draw is $(1- \frac 1 N)$
		- The probability of it not being picked in any of the $N$ draws is $(1 - \frac 1 N)^N$ 
	- At $N \rightarrow ∞$, this probability converges to
		- $\lim_{N→∞} ( 1 − \frac 1 N) ^N = e^{−1} ≈ 0.368$
	- This means for any given tree in the forest, about 37% of the original data points are left out of its original training set. These are its Out-of-Bag (OOB) samples

#### Using OOB Error for Model Evaluation 
- The OOB samples give a "free" estimate of test error, with no separate validation set or cross-validation.
- The OOB Evaluation Algorithm 
	- 1. For each data point $i$ in the original training set:
		- Find the trees that did not use point $i$ in training (its OOB trees) 
		- Let the sub-ensemble of OOB trees make a prediction for point $i$ 
	- 2. The OOB error is the total number of incorrect predictions made this way, divided by $N$.
- A key advantage: OOB error is a nearly unbiased estimate of the test error once the forest has enough trees. With only a few trees it runs high, since each point is predicted by just $\approx 37$% of them.