2025-11-25 11:35

Status:

Tags: [[Artificial Intelligence]]


# Machine Learning Part 1


#### AI and Machine Learning
- ![[Pasted image 20260101150002.png]]

- What is machine learning?
	- Machine Learning is the field of study that gives the computer the ability to learn without being explicitly programmed
	- A computer is said to learn from experience E with respect to some class of tasks T and performance metric P, if its performance of tasks in T, as measured by P, improves with experience E.
		- e.g:
			- T = playing checkers
			- P = percent of games won against a human
			- E = games played against itself

#### Types of learning 
-  Supervised learning
- Unsupervised learning
- Reinforcement learning

#### Supervised learning 
- Training data:
	- ![[Pasted image 20260101150511.png]]
- $y_1$ is the the label for feature vector $x_1$ 
- Classification: 
	- Labels are discrete values, e.g. {spam, no-spam} {cancer, healthy}
- Regression:
	- Labels are continuous values: stock market, blood pressure measurements, anything expressed as a Real Number, i.e. $y_i \in \mathbb{R}$ 

#### Example
- Training data example:
	- ![[Pasted image 20260101150747.png]]
- Anatomy of a feature vector 
	- ![[Pasted image 20260101150807.png]]

- Each component of the vector is a feature or a measurement 

#### Algorithms for classification 
- Classifiers find a function $h(x) \rightarrow y$ 
- Standard success metric, $P$: fraction of correctly classified objects 
- ![[Pasted image 20260101150956.png]]


#### Unsupervised learning 
- Input data: $\{x_1, x_2, x_3...x_n\}$
- No label information available - only feature vectors 
- Classic problem: clustering 
- Applications: anomaly detection, knowledge discovery, etc.

#### Handwritten recognition learning problem
- ![[Pasted image 20260101151329.png]]


#### Self - Driving Car learning problem
- ![[Pasted image 20260101151357.png]]

#### Gene similarities learning problem
- ![[Pasted image 20260101151424.png]]

#### Why do we need machine learning?
- Tasks that are too complex to program:
	- Computer vision: we know to detect objects but have no idea how we do it 
	- Search engines: a human cant read the entire internet
-  Adaptivity 
	- Speedy and adaptive development of programs 


#### Decision trees - definition 
- Decision tree learning is a method for approximating discrete-valued target functions, in which the learned function is represented as a decision tree
- $h(x) \rightarrow y$ takes the form of a tree
- Each node represents a test on a feature, each leaf is a final decision (classification) on an example (x, y)
- Ordering of the features we test matters

#### Example 
- ![[Pasted image 20260101152557.png]]

#### Selecting features
- Features testing is based on maximising the information gain obtained from each feature 
- Informative features allow us to reach decisions with fewer tests; they meaningfully reduce ambiguity for the final decision 
- Think of 20 questions, bad questions don't reveal much about the answer

#### Example 
- ![[Pasted image 20260101152742.png]]
- features: $[$outlook,temperature, humidity, wind$]$
- label: PlayTennis $∈$ {yes, no}
- When outlook = "overcast", we can immediately make a decision:
	![[Pasted image 20260101152840.png]]
- Descent to sunny and then rain and repeat 
	![[Pasted image 20260101152949.png]]

#### Formal information gain
- This concept can be mathematically be defined in terms of the concept of entropy 
 - The information gain is the reduction of entropy observed when selecting a specific feature from the tree
#### Important Considerations 
- Trees can be successfully used with both discrete and continuous features
- In practise, Trees can grow large. This needs to be controlled, e.g. by pruning, to avoid overfitting 



#### K nearest neighbours (KNN)
- Training data: 
	![[Pasted image 20260101153927.png]]
- KNN will make a prediction for a new object $x_{new}$ based on the closest $k$ examples from the training data ("its neighbours")
	- When $k=1$, KNN predicts for $x_{new}$ the label of the closest point in the training set 
	- when $k > 1$, KNN uses a consensus mechanism to reach an agreement on the prediction. Popular choice: majority voting 
- Underlying Principle:
	- Points whose geometric representations are close are likely to be similar 
- Contrary to decision tree, KNN works in a lazy way: 
	- Learning happens only once a new object $x_{new}$ has been disclosed 
	- ![[Pasted image 20260101154313.png]]

#### Example 
- ![[Pasted image 20260101154346.png]]
- Feature vectors: hospital locations 
- Label $y \in \{$high, low$\}$
- ![[Pasted image 20260101154432.png]]
-  hospital $x_{new}$ is disclosed. What’s its label?
- KNN with $k=1$ will immediately predict green

#### KNN with $k=1$: nearest neighbour
- Rationale: the closest point is the most similar one.
- Only the nearest neighbour has a say in deciding the predicted label $\hat{y}_{new}$ for $x_{new}$ 
- What can go wrong?
	- Heavy bias on the nearest point
	- if nearest neighbour is noisy, the prediction will be noisy 

#### Example 2 
- ![[Pasted image 20260101154717.png]]
- Feature vectors: families’ locations
- y $∈${Dutch, Belgium}
- ![[Pasted image 20260101154736.png]]
- Nearest neighbour fails: it does not reflect reality faithfully 
- KNN with k = 5 gives a better representation of local structure
- ![[Pasted image 20260101154819.png]]
- Majority voting: 4/5 are "Belgium", KNN predicts "Belgium"

#### Important considerations 
- Distance (similarity) measures 
- Squared Euclidean distance: $d ^2 (x, z) = (x_1 − z_1) ^2 + (x_2 − z_2)^ 2 . . .$
- Others: Manhattan distance, Kolmogorov distance, and more.

- KNN needs Normalisation 
	- Features are typically different under very different scales
	- This can hurt prediction power, i.e. large-valued features will dominate small valued ones 
	- Trick:
		- Apply normalisation to make features comparable, e.g. rescale all features between 0 and 1

- The right value for $k$ 
	- No clear answer, "good" values for $k$ are problem dependent 
	- Small values of $k$ can give noisy predictions due to imposed bias
	- Large values of $k$ can overlook meaningful local information 
	- Large values of $k$ have computational implications 
	- Tip:
		- test different values of $k$ against accuracy on the training data, using cross-validation 



# References