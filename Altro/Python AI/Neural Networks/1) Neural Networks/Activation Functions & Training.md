- during the first execution, we can't garante an output in the range (ex. we expect an output beween 0-1 but we can get 43, or -2.34)
	 - we use*** Activation Function*** to compense that
	 	- **Relu** (Rectified Linear Unit)
	 		- every vale <0 is equale to 0, evry vale >0 is hitset 
	 	- **Tanh** (Hyperbolic Tangent)
	 		- limit the value between -1 and 1 
		- **Sigmoid** (Squishy fire function)
			- limit the valuse between 0 and 1  ($\phi(z)=\frac{1}{1+e^{-z}}$)
	- we  apply Activation Function after every weighted sum for get a coerent output

## Training
- we give input and expected output like other case
	- at the firsts tests, the output can be complety wrong, but how much wrong?
		- we have the **loss** function to calculate that (how ware away is the output)
			- if loss is high, we need to tweak our weight and bias more in a different direvtion
			- if loss is low, we have get a good output, so we tweak weight and bias a only bit 
		- Exemple of Loss function
					1. Mean Squared Error
					2. Mean Absolute Error
					3. Hinge Loss 

		### Gradient Descent
 - is the algorithm used to find the optimal paramaters for our network
		![[Pasted image 20210717165207.png]]
- this is how a N.N. function look like

We're atring to optimize this loss function as low as possible, that means we should have a better nureal network

- We are looking for the global minimum value
	- the algorithm Gradient Descent is what tell us what direction we need to move  our function for find the minimum value
	- It work whit the *backpropagation* algorithm which go back through the Network and update the Weights and biases

## Optimizer
it's the function that implemente the backpropagation algorithm described above.
There are few version
- Gradient Descent
- Stochastic Gradinet Descent
- Mini-Batch Gradient Descent
- Momentum
- Nesterov Accelerated Gradient

[[Creating a N.N.]]