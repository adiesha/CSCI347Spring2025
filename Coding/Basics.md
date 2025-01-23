Let's do some coding

Let's start with a simple exercise. Let us compute the estimated mean of a given array. 
Suppose you are given `X = [20, 3, 1 , 3, 6, 4]`. First, in the shell, start python and type following.

```
X = [20, 3, 1 , 3, 6, 4]

sum = 0
for x_i in X:
  sum += x_i
x_hat = sum/len(X)
```


Okay, now let's try to abstract it by creating a function.
```
def mean(X):
  sum = 0
  for x_i in X:
    sum += x_i
  x_hat = sum/len(X)
  return x_hat

X = [20, 3, 1 , 3, 6, 4]
mean(X)
```
Okay, now observe that for the semester, we are going to work with Vecctors and matrices. After while it will become harder to work with loops to manipulate them.
So we are going to use tools to make our life easier. First we will use numpy. 

Let's install numpy
```
pip install numpy
```
Okay let's get back to the coding

```
import numpy as np
X = np.array([20, 3, 1 , 3, 6, 4])
x_hat = X.sum()/ X.size
```
Or we can just use the mean function directly.

```
X.mean()
```

Nice thing about is that np has some functions for decriptive stats.

```
    X.max()
    X.min()
    X.std()
```
OKAY! We learnt a lot about matrices in the last few lectures. Let's try to see whether we can use numpy to handle matrices.
Let's create a matrix of 6 rows and 4 columns of some random data to play with.

```
D = np.random.random((5,3))
```
Breaking down the code....

```np.random```

This is the random number generation module in NumPy, which provides various functions for generating random numbers.
Now, let's see the shape of the data that we created.

```random```

The random function generates random values uniformly distributed in the range 
```[0.0,1.0)```

```(5,3)```

This This tuple specifies the shape of the array. ```5``` is the number of rows, ```3``` is the number of columns.

Manually creating a matrix with values using numpy
```
N = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])
```

```print(D)```

Let us look at the shape of the data.

```
D.shape
```

Let us try to access a value:

```D[0,1]```

Note that ```D``` is ```0``` indexed.

```D[4,2]```

```D[5,1]``` 

IndexError: index 5 is out of bounds for axis 0 with size 5.... Obviously!!!

Variable ```D``` stores the resulting 2D array.

Okay, now let's move onto slicing!! This is very powerful technique. We can do lot of fun stuff.
[slicing and dicing (_**See User Docs**_)](https://numpy.org/doc/stable/user/quickstart.html#indexing-slicing-and-iterating)
but today we will just do some basics.

First let us try to do this by looping.. Try this by yourself!!! 


column_0 = []
for row in D:
    column_0.append(row[0])

or 
column_0 = [row[0] for row in D]

Let's use numpy to access the first column.

```X0 = D[:, 0]```

and the 2nd column

```X2 = D[:, 2]```

Key points in this 
- ```D``` This is the NumPy array, which is a 2-dimensional structure (like a matrix) where elements can be accessed using row and column indices.
- ```:``` is the slicing operator, it means select all rows in this example
- ```0``` Refers to the ith column.

What if we want to select multiple columns?

```X02 = D[:, [0,2]]```

We can do the other way around as well. We can select all columns and one row (or subset). Let's play with this.....

Now let's move to dot product.

```np.dot(X0, X2)```

We can even get values for the different norms that we talked about.  The
[np.linalg package](https://numpy.org/doc/stable/reference/routines.linalg.html)
has tons of functionality, but we will just use the norm for now.

```
    d1 = np.linalg.norm(X2-X0, 1)
    d2 = np.linalg.norm(X2-X0, 2)
```

And, we can also scale by a number!  So to double our vector X0, we can multiply
by 2!

```4*X1```

So, let's normalize our vector.  That is, make our vector length 1 (in the
2-norm).

```
two_norm_of_X0 = np.linalg.norm(X0, 2)
normalized_X0 = X0 / two_norm_of_X0
```

The above code is an example of what numpy (and now other libraries in the
python world call) ([broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)).
The idea behind broadcasting is that the system "stretches" objects to higher
dimensional objects so that operations can occur in a meaningful way.

The numpy docs have a nice [visualisation of broadcasting a number to a vector](
https://numpy.org/doc/stable/_images/broadcasting_1.png) and then using the
vector for an element-wise operation.

We could subtract a vector from a matrix

```D - np.array([1,2,3])```

Add a vector to a matrix

```D + np.array([1,2,3])```

Let's look at the mean function again. Try the following and see what they mean.


```
D.mean()
D.mean(axis=0)
D.mean(axis=1)
```

We can use broadcasting for all sorts of applications.  Use the `mean` function
and broadcasting to to mean center your data:

```D-D.mean(axis=0)```






Manually creating a matrix with values using numpy
```
N = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])
```

You can take the transpose your matrix as follows:

```D.transpose()```

... while I don't have a great reason why you would do this, it illustrates a
useful function, write some code to mean center along the rows.  Check out docs
for [mean](https://numpy.org/doc/stable/reference/generated/numpy.mean.html) and
[transpose](https://numpy.org/doc/stable/reference/generated/numpy.transpose.html)
for some help.


```(D.transpose()-D.mean(axis=1)).transpose()```

Okay, now let us move to some statistics. Let us compute the variance of the X0

```
    np.sum((X0-X0.mean())**2) / (X0.size-1)
```

okay, what if we use ```np.var(X0)```

What's going on here? Did we make a mistake? Let's check the docs.

[np.var](https://numpy.org/doc/stable/reference/generated/numpy.var.html)

There is an optional arguement called ddof. By default **ddof** is **zero**. Basically, this mean it calculates the variance using the population variance formula. But the formula that we learnt in the class is an unbiased estimator of the variance.
So, let's use that.

```np.var(X0, ddof =1)```

Let's do a exercise.
1.  Create a matrix M of 10 rows and 8 columns, fill with it with random values.
2.  Calculate the multi dimensional mean (represent the multi dimensional mean as a vector)
3.  Calculate the min, max, variance and SD of each attribute.
4.  Create matrix R with range normalized data.
5.  Create matrix Z with z-scores.


Okay, I think this is enough for today!!!! We will move to Jupyter Lab in the next class.
