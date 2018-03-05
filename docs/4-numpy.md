# Using Numpy and Matplotlib

## A couple of examples:
- Recall the movielens dataset introduced last time.
   - It is a [movie, item, rating] triplet with roughly 1,000,000 ratings with a training and test split.
   - The first task is to convert the data set into a matrix $A$ so that each entry of the matrix $A(movie, item) = rating$
   - The file has a _trainvec_ and a _probevec_. _trainvec_
     corresponds to the training data and we'll try to keep the fact
     in mind that some users may exist in the testing data that may
     not be there in the training data.
  - We can open the file and load it like:
	```python
		import numpy as np
		from scipy.io import loadmat
		mat = loadmat('moviedata.mat')
		# using copy() just to be safe in case file is closed later
		traindata = mat['trainvec'].copy()
		probedata = mat['probevec'].copy()
		```
  - A simple line of numpy code that'll convert the triplets into matrix could be:
	```python
		 for i in traindata:
			 train_matrix[i[0], i[1]] = i[2]
    ```
	- But we don't want to use a loop now do we?
	- Also what's the shape of `train_matrix`?  We have not defined it.
	- The first problem therefore is to know what sort of shape the matrix will have.
	- 

<!-- ## A brief overview of various useful functions in numpy -->
<!-- ```python -->
<!-- import numpy as np # It'll be assumed to be imported like this everywhere -->
<!-- ``` -->

<!-- #### np.concatenate :  Join a sequence of arrays along an existing axis. -->
<!-- #### np.split : Split array into a list of multiple sub-arrays of equal size. -->
<!-- #### np.hsplit : Split array into multiple sub-arrays horizontally (column wise) -->
<!-- #### np.vsplit : Split array into multiple sub-arrays vertically (row wise) -->
<!-- #### np.dsplit : Split array into multiple sub-arrays along the 3rd axis (depth). -->
<!-- #### np.stack : Stack a sequence of arrays along a new axis. -->
<!-- #### np.hstack : Stack arrays in sequence horizontally (column wise) -->
<!-- #### np.vstack : Stack arrays in sequence vertically (row wise) -->
<!-- #### np.dstack : Stack arrays in sequence depth wise (along third dimension) -->
<!-- #### np.tile :  -->

