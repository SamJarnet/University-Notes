2026-11-03 15:36

Status:

Tags: [[Computer Vision]]


# Machine learning for Pattern Recognition

#### Computer Vision Machine Learning
- Many computer vision applications involving machine learning take the following form:
	- Image goes in -> Feature Extractor -> Machine Learning 
		- Feature Extactor: where the image processing happens - makes feature vectors from images
		- Machine Learning: system uses feature vectors to make intelligent decisions

#### Key Terminogoly
- Feature vector:
	- a list of (usually real) numbers
	- has a fixed number of elements in it
		- the number of elements is the dimensionality of the vector
	- represents a point in a feature space or equally a direction in the feature space
	- the dimensionality of a feature space is the dimensionality of every vector within it
		- vectors of differing dimensionality can't exist in the same feature space

#### Simple feature vectors
- Example of Pickachu image
- Dimensions of the image
	- (256, 274, 3) (Height, Width, Channel)
- Colour mean
	- (51, 83, 95) (Blue, Green, Red)
- Mean and standard Deviation
	- (51, 83, 95) (62.43, 101.1, 114.51)
- Colour histogram
	- 3 x 256 or 256$^3$ vector

#### Distances in feature space
- Feature extractors are often defined so that they produce vectors that are close together for similar inputs
	- Closeness of two vectors can be computed in the feature space by measuring a distance between the vectors.
- Euclidian distance (L2) is the most intuitive distance
	- The straight line distance between two points
	- Compter via an extension of Pythagoras theorem to $n$ dimensions:
		![[Pasted image 20261105174503.png]]
- L1 distance is computed along paths parallel to the axes of the space
	![[Pasted image 20261105174535.png]]
- Cosine similarity measures the cosine of the angle between two vectors
	- It is not a distancce
	![[Pasted image 20261105174603.png]]
	- Useful if you don't care about the relative length of the vectors

#### Choosing Good Feature Vector Representations For Machine Learning
- Choose features which allow to distinguish objects or classes of interest
	- Similar within classes
	- Difference between classes 
- Keep number of features small
	- Machine learning can get more difficult as dimensionality of feature space gets large

#### Supervised Machine Learing: Classification 
- Classification is the process of assigning a class label to an object
- A supervised machine learning algorithm uses a set of pre-laballed training data to learn how to assign class labels to vectors (and the corresponding objects)
	- A binary classifier only has two classes
	- A multiclass classifier has many classes

#### Linear Classifiers
- Linear classifiers try to learn a hyperplane that separates two classes in featurespace with minimum error
- There are lots of of hyperplanes to choose from. Different linear classification algorithms apply differing constraints when learning the classifier
- To classify a new image you just need to check which side of the hyperplane it is on

#### Non-Linear Binary Classifiers
- Linear classifiers work best when the data is linearly separable.
- There can be outliers.
	- False positive / False negative
- Non-Linear binary classifiers, such as Kernel Support Vector Machines learn non-linear decision boundaries
- You have to be careful, you might lose generality by overfitting

#### Multiclass classifiers: kNN
- Assign class of unknown point based on majority class of closest $K$ neighbours in feature space
- $K$: even number is not a good idea
	- Tie Breaker: Random or Nearest
- Computationally expinsive if there are:
	- lots of training examples
	- many dimensions

#### Multiclass Linear Classifiers
- A linear classifier is by definition binary
- How can we solve multiclass problems with linear classifiers?
	- One versus All (OvA)/One versus Rest (OvR)
		- One classifier per class
	- One versus One (OvO)
		- $K(K-1)/2$ classifiers
	- Check the confidences (distances) and choose the highest one 

#### Unsupervised Machine Learning: Clustering
- Clustering aims to group data without any prior knowledge of what the groups should look like or contain
- In terms of feature vectors, items with similar vectors, items with similar vectors should be grouped together by a clustering operation
- Some clustering operations create overlapping groups; for now we're only interested in disjoint clustering methods that assign an item to a single group.

#### K-Means Clustering
- K-means is a classic featurespace clustering algorithm for grouping data into $K$ groups with each group represented by a centroid:
	- The value of $K$ is chosen
	- $K$ initial cluster centres are chosen
	- Then the following process is performed iterativelly until the centroids don't move between iteration:
		- Each point is asign to its closest centroid 
		- The centroid is recomputed as the mean of all the points assigned to it. If the centroid has no points assigned it is randomly re-initialised to a new point



