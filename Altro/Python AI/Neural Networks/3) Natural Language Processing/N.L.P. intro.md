# Natural Language Processing
- is a discipline that deals whit the communication between natural lenguage and computer languages
	 

## Recurrent Neural Network
- learn how to use
	- Sebtunebt Analysis
	- Character Generation
- RNN's are complex and have different forms so is difficult focus on how them work

## Sequence Data
- now look at sequences of text and learn how we can encode them in a meaningful way
- sequence data (chains of text, vido ecc...) need to be processed and handled in a special way
	- But what do I mean by sequences and why is text data a sequence? 
		- Textual data contains many words that follow in a very specific and meaningful order
		 we need to be able to keep track of each word and when it occurs in the data
		  - encode 1 paragraph on 1 datapoint wouldn't give a very usefull information
		  - So we keep track of where each of these words appear and use that information to try to understand the meaning of peices of text

## Encoding Text
- Before we get into the different encoding/preprocessing methods let's understand the information we can get from textual data by looking at the following two movie reviews.

	- I thought the movie was going to be bad, but it was actually amazing!
	- I thought the movie was going to be amazing, but it was actually bad!
	
These two setences are very similar but have very different meanings. This is because of the **ordering** of words, a very important property of textual data

### Bag of Words
- simplest way to encode our data
- eatch word is correlate with and integer on a vocabulary
- we  save how much time that word is used
- we **not** save the order
```python
vocab = {} # maps word to integer representing it
word_encoding = 1
def bag_of_words(text):
 	global word_encoding
  
 	words = text.lower().split(" ") # create a list of all of the words in the text, well assume there is no grammar in our text for this example
 	bag = {} # stores all of the encodings and their frequency

  

 	for word in words:
 		if word in vocab:
 			encoding = vocab[word] # get encoding from vocab
 		else:
 			vocab[word] = word_encoding
			 encoding = word_encoding
 				word_encoding += 1
 		if encoding in bag:
 			bag[encoding] += 1
 		else:
 			bag[encoding] = 1
 	return bag

  

text = "this is a test to see if this test will work is is test a a"
bag = bag_of_words(text)
print(bag)
print(vocab)
```
- This isn't really the way we would do this in practice
	- let's look at how this encoding works for the two sentences we showed above

```python
positive_review = "I thought the movie was going to be bad but it was actually amazing"
negative_review = "I thought the movie was going to be amazing but it was actually bad"  

pos_bag = bag_of_words(positive_review)
neg_bag = bag_of_words(negative_review)

print("Positive:", pos_bag)
print("Negative:", neg_bag)
```

- We can see that even though these sentences have a very different meaning they are encoded exaclty the same way

### Integer Encoding
- This involves representing each word or character in a sentence as a unique integer and maintaining the order of these words

```python
vocab = {} 
word_encoding = 1
def one_hot_encoding(text):
 	global word_encoding 

 	words = text.lower().split(" ") 
 	encoding = [] 
  
 	for word in words:
 		if word in vocab:
 			code = vocab[word] 
 			encoding.append(code)
 		else:
 			vocab[word] = word_encoding
 			encoding.append(word_encoding)
			 word_encoding += 1
 	return encoding
  
text = "this is a test to see if this test will work is is test a a"
encoding = one_hot_encoding(text)
print(encoding)
print(vocab)
```
- And now let's have a look at one hot encoding on our movie reviews.
```python
positive_review = "I thought the movie was going to be bad but it was actually amazing"
negative_review = "I thought the movie was going to be amazing but it was actually bad"  

pos_encode = one_hot_encoding(positive_review)
neg_encode = one_hot_encoding(negative_review)  

print("Positive:", pos_encode)
print("Negative:", neg_encode)
```
- now we are keeping track of the order of words and we can tell where each occurs, but whit some issues
	-  Ideally when we encode words, we would like similar words to have similar labels and different words to have very different labels
	-  ex. if 1= good, 2=bad, 10000=nice, it's difficult for a program undertand that 1 is nearest to 10000 and far away to 2 (and if we add 9999 = horrible, it's come   
even more difficult)

### Word Embeddings
- Luckily there is a third method that is far superior
	-  This method keeps the order of words intact and encodes similar words with very similar labels
	-  It encodes each word as a dense vector that represents its context in the sentence
- Unlike the previous techniques word embeddings are learned by looking at many different training examples


[[Recurrent Neural Networks]]