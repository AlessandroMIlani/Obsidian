## Imports
```python
# TensorFlow and tf.keras
import tensorflow as tf
from tensorflow import keras

# Helper libraries
import numpy as np
import matplotlib.pyplot as plt
```

## Dataset
- 60000 images for training and 10000 image of testing
 ```python
 fashion_mnist = keras.datasets.fashion_mnist # load dataset
(train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data() # split into tetsing and training
 ```
 - look the data whit the usual ".shape" function (60000,28,28)

- we can look at 1 picel whit "train_images[0, 23, 23]" (image, x, y position of pixel) -> 194 (numb. betwwn 0 black and 255 white)
	- we have grayscale

- train_labels[:10] -> array([9, 0, 0, 3, 2, 7, 2, 5, 5], dtype=unit8) ->10 diffenret class
  - ```python 
class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat',
 'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']```
 
 look same image
 ```pyhton
 plt.figure()
plt.imshow(train_images[1])
plt.colorbar()
plt.grid(False)
plt.show()
 ```

## Data preprocessing
we scale all our value 0-255 to the range 0 and 1
- doing this make easir for our model to process our valuse
 ```python
 train_images = train_images / 255.0
 test_images = test_images / 255.0
  ```

## Building the Model
```python
model = keras.Sequential([
keras.layers.Flatten(input_shape=(28, 28)), # input layer (1)
keras.layers.Dense(128, activation='relu'), # hidden layer (2)
keras.layers.Dense(10, activation='softmax')  # output layer (3)
])
```
- layers described in [[Neural Network intro | introduction]]

## Compile the model
The last step in building the model is to define the loss function, optimizer and metrics we would like to track
```python
model.compile(optimizer='adam',
 			  loss='sparse_categorical_crossentropy',
 			  metrics=['accuracy'])
```

## Training the Model
```python
model.fit(train_images, train_labels, epochs=10) # we pass the data, labels and epochs and watch the magic!
```

## Evaluating the model
```python
test_loss, test_acc = model.evaluate(test_images, test_labels, verbose=1) 
print('Test accuracy:', test_acc)
```
## Make prediction
```python
predictions = model.predict(test_images)
print(predictions[0])
print(np.argmax(predictions[0]))
print(test_labels[0])
```

## Verifyng Prediction
```python
COLOR = 'white'
plt.rcParams['text.color'] = COLOR
plt.rcParams['axes.labelcolor'] = COLOR
  
def predict(model, image, correct_label):
 class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat',
 			   'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']
 prediction = model.predict(np.array([image]))
 predicted_class = class_names[np.argmax(prediction)]  
 
 show_image(image, class_names[correct_label], predicted_class)

def show_image(img, label, guess):
 plt.figure()
 plt.imshow(img, cmap=plt.cm.binary)
 plt.title("Excpected: " + label)
 plt.xlabel("Guess: " + guess)
 plt.colorbar()
 plt.grid(False)
 plt.show()

def get_number():
 while True:
 	num = input("Pick a number: ")
 	if num.isdigit():
 		num = int(num)
 		if 0 <= num <= 1000:
 			return int(num)
 		else:
 			print("Try again...")
 
num = get_number()
image = test_images[num]
label = test_labels[num]
predict(model, image, label)
```

[[**Convolutional Neural Networks**]]