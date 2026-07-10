2026-01-01 16:14

Status:

Tags: [[Artificial Intelligence]]


# Machine Learning Part 3

#### The classification task
- Algorithms who learn a classification rule: 
	- $h(x) = \hat{y}$
- We hope that $\hat{y} = y$ 

#### Many important classifiers are parametric
- We look for optimal parameters
	![[Pasted image 20260101165736.png]]
- A class of classifiers that are simple and effective:
	- For an object $x$ 
		- $h(x) = w ⊤ x + b$ 
		- $w$ and $b$ are the parameters.
		![[Pasted image 20260101165852.png]]

#### Examples of linear classifiers
- Logistic regression
- halfspaces
- support vector machines - no kernels 

#### The perceptron: a linear classifier
- A simple and elegant method for linear binary classification 
- Perceptron rule:
	- First run: randomise weights 
		- For each training example (x, y):
			![[Pasted image 20260101170046.png]]
- The perceptron updates its parameters only when a training example is misclassified
- If the predicted label does not match the true label, the algorithm adjusts the weight vector and bias in the direction that would correctly classify the current example 
- This update incrementally shifts the decision boundary, improving the classifier's ability to separate the two classes. 
 - ![[Pasted image 20260101170312.png]]
	 - Works well
 - ![[Pasted image 20260101170331.png]]
	 - Doesn't work well 

- Only works on linearly-separable data
- Observation: Real-world data are often non-linear 
- Trick:
	- Space warping
		- Apply non-linear transformations to the input data 
		- Classify the transformed data

#### Example 
- ![[Pasted image 20260101170555.png]]
- Linear transformations do not help much
	- ![[Pasted image 20260101170602.png]]
- Data remains non-separable in the feature space
	- This is why the perceptron fails 
- Non-linear transformations work
	- ![[Pasted image 20260101170707.png]]
- left side - 
	- linear classifier in feature space gives nonlinear classifier in original space
- right side- 
	- points are linearly separable in feature space
- Now the linear classifier in feature space is a non-linear classifier in the input space

#### Biological Neuron 
- Receives multiple stimuli, transmits signals to other neurons
-  Performs highly complex non-linear transformations of their input stimuli 
- Complex behaviour 
- Artificial neurons are a simplified abstraction
	![[Pasted image 20260101171045.png]]
- A neuron is a computing unit 
- It receives input data along with weights 
- Performs a weighted sum (linear operation)
- Applies a non-linear activation function, which may or not fire up the neuron

#### Architecture: Multi-Layer Perceptron (MLP)
- Each neuron in an MLP behaves like a perceptron, but instead of using simple threshold decision it applies nonlinear activation function to its weighted sum
- The neurons are grouped in layers, each of which players one of three roles 

- One input layer (blue)
- Two (or more) hidden layers (black)
- one decision layer (green)
	![[Pasted image 20260101171339.png]]

#### A popular activation function
![[Pasted image 20260101171412.png]]
- If the weighted sum is positive, the neuron activates and passes this value to the next layer
#### Training MLP 
- Set all weights $w_i$ to random values
- for each training pair (x, y) in the training set, pass the object x through the network 
	- each feature j of x goes to one neuron in the input layer
- The network applies the operations in the hidden layers (weighted sum + non-linear transformation)
- ![[Pasted image 20260101171640.png]]
- Make a prediction for y 
- ![[Pasted image 20260101171710.png]]
- Compute the Loss
	- The loss is a function that quantifies the discrepancy between the model's prediction and the true label 
	- ![[Pasted image 20260101171750.png]]
- Perform Back-Propagation and weights updates 
	- Crucial step: compute the gradient of the loss with respect to the model parameters (weights and biases), and propagate it backward through the network to update them 
- The main goal is adjusting the weights and biases 
- The process is repeated for every other training point
	- By repeatedly performing forward and backward passes, the network can automatically adjust its parameters to reduce the loss.
	![[Pasted image 20260101171951.png]]

#### Effect of adding more neurons 
- More units/layers, better fit the training data but...
- enlarging the architecture can lead to overfitting and computational bottlenecks 
- ![[Pasted image 20260101172107.png]]

#### Considerations
- Number of neurons in the input layer needs to match the number of features in the training set
- Number of neurons in the decision layer depends on the task, e.g. three neurons if we have 3 classes 
- Number of neurons in the hidden layer can be arbitrary 
- Back propagation computes and propagates the changes in weights. The updates are done via an optimiser:
	- Stochastic gradient descent 

#### Convolutional Neural Networks
- CNN is an architecture designed for structured data, e.g. images, audio, video
- Replace dense layers with convolutional filters:
	- Filters detect local patters (edges, curves, textures)
	- Filters are applied to the full image via weights sharing
- Capture spacial hierarchy: early layers learn simple features, deep layers learn complex and abstract objects
- Implementing pooling layers: layers that summarise important features, making the learning strong against variances, perturbations, noise, etc 


#### Recurrent Neural Networks 
- RNN is an architecture designed for sequential data
- Maintain hidden memory, designed for long-running training sequences
- A RNN can model temporal dependencies (while MLP and CNN cannot) 
- The hidden memory from one time step back is fed back into the next step along with the new input, allowing the network to keep memory of past information 
- Powerful for applications such as language modelling, translation, speech recognition 



# References