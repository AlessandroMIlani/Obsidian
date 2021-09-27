- ***TRAINING DATASET***: WHAT WE FEED THE MODEL
  - it cal learn from it
  - general bigger tha testing dataset
  
 
 - In our dataset  we have Categorical and numeric colums:
     - Categorical: non numeric data, like: sex, class, city ecc...
     - Numerical: numerical data, like: age, fare      
     
```python
	CATEGORICAL_COLUMS = ['sex', 'n_siblings_spouses', 'parch', 'class', 'deck', 'embark_town', 'alone']  
    NUMERIC_COLUMS = ['age', 'fare']
```

- Before we continue and create/train a model we must convet our categorical data into numeric data. 
We can do this by encoding each category with an integer (ex. male = 1, female = 2)

```python
feature_colums = []  
for feature_name in CATEGORICAL_COLUMS:  
    vocabulary = dftrain[feature_name].unique()  # gets alist of all unique values   from given feature column      feature_colums.append(tf.feature_column.categorical_column_with_vocabulary_list(feature_name, vocabulary))    
for feature_name in NUMERIC_COLUMS:  
    feature_colums.append(tf.feature_column.numeric_column(feature_name, dtype=tf.float32))
```

## Training Process
- it's how we fed our model with the data from the dataset
  - if we have a lot of data (es. 25Tb) we can't save all in our Ram, so we need to split the on more **batches** [we use batches of 32]
  - 1 **epoch** is 1 stram of our entire dataset
    - it's usefull fed the model with the same dataset more time whit a shuffle order, to finde more correlation
    	- !! WARNING to avoid overfeeding
    	
		
## Input Function
- Is the way how our data is going to be broke into epochs and into batches for feed our model
	- function input:
	  1.   dataframe from panda
	  2.   labeled dataframe (train, y_eval ...)
	  3.   numb. of epochs
	  4.   enable or disable shuffle
	  5.   batch dimension
	  
```python
def make_input_fn(data_df, label_df, num_epochs=10, shuffle=True, batch_size=32):  
    def input_function():  # inner function, this will be returned  
    	ds = tf.data.Dataset.from_tensor_slices((dict(data_df), label_df))  # create tf.data.Dataset object with data and its label 
		if shuffle:  
            ds = ds.shuffle(1000)  # randomize order of data  
    	ds = ds.batch(batch_size).repeat(num_epochs)  # split dataset into batches of 32 and repeat process for number of epochs return ds return a batch of the dataset 
    	return ds  # return a batch of the dataset
 	return input_function  # return a function object for use  
train_input_fn = make_input_fn(dftrain, y_train)  # here we will call the input_function that was returned to us to get  a dataset object we can feed to the model  
eval_input_fn = make_input_fn(dfeval, y_eval, num_epochs=1, shuffle=False)
```

## Creating the Model
Creating a linear model is pretty easy
```python
linear_est = tf.estimator.LinearClassifier(feature_columns=feature_columns)
# We create a linear estimtor by passing the feature columns we created earlier
```

## Training the Model
```python
linear_est.train(train_input_fn) # train
result = linear_est.evaluate(eval_input_fn) # get model metrics/stats by testing on tetsing data
clear_output() # clears consoke output
print(result['accuracy']) # the result variable is simply a dict of stats about our model
```

- We can use the ``` .predict()``` method to get survival probabilities from the model
  - This method will return a list of dicts that store a predicition for each of the entries in our testing data set
  
```python
pred_dicts = list(linear_est.predict(eval_input_fn))
probs = pd.Series([pred['probabilities'][1] for pred in pred_dicts])
probs.plot(kind='hist', bins=20, title='predicted probabilities')
```

[[3) Classification | Classification]]