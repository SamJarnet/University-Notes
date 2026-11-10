2026-11-10 10:44

Status:

Tags: [[Foundation of Machine Learning]]


# Multi-Layer Perceptrons

#### The Multilayer Perceptron (MLP)
- Input layer: $d$ input units, no computation - each simply emits $x_i$.
- Hidden Layer(s): neurons with a non-linear activation.
- Output Layer: $c$ neurons; $c$ and the activation depend on the task.
- Fully Connected: Every unit feeds every unit in the next layer.
- Example: a 4-5-2 network.
	![[Pasted image 20261110104717.png]]
- Convention: we count layers of weights, so a 4-5-2 network has $L=2$ layers
	![[Pasted image 20261110105556.png]]

#### MLP: Formal Definition (Forward Pass)
- For layers $ℓ = 1, ..., L$ with $n_ℓ$ units each ($n_0 = d, n_L = c$):
	![[Pasted image 20261110105713.png]]
- Shapes: 
	![[Pasted image 20261110105813.png]]
- Entry $W_{jk}^{(ℓ)}$ is the weight from unit $k$ in layer $ℓ  - 1$ to unit $j$ in layer $ℓ$
- Hidden layers typically share one $\sigma$; the output layer's $\sigma^{(L)}$ is chosen for the task/
- parameter count of layer $ℓ: n_ℓ(n_{ℓ -1}+1)$

#### Activation Functions
- Why Non-Linear Activations?
- Suppose every activation is the identity, $\sigma(z) = z$. Then for two layers.
	![[Pasted image 20261110110755.png]]
	- A stack of linear layers is still a single linear map, however deep.
	- So it still cannot solve XOR. Non-linearity is what gives depth its power
- Activation Function:
	- Map a unit's pre-activation $z$ to its output $a=\sigma(z)$
	- Must be non-linear and for gradient-based training, (almost everywhere) differentiable
	- Hidden layers: ReLU (default today), tanh, sigmoid
	- Output layer: identity (regression), sigmoid (binary), softmax (multi-class)
	- Sigmoid and tanh are "squashing" (bounded); ReLU is not. Softmax acts on the whole vector $z$, not elementwise

#### Logistic (Sigmoid) Activation
- Range (0, 1): interpretable as a probability
- Smooth , monotonic
- $\sigma'(z) \leq 0.25$  and $\rightarrow 0$ for large $|z|$:
	- saturation slows learning 
	![[Pasted image 20261110111627.png]]
	![[Pasted image 20261110111633.png]]

#### Hyperbolic tangent (tanh)
- Range (-1, 1), zero-centred.
- also saturates for large $|z|$ 
	![[Pasted image 20261110111729.png]]![[Pasted image 20261110111733.png]]

#### Rectified Linear Unit (ReLU)
- Range $[0, ∞)$; cheap to compute
- Does not saturate for $z > 0 \Rightarrow$ faster training of deep networks
- Units stuch at $z<0$ get zero gradient ("dead ReLUs")
- Not differentiable at 0; in practice use 0 or 1 there
	![[Pasted image 20261110111931.png]]
	![[Pasted image 20261110111938.png]]
#### Softmax (Output Layer)
- Converts logits $z \in \mathbb{R}^K$ into a probability distribution:
	![[Pasted image 20261110112056.png]]
- Derivative (full Jacobian):
	![[Pasted image 20261110112107.png]]
	
	![[Pasted image 20261110112116.png]]

#### Cost Function: Mean Squared Error
- From $M$ data points:
	![[Pasted image 20261110112207.png]]
- The natural choice for regression (identity output)
- The constant $1/2M$ is sometimes $1/2$ or $1/M$; it only rescales the gradient
- With a sigmoid output, $\partial J/ \partial z = (y-t) \sigma'(z)$: if the unit is saturated and confidently wrong, $\sigma'(z) \approx 0$, so learning is slow

#### Cross-Entropy Cost Function
- Binary (sigmoid output, $t \in \{0, 1\}$):
	![[Pasted image 20261110112445.png]]
- Multi-class (softmax output, one-hot $t$):
	![[Pasted image 20261110112509.png]]
	- $J \geq 0$ and $J \rightarrow 0$ as predictions approach the targets
	- For sigmoid + binary CE, and for softmax + multi-class CE:
		![[Pasted image 20261110112623.png]]
	- The $\sigma'$ factor cancels, so a confidently wrong output still learns quickly


#### Choosing the Output Layer and Loss![[Pasted image 20261110112725.png]]


#### Gradient Descent
- Minimise $J(w)$ by repeatedly stepping against the gradient (the direction of steepest descent): 
	- $w \leftarrow \eta ∇_wJ(w)$
- Types of GD:
	- Batch GD: gradient over all $M$ examples per step
	- Stochastic GD: gradient of one example per step (noisy, cheap)
	- Mini-batch GD: average over $B$ examples - the standard in practice
	- $\eta$ too small $\Rightarrow$ slow; too large $\Rightarrow$ oscillation or divergence
- How to compute:
	- To use gradient descent we need $∂J/∂W^{(ℓ)}_{jk}$ for every weight
		- Forward pass: compute all $z^{(ℓ)}$, $a^{(ℓ)}$ and the loss $J$
		- Forward pass: propagate $∂J/∂z^{ (ℓ)}$ from the output back to the input using the chain rule - backpropagation 
- 