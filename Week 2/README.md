# Week 2
### Topics covered
- Deeper into Python and OOP
- Scientific and vectorized computing using ```matplotlib```
- Plotting basics with ```matplotlib```
- Introduction to ```random``` module
- Introduction to ```datetime``` module

## Scope Rules
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
## Classes and Object-Oriented Programming
Classes can be used to created a new object in Python to help in programming to one's requirements.

A class specifies the internal structure of these new types of objects, including what methods and operations they support, but it does not create any object of that type. When an object of a particular type is created, that object is sometimes called an <i>Instance</i> of that type.

The functions defined inside a class are known as <i>instance methods</i> because they operate on an instance of the class. By convention, the name of the class instance is called <i>self</i>, and it is always passed as the first argument to the functions defined as part of a class.

### Inheritence

To create an object which follows properties from a pre-existing object, the concept of <i>Inheritence</i> is used. When a class is created via inheritance, the new class inherits the attributes defined by its base class, the class it is inheriting. 

For example, when we define a new object by writing ```class MyList(list):```, the object inside the parentheses is used to specify Python of Inheritence.

### Sample class
```
class MyList(list):
  def remove_min(self):
    self.remove(min(self))
  def remove_max(self):
    self.remove(max(self))
```
The above creates a new object known as ```MyList``` which has the properties of the pre-defined object ```list``` and additonal functions that were mentioned as well.
