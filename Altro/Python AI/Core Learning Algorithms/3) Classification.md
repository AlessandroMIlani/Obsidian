- *Classification* is used to separate data points into 

## Import & Setup
```python
from __future__ import absolute_import, division, print_function, unicode_literals  
import tensorflow as tf  
import pandas as pd
```

## Exemp Dataset
3 different classes of species (on this data set)
 1.   Setosa
1.  Versicolor
1.  Virginica
    - all whit 4 info
    	1. sepal length
    	2.  sepal width
    	3.   petal length
    	4.   petal width

```python
CSV_COLUMN_NAMES = ['SepalLength', 'SepalWidth', 'PetalLength', 'PetalWidth', 'Species']
SPECIES = ['Setosa', 'Versicolor', 'Virginica']
# Lets define some constants to help us later on

train_path = tf.keras.utils.get_file(
 "iris_training.csv", "https://storage.googleapis.com/download.tensorflow.org/data/iris_training.csv")
test_path = tf.keras.utils.get_file(
 "iris_test.csv", "https://storage.googleapis.com/download.tensorflow.org/data/iris_test.csv")
train = pd.read_csv(train_path, names=CSV_COLUMN_NAMES, header=0)
test = pd.read_csv(test_path, names=CSV_COLUMN_NAMES, header=0)
# Here we use keras (a module inside of TensorFlow) to grab our datasets and read them into a pandas dataframe
```

look data with .head() nad remove "Species" colums with .pop

## Input Function
```python
def input_fn(features, labels, training=True, batch_size=256):  
    # Convert the inputs to a Dataset.  
 dataset = tf.data.Dataset.from_tensor_slices((dict(features), labels))    
    # Shuffle and repeat if you are in training mode.  
 if training:  
        dataset = dataset.shuffle(1000).repeat()    
    return dataset.batch(batch_size)
```

## Feature Columns
```python
my_feature_columns = []  
for key in train.keys():  
    my_feature_columns.append(tf.feature_column.numeric_column(key=key))  
print(my_feature_columns)
```

## Building the model
We need to create a model.
We have 2 option
   - DNNClassifier( Deep Neural Network) --> best choise
   - LinearClassifier
```python
# Build a DNN with 2 hidden layers with 30 and 10 hidden nodes each.
classifier = tf.estimator.DNNClassifier(
 feature_columns=my_feature_columns,
 # Two hidden layers of 30 and 10 nodes respectively.
 hidden_units=[30, 10],
 # The model must choose between 3 classes.
 n_classes=3)
```

 ## Training 
[  we need to create  a "lambda" --> a 1 line function]
```python
x = lambda: print("hi")
x()  # this print Hi
```
---
```python
classifier.train(input_fn=lambda: input_fn(train, train_y, training=True), steps=5000)
# We include a lambda to avoid creating an inner function previously
```
- Spteps are similar to epchs, but them not cyclic all datas X time, but read X datas (so if they ar less, they ar reed more time on shuffle order)

## Evaluation
```python
eval_result = classifier.evaluate(input_fn=lambda: input_fn(test, test_y, training=False))
print('\nTest set accuracy: {accuracy:0.3f}\n'.format(**eval_result))
```

## Prediction
```python
def input_fn(features, batch_size=256):
 # Convert the inputs to a Dataset without labels.
 return tf.data.Dataset.from_tensor_slices(dict(features)).batch(batch_size)

features = ['SepalLength', 'SepalWidth', 'PetalLength', 'PetalWidth']
predict = {}

print("Please type numeric values as prompted.")
for feature in features:
 valid = True
 while valid: 
 	val = input(feature + ": ")
 	if not val.isdigit(): valid = False

 predict[feature] = [float(val)]
  
predictions = classifier.predict(input_fn=lambda: input_fn(predict))
for pred_dict in predictions:
 class_id = pred_dict['class_ids'][0]
 probability = pred_dict['probabilities'][class_id]

 print('Prediction is "{}" ({:.1f}%)'.format(SPECIES[class_id], 100 * probability))
```

[[4) Clustering |  Clustering]]