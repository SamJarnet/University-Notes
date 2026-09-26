2026-09-24 10:08

Status:

Tags: [[Foundation of Machine Learning]]


# Basic Maths

#### Linear Algebra - Representing Data
- Scalar:
	- A single mumber (e.g. $c = 5$)
	- Vector: An array of numbers. Represents a single data point or a model's weights. $\mathbb{R}^d$
	- Matrix: A 2D array of numbers. Represents the entire dataset. $\mathbb{R}^{n \times d}$
#### Linear Algebra: Example
- Consider dataset to predict house prices:
	![[Pasted image 20260924103615.png]]
- In machine learning, we represent this as:
	- Feature Matrix X ($n=3$ samples, $d=2$ features)
		![[Pasted image 20260924103652.png]]
	- Target Vector y ($n=3$ targets)
		![[Pasted image 20260924103709.png]]

#### Linear Algebra: Key Operations
- Vector Dot Product
	- Measures the similarity or projection of one vector onto another
		![[Pasted image 20260924103850.png]]
	- ML Connection:
		- Fundamental to linear models, neural networks and measuring similarity (cosine similarity).
- Vector Norms (Magnitude)
	- Measures the "length" or "size" of a vector.
		- L2 Norm: 
			![[Pasted image 20260924104008.png]]
		- L1 Norm:
			![[Pasted image 20260924104016.png]]
	- ML Connection: Used in regularisation (Ridge L22, Lasso L1) to keep model weights small and prevent overfitting.
- Matrix Multiplication
	- USed to apply transformations and make preditions. A prediction for a single point $x$ with weights $w$ is a dot product:
		![[Pasted image 20260924104203.png]]
- Eigenvectors & Eigenvalues
	- For a given matrix $A$, an eigenvector $v$ is a special vector that is only scales by a scaler eigenvalue $\lambda: Av = \lambda v$.
	- ML Connection:
		- The core concept behind Principle Component Analysis (PCA) for dimensionality reduction. Eigenvectors identify the "principle axes" of the data.

#### Probability - Reasoning About Uncertainty
- ML is filled with uncertainty. We need a way to quantify it.
	- Uncertainty in the data (noise, measurement errors)
	- Uncertainty in the model (is our model a good fit for the world?)

- Key Concepts:
	- Random Variable: A variable whose value is a numerical outcome of a random phenomenon (e.g. the result of a coin flip, the height of a person)
	- Probability Distribution: A function that describes the likelihood of a random variable taking on the a certain value
		- Bernoulli: For binary events (e.g. spam/not spam)
		- Gaussian (Normal): For continuous values (e.g. height, temperature, model errors)

#### Probability - Conditional Probability & Bayes' Theorem
- Conditional Probability:
	- The probability of an event occuring, given that another event has already occured.
		![[Pasted image 20260926124940.png]]
- Bayes' Theorem:
	- Flips conditional probability around. Hugely important in ML.
		![[Pasted image 20260926125014.png]]
	- $P(A|B)$: Posterior (what we want to know)
	- $P(B|A)$: Likelihood (how data relates to the event)
	- $P(A)$: Prior (our initial belief)
- ML connection:
	- The basis for the Naive Bayes Classifier and Bayesian inference.

#### Statistics: The Likelihood Function
- A critical concept for training models
	- We have a model with parameters $\theta$
	- We have observered data $D = \{X,y\}$ 

- Maximum Likelihood Estimation (MLE) 
	- A core principle in statistics and ML
		- "Find the parameters $\theta$ that make the observed data most likely"
	- This turns model training into an optimisation problem: find $\theta$ that maximises $L(\theta | D)$ 

#### Calculus 
- How do we actually find the parameters $\theta$ that maximise likelihood or miminise error?
	- We define a Cost Function (or Loss Function) $J(\theta)$ that measures how "bad" our model is.
	- For example the Mean Squared Error in regression
	- Our goal: Find the $\theta$ that results in the minimum cost.
		![[Pasted image 20260926125718.png]]
- Calculus gives us the tools to find this minimum

#### Calculus: Derivatives and the Gradient
- The Derivative: $\frac{dJ}{d\theta}$
	- Measures the slope of the cost function at a specific point $\theta$. It tells us how the cost changes if we "nudge" the parameter a tiny bit.
		- Positive slope: Increasing $\theta$ increases the cost.
		- Negative slope: Decreasing $\theta$ decreases the cost
		- Zero slope: We are at a minimum, maximum, or saddle point
- The Gradient: $∇J(\theta)$ 
	- A vector of all the partial derivatives. For a model with many parameters $(\theta_1, ..., \theta_n)$
		![[Pasted image 20260926130052.png]]
- Key Intuition:
	- The gradient vector always points in the direction of the steepest ascent of the cost function.

#### Calculus: Optimisation with Gradient Descent
- If the gradient points "uphill", we can find the minimnum by taking small steps "downhill"
	![[Pasted image 20260926130204.png]]
- The Gradient Descent Algorithm
	- 1. Initialise parameters $\theta$ randomly
	- 2. Repeat until convergence:
		- Compute the gradient $∇J(\theta)$ 
		- Update the parameters by taking a step in the opposite direction of the gradient:
			- $θ := θ − α∇J(θ)$ 
	- $\alpha$ is the learning rate, a small number that controls the step size.

#### Tying it all together: A preview of Linear Regression
- How do the three pillars build our first model?
	- The model (linear algebra):
		- We define our prediciton. A line is a weighted sum of features.
			- $\hat{y} = w_1x_1 + w_2x_2 + · · · + w_nx_n ⇒ \hat{y} = Xw$
	- The objective (probability):
		- We want the best weights $w$. We assume the erros are Gaussian and use Maximum Likelihood Estimation to find the most plausible $w$ given our data.
	- The algorithm (calculus):
		- It turns out that miximising the likelihood is the same as minimising a cost function: The Mean Squared Error. We find the best $w$ by using Gradient Descent to walk down the error surface to the minimum point.
			- $w := w − α∇J(w)$



# References