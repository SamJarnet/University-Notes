2026-10-06 12:36

Status:

Tags:  [[Foundation of Machine Learning]]


# Logistic Regression

#### Definition
- Logistic regression is a widely used discriminative classification model
- It models the probability of a class label $y$ given an input vector $x$, written as $p(y|x; \theta)$
- The parameters of the model are represented by $\theta$.
- It's a foundational method for classification tasks and serves as a building block for more complex models like neural networks
- Binary Logistic Regression
	- Used when there are two classes ($C=2$), e.g. spam/not-spam
- Multinomial logistic Regression
	- Used when there are more than two classes ($C>2$), e.g. cat/dog/bird

#### The need for probability
- Linear regression outputs a continuous value, e.g. $y = w^Tx + b$
- This output can be any real number (-inf, inf), which is not suitable for classification
- We want a probability: value between 0 and 1
- Goal map linear output to valid probability with a squashing function

#### Sigmoid (Logistic) Function
- Sigmoid squashed perfectly
	![[Pasted image 20261006124605.png]]
- Maps 

