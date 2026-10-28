2026-10-20 12:24

Status:

Tags: [[Foundation of Machine Learning]]


# Ensemble Methods

#### Bagging and Random Forests
- Goal:
	- Reduce the variance of high-variance models (like deep decision trees)
- Method:
	- Train many independent, complex models on different bootstrap samples of the data
- Result:
	- The average of these diverse models is more stable and less prone to overfitting
- What if our base models are too simple?
	- Simple models, like shallow decision trees ("stumps"), have high bias but low variance. They underfit the data.
- Can we combine many simple, high-bias models to create a single, powerful, low-bias model?

#### Boosting: The Core Idea
- Boosting is an ensemble method that builds strong learner by combining weak learners sequentially
- The Process
	- Each new model is trained to correct the mistakes made by the previous models in the sequence.
	![[Pasted image 20261020122816.png]]
- It converts a set of "weak learners" (models only slightly better than random guessing) into a  single "strong learner"

#### Boosting vs Random Forest
- Random Forest (Bagging)
	- Goal: Reduce Variance
	- Trains models in parallel
	- Base learners are complex (deep trees)
	- Each model is independent
	- Final prediction is a simple average/vote
- Boosting
	- Goal: Reduce Bias
	- Trains model sequentially
	- Base learners are simple (weak learners)
	- Each model depends on the previous
	- Final prediction is a weighted average 


#### AdaBoost: 
- AdaBoost works by sequentially training weak classifiers and giving more weight to the data points that are misclassified at each step. 
- The AdaBoost Algorithm
	- 1. Initialise equal weights for all data points $w_n^{(n)} = \frac 1 N$
	- 2. For $t=1, ..., T$:
		- Train a weak learner $h_t(x)$ on the data using weights $w^{(t)}$ 
		- Calculate the weighted error $\epsilon_t$ of $h_t(x)$
		- Calculate the classifier's weight $\alpha_t = \frac 1 2 \log(\frac{1-\epsilon_t} {\epsilon_t})$
		- |
		  |
		  |
		  |



