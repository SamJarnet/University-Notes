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
# References