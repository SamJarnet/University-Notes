2026-11-05 21:32

Status:

Tags: [[Computer Vision]]


# Coviariance and Principal Components

#### Random Variables and Expected Values
- Mathematicians talk variance (and covariance) in terms of random variables and expected values
- The expected value (denoted $E[X]$) is the most likely value a random variable will take
	- We will assume that the values an element of a feature can take are all equally likely
		- The expected value is just the mean value

#### Variance
- Variance ($\sigma^2$) is the mean squared difference from the mean ($\mu$).
	![[Pasted image 20261105213547.png]]
- It is a measure of how spread out the data is
- It is $E[(X-E[X])^2]$ 

#### Covariance
- Covariance ($\sigma(x,y)$) measures how two variables change together
	![[Pasted image 20261105213706.png]]
- It is $E[(x - E[x])(y-E[y])]$
- The variance is the covariance when the two variables are the same
- Covariance is related to correlation
	![[Pasted image 20261105213746.png]]
- A covariance matrix encodes how all possible pairs of dimensions in an $n$-dimensional dataset vary together.
	![[Pasted image 20261105213911.png]]
- The covariance matrix is the square symmetric matrix
	![[Pasted image 20261105214004.png]]

#### Mean Centring
- Mean Centring is the process of computing the mean (across each dimension independently) of a set of vectors and then subtracting the mean vector from every vector in the set.
	- All the vectors will then be translate so their average position is the origin
	![[Pasted image 20261105214215.png]]

#### Basis 
- A basis is a set of $n$ linearly independent vectors in an $n$ dimensional space
	- The vectors are orthogonal
	- The form a "coordinate system" 
	- There are an infinite number of possible basis

#### The Principle Axes of Variation
- For a given set of $n$ dimensional data, the first principle axes (or just principle axes) is the vector that describes the direction of greatest variance
- The second principle axes is a vector orthogonal (perpendicular) to the first major axis
- In a space with 3 or more dimensions, the second principle axes is the direction of the second greatest variance orthogonal to the first principle axes
	- The set of $n$ principle axes of an $n$ dimensional space are a basis

#### Eigenvectors and Eigenvalues
![[Pasted image 20261105214718.png]]
- There are at most $n$ eigenvector-eigenvalue pairs
- If $A$ is symmetric, then the set of eigenvectors is orthogonal
- If $A$ is the covariance matrix, then the eigenvectors are the princapal axes
- The eigenvalues are proportional to the variane of the data along each eigenvector 
- The eigenvector corresponding to the largest eigenvalue is the first P.C.

#### Finding the Eigenvectors and Eigenvalues
- For small matrices $n \leq 4$ there are algebraic solutions to finding all the eigenvector-eigenvalue pairs
- For larger matrices, numerical solutions to the Eigendecomposition must be sought
- Eigendecomposition:
	![[Pasted image 20261106121811.png]]
- If $A$ is real symmetric (i.e. a covariance matrix), then $Q^{-1} = Q^T$ (i.e. eigenvectors are orthogonal), so:
	![[Pasted image 20261106121902.png]]
- Therefore, $A=Q𝚲Q^T$ gives you the principle axes and their relative magnitudes

#### Ordering
- Standard Eigendecomposition implementations will order the eigenvectors (columns of $Q$) such that the eigenvalues (in the diagonal of $𝚲$) are sorted in order of decreasing value
	- Some solvers are optimised to only find the top $k$ eigenvalues and corresponding eigenvectors, rather than all of them
	![[Pasted image 20261106123710.png]]

#### Linear Transform
- A linear transform $W$ projects data from one space to another:
	- $T=ZW$
		- Original data is stored in the rows of $Z$
	- $T$ can have fewer dimensions than $Z$
- The effects of a linear transorm can be reversed if $W$ is invertible:
	- $Z= TW^{-1}$
		- A lossy process if the dimensionality of the spaces is different

#### Principal Component Analysis (PCA)
- PCA is an Orthogonal Linear Transform that maps data from its original space to a space defined by the principle axes of the data.
	- The transform matrix $W$ is just the eigenvecotr matrix $Q$ from the Eigendecomposition of the covariance matrix of the data.
	- Dimensionality reduction can be achieved by removing the eigenvectors with low eigenvectors from $Q$ (i.e. keeping the first $L$ columns of $Q$ assuming the eigenvectors are sorted by decreasing eigenvalue).
- The algorithm:
	- 1. Mean-Centre the data vectors
	- 2. Form the vectors into a matrix $Z$, such that each row corresponds to a vector
	- 3. Perform the Eigendecomposition of the matrix $Z^TZ$, to recover the eigenvector matrix $Q$ and diagonal eigenvalue matrix $Λ: Z^TZ = QΛQ^T$
	- 4. Sort the columns of $Q$ and corresponding diagonal values of $Λ$ so that eigenvalues are decreasing. 
	- 5. Select the $L$ largest eigenvectors of $Q$ (the first $L$ columns) to create the transform matrix $Q_L$.
	- 6. Project the original vectors into a lower dimensional space, $T_L:T_L = ZQ_L$ 

#### Eigenfaces (Eigenimages)
- Simple feature:
	![[Pasted image 20261106124721.png]]
- not invariant to:
	- change in position/orientation/scale of the object in the image
	- Changes in lighting
	- size of the image
- highly susceptible to image noise
- Making it invariant
	- Require (almost) the same object pose across images (i.e. full frontal faces)
	- Align (rotate, scale and translate) the images so that the common feature is in the same place (i.e. the eyes in a set of face images)
	- Make all the aligned images the same size
	- (optional) normalise (or perhaps histogram equalise) the images so they are invariant to global intensity changes
- Problem: the feature vectors are huge,
	- if the images are 100x200 pixels, the vector has 20000 dimensions
	- the feature vectors are still highly susceptible to imaging noise and variations due to the slight misalignments.
- Solution: apply PCA,
	- PCA can be used to reduce the dimensionality 
		- smaller number of dimensions allow greater robustness to noise and misalignment
			- there are fewer degrees of freedom, so noise/misalignment has much less effect
			- and the dominant features are captured
		- Fewer dimensions makes applying machine-learning much more tractable
