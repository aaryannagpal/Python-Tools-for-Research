# Week 2
### Topics covered
- Deeper into Python and OOP
- Scientific and vectorized computing using ```matplotlib```
- Plotting basics with ```matplotlib```
- Introduction to ```random``` module
- Introduction to ```datetime``` module

## Deeper into Python
### Scope Rules
Scope rules follow the <b>LEGB</b> rule, which stands for: <i><b>L</b>ocal, <b>E</b>nclosing function, <b>G</b>lobal and <b>B</b>uilt-In</i>

An example demonstrating the same:

```
def update(n,x):
  n = 2
  x.append(4)
  print("Updated: ", n, x)

def main():
  n = 1
  x = [0, 1, 2, 3]
  print("Main: ", n, x)
  update(n,x)
  print("Main: ", n, x)
  
main()
```
The following output is obtained:
```
Main: 1 [0, 1, 2, 3]
Updated: 2 [0, 1, 2, 3, 4]
Main: 1 [0, 1, 2, 3, 4]
```
### Classes and Object-Oriented Programming
Classes can be used to created a new object in Python to help in programming to one's requirements.

A class specifies the internal structure of these new types of objects, including what methods and operations they support, but it does not create any object of that type. When an object of a particular type is created, that object is sometimes called an <i>Instance</i> of that type.

The functions defined inside a class are known as <i>instance methods</i> because they operate on an instance of the class. By convention, the name of the class instance is called <i>self</i>, and it is always passed as the first argument to the functions defined as part of a class.

#### Inheritence

To create an object which follows properties from a pre-existing object, the concept of <i>Inheritence</i> is used. When a class is created via inheritance, the new class inherits the attributes defined by its base class, the class it is inheriting. 

For example, when we define a new object by writing ```class MyList(list):```, the object inside the parentheses is used to specify Python of Inheritence.

#### Sample class
```
class MyList(list):
  def remove_min(self):
    self.remove(min(self))
  def remove_max(self):
    self.remove(max(self))
```
The above creates a new object known as ```MyList``` which has the properties of the pre-defined object ```list``` and additonal functions that were mentioned as well.

## NumPy
### Arrays
- NumPy arrays are n-dimensional array objects which are a core component of scientific and numerical computation in Python.
- Unlike dynamically growing Python lists, NumPy arrays have a size that is fixed when they are constructed.
- Elements of NumPy arrays are also all of the same data type leading to more efficient and simpler code than using Python's standard data types.
- By default, the elements are floating point numbers.

#### Zeros and Ones
We can construct vectors and matrices only containing 0 or 1 using NumPy

```
import numpy as np

zero_vector = np.zeros(3)
zero_matrix = np.zeros((2,3)) # 2 x 3 matrix
```
```np.ones``` is used similarly to create arrays of 1s.

#### Empty array
We can also initialize an empty array using ```np.empty``` which allocates the requested space for the array, but does not initialize it.

If you are dealing with a very large array and you know for sure that you will be updating each element of the array, this could save you some computation time because Python doesn't need to initialize the array.

#### Specific values
We use ```np.array``` to create an array for the values given as an argument.

```
x = np.array([1, 2, 3]) #One Dimensional
X = np.array([[1, 2], [3, 4]]) #Two Dimensional
```
#### Operations on Arrays
- Element-wise operations happen if the operand arrays are of the same size. 
```
np.array([1, 2, 3]) + np.array([4, 5, 6)]
>>> array([5, 7, 9])
np.array([1, 2, 3]) * np.array([4, 5, 6)]
>>> array([4, 10, 18])

np.array([[1, 2], [3, 4]]) + np.array([[4, 5], [6, 7]])
>>> array([[5, 7],
           [9, 11]])
```
Note: If the ```+``` operator is used with ```lists```, the operands are <b>concatenated</b> rather than added element-wise.
```
[1, 2] + [3, 4]
>>> [1, 2, 3, 4]
```
- Slicing
```
x = np.array([1, 2, 3, 4])
X = np.array([[1, 2], [3, 4]])

x[0:2] #works like in a list
>>> [1, 2]

X[1,:] # or X[1] returns row at index 1
>>> [3, 4]
X[:,1] # returns column at index 1
>>> [2, 4]
```
- Indexing
```
# can access elements in arrays by passing lists and arrays.
z = np.array([1, 3, 5, 7])
ind = [0, 2, 3]
z[ind]
>>> array([1, 5, 7])

# can also access Boolean arrays
z > 6
>>> array([False, False, False, True], dtype=bool)

# can also use the boolean array as logical index
z[z > 6]
>>> array([7]) #only displayes the elements who have True as corressponding values
```
Note: For all cases of indexed arrays, what is returned is a copy of the original data, not a view as one gets for slices. Meaning, the original values will change if values are modified after accessing using slicing, unlike when values are accessed using indexing.

#### Constructing linearly and logarithmically spaced arrays
```
# (starting point - in the scale of the function, ending point - in the scale of the function, number of steps)
np.linspace(0, 100, 10)
>>> array([0, 11.111, 22.222, 33.333, 44.444, 55.556, 66.667, 77.778, 88.889, 100])
        
np.logspace(1, 2, 10) #for 10, it is 1 as log(10) = 1, and for 100 it is 2 as log(100) = 2
>>> array([10, 12.915, 16.681, 21.544, 27.825, 35.938, 46.415, 59.94842503, 77.426, 100])

np.logspace(np.log10(250), np.log10(350), 3)
>>> array([250, 295.803, 350])
```
#### Shape and Size
Use ```np.shape``` to know the array's dimensions and use ```np.size``` to know the number of elements in the array

#### Random in NumPy
NumPy has its own random module which can be accessed using ```np.random```

To create an array of 10 elements with random uniform distribution, we type ```np.random.random(10)``` and ```np.random.normal(10)``` for random normal distribution.
Using ```np.any(*condition*)``` we can check if an array as any element that satisfies the condition given. Similarly, ```np.all(*condition*)``` can be used to check if all the elements in the array satisfy the condition. In both cases, a Boolean value is returned.

```
x = 20
not np.any([x%i == 0 for i in range(2, x)]) # to check if x is prime or not
```
## Matplotlib and Pyplot
Since Matplotlib is a huge library, we used Pyplot for our task. Pyplot is a collection of functions that make matplotlib work like Matlab.

We access it by ```import matplotlib.pyplot as plt```.

Every plot is shown by using ```plt.show()```.

### plt.plot
This function can be used to plot lines and markers. 

The simplest version of plot has just one argument, and it specifies the y-axis values that are to be plotted, against its corresponding index value on the x-axis. Otherwise, the plot function takes in 2 values, with the first one corressponding to the x-axis and the second one corressponding to the y-axis.

A third argument to the plot function can be given, which is a format string that specifies color, marker, and line type for the plot, known as <b>Keyword Arguments</b>.

_**Keyword argument is an argument which is supplied to the function by explicitly naming each parameter and specifying its value**_

### Customizing the Plots
- ```plt.xlabel``` and ```plt.ylabel``` is used to set the names for the axes. The label support LaTeX format as well.
- ```plt.axis``` are used to define custom axis sizes. The format for this is ```plt.axis(xmin, xmax, ymin, ymax)```

- To add legend to the plots, first the keyword argument ```label``` is mentioned while initialising the plots. To show the legend in the plots, ```plt.legend()``` is used. An additional keyword argument ```loc``` is used for specifying the specific location of the legend. Eg: ```plt.legend("Upper Left")```
- We use ```plt.savefig("name.type")``` to save the plot in the working directory.
- ```plt.semilogx()``` plots the x-axes on a log scale and the y in the original scale, ```plt.semilogy()``` plots the y-axes on the log scale and the x in the original scale, ```plt.loglog()``` plots both x and y on logarithmic scales.

### plt.hist

Used to create histograms for a dataset.

```np.hist(x)``` is used to create histograms for the data set ```x```. By default, hist uses 10 evenly spaced bins and optimizes both bin width and bin locations. To have custom bins and binwidth, the keyword parameter ```bins```. For _n_ number of bins, we write either ```bins = n``` or for specific spaces between values, we write ```bins = linspace(start, end, n+1)```.

```plt.subplot``` enables us to have several subplots within each figure and takes three arguments where the first two specify the number of rows and the number of columns in the subplot, and the third argument gives the plot number. The plot number always starts at 1 and are incremented across rows first.

Some keyword arguments: 
- ```histtype``` is used to set a particular type of histogram
- ```cumulative = True``` for creating a cumulative graph
- ```normed = True``` for normalizing the y-axis as propotions of data rather than frequency of data points.
