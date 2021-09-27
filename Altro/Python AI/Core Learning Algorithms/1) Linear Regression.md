- one of the most basic Learning Algorithms
- Correlates data point in a liner way
- possible use it on more than 2 dimension

![[Linear Reg. Graph.png]]

## Setup and import 
```python
from __future__ import absolute_import, division, print_function, unicode_literals 
import numpy as np  # math help  
import pandas as pd  # manipulate dateset  
import matplotlib.pyplot as plt  # visualization graph  
from IPython.display import clear_output  
from six.moves import urllib  
import pylab   
import tensorflow.compat.v2.feature_column as fc  
import tensorflow as tf  
  
# load dataset  
dftrain = pd.read_csv('https://storage.googleapis.com/tf-datasets/titanic/train.csv')  # training data  
dfeval = pd.read_csv('https://storage.googleapis.com/tf-datasets/titanic/eval.csv')  # testing data
y_train = dftrain.pop('survived')  # Return item and drops from series. Raise KeyError if not found
y_eval = dfeval.pop('survived')
```

## Data Manipulation
```python
print(dftrain.head())  # show the first 5 items in our dataframe

print(dftrain.loc[0], y_train.loc[0]) # .loc[] -> Access a group of rows and columns by label(s) or a boolean array

print(dftrain.describe())  # like .head() more precice

print(dftrain.shape) # shape of the dataset
```

## generate same graphs
```python
dftrain.age.hist(bins=20)  
plt.show()  

dftrain['class'].value_counts().plot(kind='barh')  
plt.show()
```

[[2) Trainig VS Testing Data | Trainig VS Testing Data]]