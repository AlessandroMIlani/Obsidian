- we can see the N.N. like ablack box or a function
	- we put some input, adn get some output
	
## general scheme
![[Pasted image 20210717155723.png]]
- we have an input layer
	- ex. if we have an image (28x28 pixel -> 784pixel) we need an input neuron for eatch pixel (for this example -> 284 input neurons)
- we can design the output layer on some diffente way
	1. ex. if we have 2 possible output classes, we can choose to have 0 or 1 like the 2 possible putput from the N.N. (ex. if we get 0.4 -> approximate to 0 and 0.7-> to 1)
	1. we can have more output neurons and they can have a value between 0 and 1, whit a sum =1 --> it's sound like a probability distribution
- **Between** we have the hidden layers
-  evry node is connect to the next layer with sometihing called weights
	- if every node is connet to every node of the next layer, we call it a densy connect layer  
	- every weights have a numeric value
- we can have *Bias*
	- particulary node connet to che next layer
	- they not have an input
	- the contain a trainable constant.
		- at start they contain the value 1 
		
		
![[Pasted image 20210717161030.png]]

## How work
- we chose an example: have same point whit coordinates (x,y,z) and they can stay on cluste red or blue
	- 3 input x,y,z 
	- 1 output neuron 0=red 1=blue 
- the hidden layer?
	- every node make the weighted sum of every node connect to them $N_1=\sum^{n}_{i=0}W_iX_i+b$
	- at start weights are complety random and change during the training
	- ps. the baias is also a pice of the sum  

[[Activation Functions & Training]]