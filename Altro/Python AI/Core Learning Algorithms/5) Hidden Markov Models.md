The Hidden Markov Model is a finite set of states, each of which is associated with a (generally multidimensional) probability distribution.
Transitions among the states are governed by a set of probabilities called transition probabilities.

- Work with probability to predic future states

## Data 
- we are interested in probability distribution of the data
	- we can have that at the start or we can extrapolate than from a data set 

### Component of Markov model
- **States**: we have a finite numeretion of states [ cold/warm, a/b/c/../z]
- **Observation**: eatch state has a particular outcome or observation  with it based on a probability distribution [ex. hot day -> 80% to be happy | cold day -> 20% to be happy]
- **Transitions**: probability to transitioning to a different state [_a cold day has a 30% chance of being followed by a hot day and a 70% chance of being follwed by another cold day_ ]

## Import setup
```python
import tensorflow_probability as tfp # We are using a different module from tensorflow this time
import tensorflow as tf
```

## Weather model
-we given at the model the following information:
1.  Cold days are encoded by a 0 and hot days are encoded by a 1.
2.  The first day in our sequence has an 80% chance of being cold.
3.  A cold day has a 30% chance of being followed by a hot day.
4.  A hot day has a 20% chance of being followed by a cold day.
5.  On each day the temperature is normally distributed with mean and standard deviation 0 and 5 on a cold day and mean and standard deviation 15 and 10 on a hot day.

```python
tfd = tfp.distributions # making a shortcut for later on
initial_distribution = tfd.Categorical(probs=[0.2, 0.8]) # Refer to point 2 above
transition_distribution = tfd.Categorical(probs=[[0.5, 0.5], [0.2, 0.8]]) # refer to points 3 and 4 above
observation_distribution = tfd.Normal(loc=[0., 15.], scale=[5., 10.]) # refer to point 5 above
# the loc argument represents the mean and the scale is the standard devitation
```
- We've created distribution variables to model our system
   - now we can create the model

```python
model = tfd.HiddenMarkovModel(initial_distribution=initial_distribution, 
transition_distribution=transition_distribution, 
observation_distribution=observation_distribution, num_steps=7)
```
- *steps* --> number of day that i would like to predict
- To get the **expected temperatures** on each day we can do the following.

```python
mean = model.mean() 

# due to the way TensorFlow works on a lower level we need to evaluate part of the graph
# from within a session to see the value of this tensor

# in the new version of tensorflow we need to use tf.compat.v1.Session() rather than just tf.Session()
with tf.compat.v1.Session() as sess: 
 print(mean.numpy())
```
[[Neural Network intro]]