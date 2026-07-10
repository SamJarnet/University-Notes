2026-01-01 16:14

Status:

Tags: [[Artificial Intelligence]]


# Machine Learning Part 2

#### Classifiers 
- Algorithms who learn a classification rule: 
	- $h(x) = \hat{y}$
- We hope that $\hat{y} = y$ 

#### We want generalisation 
- We want:
	- Small changes in training data to barely have an effect on predictions 
	- Classifiers to work well for any test set, not just one 
	- Performance, as measured by $P$, remain consistent between training and testing 

#### Example 1 
![[Pasted image 20260101161758.png]]
- KNN is generally a stable predictor 
- When $k$ is not very small, the voting mechanism keep it protected from being affected by changes in the data 
- It's non-parametric nature helps too

#### Example 2 
![[Pasted image 20260101161915.png]]

#### Intuition: use a set of models 
- instead of relying on the statement's from one model, we can consult a couple of them
- Goal: reduce variance in predictions 

#### Bagging 
- Generate $K$ distinct datasets by sampling with replacement (bootstrapping) from the training set: 
	![[Pasted image 20260101162044.png]]
- Each new dataset $D_i$ is the same size of the training set, 
	![[Pasted image 20260101162110.png]]
- $K = 5$ means we sample 5 datasets
	![[Pasted image 20260101162133.png]]
- For a new observation (feature vector) $x$ we want to make a decision about it (classify it )
- We predict what the majority predicts 
	![[Pasted image 20260101162221.png]]
- Powerful for reducing variance in the classifiers $h_i$ 
- Works well when the $h_i$ are not highly correlated 
- Problem for DT:
	- If certain features lead to large reduction of information gain, most trees $h_i$ will pick them as root
	- Trees will look more or less the same (high correlation)
#### Random Forest
- Add randomness in the observations (bagging) and in the feature selections 
- Key:
	- At each node of the tree, consider only a sample of the features for computing information gain

#### Numerical Example:
![[Pasted image 20260101162435.png]]
![[Pasted image 20260101162443.png]]
![[Pasted image 20260101162514.png]]
![[Pasted image 20260101162531.png]]
![[Pasted image 20260101162540.png]]
![[Pasted image 20260101162546.png]]
![[Pasted image 20260101162621.png]]

#### Considerations 
- Every tree in the forest is, in isolation, potentially noisy: a weak learner 
- RF combines a couple of weak learners, an ensemble of weak learners, to provide strong predictions 
- Generally, RF provides very good stability, even without pruning its trees
- RF is computationally efficient, and easily parallelisable 

#### How to choose a good model
- We need to:
	- Find a good and stable configuration for each model
	- Validate on a holdout set, before predicting over the test set

#### K-Fold Cross-Validation
- Use your training set for training and validation 
- Divide your training set into $K$ non-overlapping sets (folds)
- Set aside 1 Fold for validation and train your classifier using the other $K-1$ folds
- Repeat until every fold was used as validation set once
- Report the average performance over the validation sets
- The averaged performance should induce low bias with respect to the data 
- ![[Pasted image 20260101164002.png]]

#### Comments 
- Using CV supposes two layers of model evaluation:
	- Evaluation of model for model selection, using the training set only.
	- Evaluation of the selected model on the test set
- Standard vales for $K$ are typically between 5 and 10
- CV is how ML practitioner do parameter tuning, e.g. find $k$ for KNN, depth bounds for DTs, etc
- When $K = n$, where $n = |D|$, we have an extreme case of CV:
	- Leave-one-out cross-validation (LOOCV). Powerful but computationally exhausting
# References