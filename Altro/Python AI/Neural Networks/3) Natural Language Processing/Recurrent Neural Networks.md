#### Simple Recurrent Layer
- type of network we use whit text data
- **it contain an internal loop**
	- it process data on diffent moments and have internal memory and state 
	- it diden't process all data at onace, but process one word at a time while maintaining an internal memory of what it's already seen.
		-  This will allow it to treat words differently based on their order in a sentence and to slowly build an understanding of the entire input, one word at a time.

![[Pasted image 20210720232903.png]]

$h_t$ = output at time t |  $x_t$ input at time t | A = Recurrent Layer (loop)

- this layer is very usefull, but have a problem
	- In very long phrase (100 or 150 words) the value of firsts words become irrelevants, beacuse them pass trowh too much other value and the networks

## LSTM (long-short memory)
- Work very similar to a simple RNN payer, but add another component
	- adds a way to access inputs from **any timestep** in the past
	- This allows for us to access any previous value we want at any point in time
		- This adds to the complexity of our network and allows it to discover more useful relationships between inputs and when they appear. 

## Sentiment Analysis
- now time to see a recurrent neural network in action
- For this example, we are going to do something called sentiment analysis
	- from **Wikipedia**: "_the process of computationally identifying and categorizing opinions expressed in a piece of text, especially in order to determine whether the writer's attitude towards a particular topic, product, etc. is positive, negative, or neutral_" 

####  Movie Review Dataset
- we load in the IMDB movie review dataset from keras
	-  This dataset contains 25,000 reviews from IMDB where each one is already preprocessed and has a label as either positive or negative
```python
from keras.datasets import imdb
from keras.preprocessing import sequence
import keras
import tensorflow as tf
import os
import numpy as np
  
VOCAB_SIZE = 88584  

MAXLEN = 250
BATCH_SIZE = 64  

(train_data, train_labels), (test_data, test_labels) = imdb.load_data(num_words = VOCAB_SIZE) 

# Lets look at one review
train_data[1]
```

### More Processing
- If we have a look at some of our loaded in reviews, we'll notice that they are different lengths
	- This is an issue. We cannot pass different length data into our neural network 
		-   if the review is greater than 250 words then trim off the extra words
		-   if the review is less than 250 words add the necessary amount of 0's to make it equal to 250. 
```python
train_data = sequence.pad_sequences(train_data, MAXLEN)
test_data = sequence.pad_sequences(test_data, MAXLEN)
```

### Creating the Model
-  We'll use a word embedding layer as the first layer in our model and add a LSTM layer afterwards that feeds into a dense node to get our predicted sentiment
```python
model = tf.keras.Sequential([
 		tf.keras.layers.Embedding(VOCAB_SIZE, 32),
 		tf.keras.layers.LSTM(32),
 		tf.keras.layers.Dense(1, activation="sigmoid")
		])

model.summary()
```

### Training
- time to compile and train the model.
```python
model.compile(loss="binary_crossentropy",optimizer="rmsprop",metrics=['acc']) 

history = model.fit(train_data, train_labels, epochs=10, validation_split=0.2)
```
- evaluate the model on our training data to see how well it performs
```python
results = model.evaluate(test_data, test_labels)
print(results)
```

## Making Predictions
- Now let’s use our network to make predictions on our own reviews
- Since our reviews are encoded well need to convert any review that we write into that form so the network can understand it
```python
word_index = imdb.get_word_index() 

def encode_text(text):
	 tokens = keras.preprocessing.text.text_to_word_sequence(text)
	 tokens = [word_index[word] if word in word_index else 0 for word in tokens]
	 return sequence.pad_sequences([tokens], MAXLEN)[0]  

text = "that movie was just amazing, so amazing"
encoded = encode_text(text)
print(encoded)
```
---

```python
# while were at it lets make a decode function
  
reverse_word_index = {value: key for (key, value) in word_index.items()}  

def decode_integers(integers):
	 PAD = 0
	 text = ""
	 for num in integers:
	 	if num != PAD:
	 		text += reverse_word_index[num] + " "  
	 return text[:-1]

print(decode_integers(encoded))
```
---

```python
# now time to make a prediction  

def predict(text):
	 encoded_text = encode_text(text)
	 pred = np.zeros((1,250))
	 pred[0] = encoded_text
	 result = model.predict(pred) 
	 print(result[0])
  
positive_review = "That movie was! really loved it and would great watch it again because it was amazingly great"
predict(positive_review)
  
negative_review = "that movie really sucked. I hated it and wouldn't watch it again. Was one of the worst things I've ever watched"
predict(negative_review)
```

## RNN Play Generator
- We are going to use a RNN to generate a play
- We wil show at RNN an example of something we want it to recreate and it will learn how to write a version of it on its own
 #### import
 ```python
from keras.preprocessing import sequence
import keras
import tensorflow as tf
import os
import numpy as np
 ```
 
 #### Dataset
 - we only need one peice of training data
 ```python
 path_to_file = tf.keras.utils.get_file('shakespeare.txt', 'https://storage.googleapis.com/download.tensorflow.org/data/shakespeare.txt')
 ```
 
 #### Loading your own Data
 - we need to import a file (this is for google colab )
 ```python
from google.colab import files
path_to_file = list(files.upload().keys())[0]
 ```
 
 #### Read Contents of File
 ```python
 # Read, then decode for py2 compat.
text = open(path_to_file, 'rb').read().decode(encoding='utf-8')
# length of text is the number of characters in it
print ('Length of text: {} characters'.format(len(text)))

# Take a look at the first 250 characters in text
print(text[:250])
 ```
 #### Encoding
- Since this text isn't encoded yet well need to do that ourselves. We are going to encode each unique character as a different integer

 ```python
 vocab = sorted(set(text))
# Creating a mapping from unique characters to indices
char2idx = {u:i for i, u in enumerate(vocab)}
idx2char = np.array(vocab)  

def text_to_int(text):
 	return np.array([char2idx[c] for c in text])  

text_as_int = text_to_int(text)


vocab = sorted(set(text))
# Creating a mapping from unique characters to indices
char2idx = {u:i for i, u in enumerate(vocab)}
idx2char = np.array(vocab)

def text_to_int(text):
 	return np.array([char2idx[c] for c in text])  

text_as_int = text_to_int(text)
  ```
  - And here we will make a function that can convert our numeric values to text
```python
def int_to_text(ints):

 try:
 	ints = ints.numpy()
 except:
 	pass
 return ''.join(idx2char[ints])  

print(int_to_text(text_as_int[:13]))
```
#### Creating Training Examples
- we need to split our text data from above into many shorter sequences that we can pass to the model as training examples
	- The training examples we will prepapre will use a _seq_length_ sequence as input and a _seq_length_ sequence as the output where that sequence is the original sequence shifted one letter to the right. For example:
	`input: Hell | output: ello` 
	
- Our first step will be to create a stream of characters from our text data.
```python
seq_length = 100 # length of sequence for a training example
examples_per_epoch = len(text)//(seq_length+1)
  
# Create training examples / targets
char_dataset = tf.data.Dataset.from_tensor_slices(text_as_int)
```
- Next we can use the batch method to turn this stream of characters into batches of desired length
 
```python
sequences = char_dataset.batch(seq_length+1, drop_remainder=True)
```
- Now we need to use these sequences of length 101 and split them into input and output
```python
def split_input_target(chunk): # for the example: hello
	 input_text = chunk[:-1] # hell
	 target_text = chunk[1:] # ello
	 return input_text, target_text # hell, ello
  
dataset = sequences.map(split_input_target) # we use map to apply the above function to every entry


for x, y in dataset.take(2):
	 print("\n\nEXAMPLE\n")
	 print("INPUT")
	 print(int_to_text(x))
	 print("\nOUTPUT")
	 print(int_to_text(y))
```
- Finally we need to make training batches.
```python
BATCH_SIZE = 64
VOCAB_SIZE = len(vocab) # vocab is number of unique characters
EMBEDDING_DIM = 256
RNN_UNITS = 1024  

# Buffer size to shuffle the dataset
# (TF data is designed to work with possibly infinite sequences,
# so it doesn't attempt to shuffle the entire sequence in memory. Instead,
# it maintains a buffer in which it shuffles elements).
BUFFER_SIZE = 10000

data = dataset.shuffle(BUFFER_SIZE).batch(BATCH_SIZE, drop_remainder=True)
```

## Building the Model
-  use an embedding layer a LSTM and one dense layer that contains a node for each unique character in our training data
	-  The dense layer will give us a probability distribution over all nodes (we have 1 node for eatch char)

```python
def build_model(vocab_size, embedding_dim, rnn_units, batch_size):
	 model = tf.keras.Sequential([
		 tf.keras.layers.Embedding(vocab_size, embedding_dim,
									batch_input_shape=[batch_size, None]),
	 tf.keras.layers.LSTM(rnn_units,
						  return_sequences=True,
						  stateful=True,
						  recurrent_initializer='glorot_uniform'),
	 tf.keras.layers.Dense(vocab_size)
   ])
 return model

model = build_model(VOCAB_SIZE,EMBEDDING_DIM, RNN_UNITS, BATCH_SIZE)
model.summary()
```

## Creating a Loss Function
- we are going to create our own loss function for this problem
	-   because our model will output a (64, sequence_length, 65) shaped tensor that represents the probability distribution of each character at each timestep for every sequence in the batch

```python
for input_example_batch, target_example_batch in data.take(1):
 example_batch_predictions = model(input_example_batch) # ask our model for a prediction on our first batch of training data (64 entries)
 print(example_batch_predictions.shape, "# (batch_size, sequence_length, vocab_size)") # print out the output shape
 
 
# we can see that the predicition is an array of 64 arrays, one for each entry in the batch
print(len(example_batch_predictions))
print(example_batch_predictions)


# lets examine one prediction
pred = example_batch_predictions[0]
print(len(pred))
print(pred)
# notice this is a 2d array of length 100, where each interior array is the prediction for the next character at each time step


# and finally well look at a prediction at the first timestep
time_pred = pred[0]
print(len(time_pred))
print(time_pred)
# and of course its 65 values representing the probabillity of each character occuring next


# If we want to determine the predicted character we need to sample the output distribution (pick a value based on probabillity)
sampled_indices = tf.random.categorical(pred, num_samples=1)
  
# now we can reshape that array and convert all the integers to numbers to see the actual characters
sampled_indices = np.reshape(sampled_indices, (1, -1))[0]
predicted_chars = int_to_text(sampled_indices)

predicted_chars # and this is what the model predicted for training sequence 1
```
- So now we need to create a loss function that can compare that output to the expected output and give us some numeric value representing how close the two were
```python
def loss(labels, logits):
	 return tf.keras.losses.sparse_categorical_crossentropy(labels, logits, from_logits=True)
```
## Compiling the Model
- At this point we can think of our problem as a classification problem where the model predicts the probabillity of each unique letter coming next
- 
```python
model.compile(optimizer='adam', loss=loss)
```

## Creating Checkpoints
- Now we are going to setup and configure our model to save checkpoinst as it trains. This will allow us to load our model from a checkpoint and continue training it.
- 
```python
# Directory where the checkpoints will be saved
checkpoint_dir = './training_checkpoints'
# Name of the checkpoint files
checkpoint_prefix = os.path.join(checkpoint_dir, "ckpt_{epoch}")  

checkpoint_callback=tf.keras.callbacks.ModelCheckpoint(
					 filepath=checkpoint_prefix,
					 save_weights_only=True)
```
## Training
- Finally, we will start training the model
```python
history = model.fit(data, epochs=50, callbacks=[checkpoint_callback])
```
## Loading the Model
- We'll rebuild the model from a checkpoint using a batch_size of 1 so that we can feed one peice of text to the model and have it make a prediction
```python
model = build_model(VOCAB_SIZE, EMBEDDING_DIM, RNN_UNITS, batch_size=1)
```
-  we can find the **lastest checkpoint** that stores the models weights using the following line
```python
model.load_weights(tf.train.latest_checkpoint(checkpoint_dir))
model.build(tf.TensorShape([1, None]))
```
- We can load **any checkpoint** we want by specifying the exact file to load.
```python
checkpoint_num = 10
model.load_weights(tf.train.load_checkpoint("./training_checkpoints/ckpt_" + str(checkpoint_num)))
model.build(tf.TensorShape([1, None]))
```
## Generating Text
- Now we can use the lovely function provided by tensorflow to generate some text using any starting string we'd like
```python
def generate_text(model, start_string):
	 # Evaluation step (generating text using the learned model)

	 # Number of characters to generate
	 num_generate = 800  

	 # Converting our start string to numbers (vectorizing)
	 input_eval = [char2idx[s] for s in start_string]
	 input_eval = tf.expand_dims(input_eval, 0)  

	 # Empty string to store our results
	 text_generated = []  

	 # Low temperatures results in more predictable text.
	 # Higher temperatures results in more surprising text.
	 # Experiment to find the best setting.
	 temperature = 1.0  

	 # Here batch size == 1
	 model.reset_states()
	 for i in range(num_generate):
	 	predictions = model(input_eval)
	 	# remove the batch dimension
	 	predictions = tf.squeeze(predictions, 0)

	 		# using a categorical distribution to predict the character returned by the model
	 	predictions = predictions / temperature
	 	predicted_id = tf.random.categorical(predictions, num_samples=1)				[-1,0].numpy()

	 	# We pass the predicted character as the next input to the model
	 	# along with the previous hidden state
	 	input_eval = tf.expand_dims([predicted_id], 0)

	 	text_generated.append(idx2char[predicted_id])
  
 return (start_string + ''.join(text_generated))
 
 
inp = input("Type a starting string: ")
print(generate_text(model, inp))
```

[[Reinforcement Learning]]