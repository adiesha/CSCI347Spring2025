Let's do some coding

Let's start with a simple exercise. Let us compute the estimated mean of a given array. Suppose you are given ```X = [20, 3, 1 , 3, 6, 4]```. First, in the shell, start python and type following.


```python
X = [20, 3, 1 , 3, 6, 4]

sum = 0
for x_i in X:
  sum += x_i
x_hat = sum/len(X)
x_hat
```




    6.166666666666667



Okay, now let's try to abstract it by creating a function.



```python
def mean(X):
  sum = 0
  for x_i in X:
    sum += x_i
  x_hat = sum/len(X)
  return x_hat

X = [20, 3, 1 , 3, 6, 4]
mean(X)
```




    6.166666666666667



Okay, now observe that for the semester, we are going to work with Vecctors and matrices. After while it will become harder to work with loops to manipulate them. 
So we are going to use tools to make our life easier. First we will use numpy.


Okay, now observe that for the semester, we are going to work with Vecctors and matrices. After while it will become harder to work with loops to manipulate them. 
So we are going to use tools to make our life easier. First we will use numpy.


Let's install numpy

```pip install numpy```

Type this in your command line, and install numpy.


```python
import numpy as np
X = np.array([20, 3, 1 , 3, 6, 4])
x_hat = X.sum()/ X.size
x_hat
```




    np.float64(6.166666666666667)



Or we can just use the mean function directly.




```python
X.mean()

```




    np.float64(6.166666666666667)



Nice thing about is that np has some functions for decriptive stats.




```python
X.max()

```




    np.int64(20)




```python
X.min()
    
```




    np.int64(1)




```python
X.std()
```




    np.float64(6.361778227997438)



OKAY! We learnt a lot about matrices in the last few lectures. Let's try to see whether we can use numpy to handle matrices. Let's create a matrix of 6 rows and 4 columns of some random data to play with.


```python
D = np.random.random((6,4))

D
```




    array([[0.04522235, 0.7635029 , 0.35560888, 0.35717965],
           [0.87005355, 0.09344188, 0.89981975, 0.99326811],
           [0.87334077, 0.99010486, 0.49018506, 0.04928653],
           [0.69848742, 0.93535763, 0.11820078, 0.86094916],
           [0.71672482, 0.88406492, 0.85620985, 0.88327975],
           [0.48101292, 0.940891  , 0.77681985, 0.13802364]])



Breaking down the code....

```np.random```

This is the random number generation module in NumPy, which provides various functions for generating random numbers. Now, let's see the shape of the data that we created.

```random```

The random function generates random values uniformly distributed in the range [0.0,1.0)

```(5,3)```

This This tuple specifies the shape of the array. 5 is the number of rows, 3 is the number of columns.

Also, let us create a numpy matrix with hard coded values, sometimes for testing and debugging purposes, this will help you!


```python
N = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])
N
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



Let us look at the shape of the data.


```python
N.shape
```




    (3, 3)



Let us try to access a value:

```D[0,1]```

Note that ```D``` is 0 indexed.




```python
D[0,1]
print(D[0,1])
```

    0.7635028971074811
    


```python
D[4,2]
```




    np.float64(0.8562098463826096)




```python
D[5,1]
```




    np.float64(0.9408909980940758)



IndexError: index 5 is out of bounds for axis 0 with size 5.... Obviously!!!

Variable ```D``` stores the resulting 2D array.

Okay, now let's move onto slicing!! This is very powerful technique. We can do lot of fun stuff.
[slicing and dicing (_**See User Docs**_)](https://numpy.org/doc/stable/user/quickstart.html#indexing-slicing-and-iterating)
but today we will just do some basics.

First let us try to do this by looping.. Try this by yourself!!! 



```python
column_0_loop = []
for row in D:
    column_0_loop.append(row[0])

column_0_loop
```




    [np.float64(0.04522234605622011),
     np.float64(0.8700535530321374),
     np.float64(0.8733407712302205),
     np.float64(0.6984874173614224),
     np.float64(0.7167248165090979),
     np.float64(0.481012918595245)]




```python
column_0 = [row[0] for row in D]
```

Both of these ways seems to be either too cumbersome or hard to read.

Let's use numpy to access the first column.


```python
X0 = D[:, 0]
X0


```




    array([0.04522235, 0.87005355, 0.87334077, 0.69848742, 0.71672482,
           0.48101292])




```python
X1 = D[:, 1]
X1
```




    array([0.7635029 , 0.09344188, 0.99010486, 0.93535763, 0.88406492,
           0.940891  ])




```python
X2 = D[:, 2]
X2
```




    array([0.35560888, 0.89981975, 0.49018506, 0.11820078, 0.85620985,
           0.77681985])



Key points in this 
- ```D``` This is the NumPy array, which is a 2-dimensional structure (like a matrix) where elements can be accessed using row and column indices.
- ```:``` is the slicing operator, it means select all rows in this example
- ```0``` Refers to the ith column.

What if we want to select multiple columns?


```python
X02 = D[:, [2,0]]
X02
```




    array([[0.04522235, 0.35560888],
           [0.87005355, 0.89981975],
           [0.87334077, 0.49018506],
           [0.69848742, 0.11820078],
           [0.71672482, 0.85620985],
           [0.48101292, 0.77681985]])




```python
D
```




    array([[0.04522235, 0.7635029 , 0.35560888, 0.35717965],
           [0.87005355, 0.09344188, 0.89981975, 0.99326811],
           [0.87334077, 0.99010486, 0.49018506, 0.04928653],
           [0.69848742, 0.93535763, 0.11820078, 0.86094916],
           [0.71672482, 0.88406492, 0.85620985, 0.88327975],
           [0.48101292, 0.940891  , 0.77681985, 0.13802364]])



Note that ```X02 = D[:, [2,0]]``` is interpreted by numpy as follows:


- ```:``` means slice all rows (basic slicing).
- ```[2, 0]``` is a list of column indices (advanced indexing).
- NumPy interprets this as: "For all rows, select columns 2 and 1."

How about taking a subset of rows with all the columns?


```python
D[[0,1,2], :]
```




    array([[0.04522235, 0.7635029 , 0.35560888, 0.35717965],
           [0.87005355, 0.09344188, 0.89981975, 0.99326811],
           [0.87334077, 0.99010486, 0.49018506, 0.04928653]])




```python

```

What about subset of columns with all rows?
You **cannot** use something like:

```D[[0,1,2], [1,2]]```


```python
D[[0,1,2], [1,2]]
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    Cell In[81], line 1
    ----> 1 D[[0,1,2], [1,2]]
    

    IndexError: shape mismatch: indexing arrays could not be broadcast together with shapes (3,) (2,) 


```D[[0,1,2], [1,2]]```

This is interpreted as pairing the elements of the two lists element by element.

```(0, 1) → ``` Element at row 0, column 1

```(1, 2) → ``` Element at row 2, column 2

```(2, ?) → ``` Error (shape mismatch if sizes differ)

But you can do something like following:



```python
D[[0,1],[3,2]]
```




    array([0.35717965, 0.89981975])



Basically outputting ```(0,3), (1,2)``` indices.

This is bit weird.


```python
D
```




    array([[0.04522235, 0.7635029 , 0.35560888, 0.35717965],
           [0.87005355, 0.09344188, 0.89981975, 0.99326811],
           [0.87334077, 0.99010486, 0.49018506, 0.04928653],
           [0.69848742, 0.93535763, 0.11820078, 0.86094916],
           [0.71672482, 0.88406492, 0.85620985, 0.88327975],
           [0.48101292, 0.940891  , 0.77681985, 0.13802364]])




```python
D[:, [1,2]]
```




    array([[0.7635029 , 0.35560888],
           [0.09344188, 0.89981975],
           [0.99010486, 0.49018506],
           [0.93535763, 0.11820078],
           [0.88406492, 0.85620985],
           [0.940891  , 0.77681985]])



But when it comes to subset of rows and columns, it becomes bit tricky, you cannot use the same trick that we use earlier.

Let's look at how we do this...

First define the list of rows and columns that needs to be in the result and then use ```np.ix_```


```python
rows = [0, 2, 3]  # Rows to select
cols = [1, 3]  # Columns to select

print(D[np.ix_(rows, cols)])
print("--------------------")
print(D)
```

    [[0.7635029  0.35717965]
     [0.99010486 0.04928653]
     [0.93535763 0.86094916]]
    --------------------
    [[0.04522235 0.7635029  0.35560888 0.35717965]
     [0.87005355 0.09344188 0.89981975 0.99326811]
     [0.87334077 0.99010486 0.49018506 0.04928653]
     [0.69848742 0.93535763 0.11820078 0.86094916]
     [0.71672482 0.88406492 0.85620985 0.88327975]
     [0.48101292 0.940891   0.77681985 0.13802364]]
    

Now, let us look at the dot product.


```python
np.dot(X0, X2)
```




    np.float64(2.2969604254654654)



We can even get values for the different norms that we talked about.  

The [np.linalg package](https://numpy.org/doc/stable/reference/routines.linalg.html)
has tons of functionality, but we will just use the norm for now.



```python
d1 = np.linalg.norm(X2-X0, 1)
d2 = np.linalg.norm(X2-X0, 2)
print(d1, d2)
```

    1.738887047421991 0.8292915800233719
    

And, we can also scale by a number!  So to double our vector X0, we can multiply
by 2!


```python
4*X1
```




    array([3.05401159, 0.37376754, 3.96041942, 3.74143053, 3.53625966,
           3.76356399])



So, let's normalize our vector.  That is, make our vector length 1 (in the
2-norm).


```python
two_norm_of_X0 = np.linalg.norm(X0, 2)
normalized_X0 = X0 / two_norm_of_X0
print(normalized_X0)
```

    [0.02724675 0.52421284 0.52619341 0.42084314 0.43183129 0.28981337]
    

The above code is an example of what numpy (and now other libraries in the
python world call) ([broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)).
The idea behind broadcasting is that the system "stretches" objects to higher
dimensional objects so that operations can occur in a meaningful way.

Easy way to create matrix with rand ints...


```python
# np.random.randint(low, high, size, dtype)
I = np.random.randint(-2, 20, (5,7), dtype=np.int32)
print(I)
```

    [[ 2  9 -2 -2 16 14  1]
     [13  1 16 10 -1 13  4]
     [12  5 19  9 15 19 -2]
     [11 11  8  5 19  8  6]
     [ 0 19  4 17  7  5 16]]
    

e could subtract a vector from a matrix

```D - np.array([1,2,3])```

Add a vector to a matrix

```D + np.array([1,2,3])```

Let's look at the mean function again. Try the following and see what they mean.



```python
a = np.array([1,2,3])
I - a
I + a
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[114], line 2
          1 a = np.array([1,2,3])
    ----> 2 D - a
          3 D + np.array([1,2,3])
    

    ValueError: operands could not be broadcast together with shapes (6,4) (3,) 



```python
D.shape
```




    (6, 4)



However, if try to do something like:


```python
b = np.array([[1,2,3,4,5,6,7]])
I - b
```




    array([[ 1,  7, -5, -6, 11,  8, -6],
           [12, -1, 13,  6, -6,  7, -3],
           [11,  3, 16,  5, 10, 13, -9],
           [10,  9,  5,  1, 14,  2, -1],
           [-1, 17,  1, 13,  2, -1,  9]])



Basically, it will broadcast to fit the number of rows, but not columns.

Let's look at the mean function again. Try the following and see what they mean.



```python
I.mean()
```




    np.float64(0.6279598336942959)




```python
I.mean(axis=0)
```




    array([0.6141403 , 0.76789386, 0.58280736, 0.5469978 ])




```python
I.mean(axis=1)
```




    array([0.38037844, 0.71414582, 0.6007293 , 0.65324875, 0.83506983,
           0.58418685])




```python
I
```




    array([[ 2,  9, -2, -2, 16, 14,  1],
           [13,  1, 16, 10, -1, 13,  4],
           [12,  5, 19,  9, 15, 19, -2],
           [11, 11,  8,  5, 19,  8,  6],
           [ 0, 19,  4, 17,  7,  5, 16]], dtype=int32)



We can use broadcasting for all sorts of applications.  Use the `mean` function
and broadcasting to to mean center your data:



```python
D-D.mean(axis=0)
```




    array([[-0.56891796, -0.00439097, -0.22719848, -0.18981816],
           [ 0.25591325, -0.67445198,  0.31701239,  0.4462703 ],
           [ 0.25920047,  0.22221099, -0.0926223 , -0.49771128],
           [ 0.08434711,  0.16746377, -0.46460658,  0.31395136],
           [ 0.10258451,  0.11617105,  0.27340248,  0.33628194],
           [-0.13312739,  0.17299713,  0.19401249, -0.40897417]])



You can take the transpose your matrix as follows:


```python
P = np.random.randint(0, 20, (4,3), dtype=np.int32)
print(P)
print(P.transpose())
```

    [[ 6  3 17]
     [ 5 12  3]
     [ 6  4  6]
     [17 13 11]]
    [[ 6  5  6 17]
     [ 3 12  4 13]
     [17  3  6 11]]
    

while I don't have a great reason why you would do this, it illustrates a
useful function, write some code to mean center along the rows.  Check out docs
for [mean](https://numpy.org/doc/stable/reference/generated/numpy.mean.html) and
[transpose](https://numpy.org/doc/stable/reference/generated/numpy.transpose.html)
for some help.


```python
(P.transpose()-P.mean(axis=1)).transpose()
```




    array([[-2.66666667, -5.66666667,  8.33333333],
           [-1.66666667,  5.33333333, -3.66666667],
           [ 0.66666667, -1.33333333,  0.66666667],
           [ 3.33333333, -0.66666667, -2.66666667]])



Okay, now let us move to some statistics. Let us compute the variance of the X0


```python
var_x0 = np.sum((X0-X0.mean())**2) / (X0.size-1)
print(var_x0)
```

    0.09834100691946199
    

okay, what if we use ```np.var(X0)```


```python
np.var(X0)
```




    np.float64(0.08195083909955166)



What's going on here? Did we make a mistake? Let's check the docs.

[np.var](https://numpy.org/doc/stable/reference/generated/numpy.var.html)

There is an optional arguement called ddof. By default **ddof** is **zero**. Basically, this mean it calculates the variance using the population variance formula. But the formula that we learnt in the class is an unbiased estimator of the variance.
So, let's use that.


```python
np.var(X0, ddof =1)
```




    np.float64(0.09834100691946199)



Let's do a exercise.
1.  Create a matrix M of 10 rows and 8 columns, fill with it with random values.
2.  Calculate the multi dimensional mean (represent the multi dimensional mean as a vector)
3.  Calculate the min, max, variance and SD of each attribute.
4.  Create matrix R with range normalized data.
5.  Create matrix Z with z-scores.
