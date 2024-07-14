# Data structure types

In Python, a variable can be assigned various types of values, including the following:

Python does not have a concept of "undefined" like JavaScript, so if a variable is declared without being assigned a value, it will raise an error. Also, Python doesn't have a distinct "null" value; `None` serves that purpose.
1. ## **None**:
   This is a special constant in Python that represents the absence of a value or a null value.
    ```python
    a = None
    ```

3. ## **Integers**:
   Whole numbers can be assigned to variables.
    ```python
    b = 5
    ```

4. ## **Floating-Point Numbers**:
   Decimal numbers can be assigned to variables.
    ```python
    c = 3.14
    ```

5. ## **Complex Numbers**:
   Complex numbers, which have a real and imaginary part, can also be assigned to variables.
    ```python
    d = 2 + 3j
    ```

6. ## **Strings**:
    A sequence of characters can be assigned to variables.
    ```python
    e = "Hello, World!"
    ```

7. ## **Booleans**:
    The `True` and `False` boolean values can be assigned to variables.
    ```python
    isReady = True
    ```

8. ## **Lists**:
    A list is an ordered collection of elements, which can be of mixed types.
    ```python
    list = [1, 2, 3, "apple"]
    ```

    NOTE: You can't do this:
    ```python
    list = [x = 5, y = 10]
    ```

9. ## **Arrays**:
    Although Python does not support arrays natively, you can use `array` or `numpy` modules for it. In general, they are more memory efficient than lists.  

    ```python
    from array import array
    python_array = array( 'i', [1, 2, 3, 4, 5] )  # 'i' is the type code for integers
    ```

    ```python
    import numpy as np
    numpy_array = np.array( [1, 2, 3, 4, 5] ) # For memory efficient calculations
    ```

10. ## **Tuples**:
    Similar to lists, but tuples are **immutable** (elements cannot be changed).
    ```python
    unchangeable = (1, 2, "banana")
    ```

11. ## **Dictionaries**:
    Dictionaries store **key-value** pairs.
    ```python
    dictionary = { "name": "Alice",
                   "age": 30 }
    ```

12. ## **Sets**:
    Sets are an **unordered** collection of **unique elements**.
    ```python
    collection = { 1, 2, 3 }
    ```

13. ## **Functions**:
    You can assign functions to variables.
    ```python
    def greet():
        return "Hello"
    
    greeting = greet
    print ( greet() )  # Output: Hello
    ```

14. ## **Objects**:
    Instances of classes can be assigned to variables.
    ```python
    class Person:
    
        # Constructor
        def __init__(self, name):
            self.name = name
    
    customer = Person("Bob")
    ```

15. ## **Modules**:
    You can assign imported modules to variables.
    ```python
    import math as math_module
    
    m = math_module
    
    print(m.sqrt(16))  # Output: 4.0
    ```

16. ## **Unspecified amount of arguments**:
If the number of arguments is unknown, add a `*` before the parameter name:

```python
def my_function( *kids ):

   print("The youngest child is " + kids[2])
   # OUTPUT: `The youngest child is Linus`

my_function("Emil", "Tobias", "Linus")
```python

16. ## **Classess**:
```python
# declare a class
class Employee:


   count = 0

   # Constructor
   def __init__(self, parameter_balance):
      self._balance = parameter_balance

   @property
   def balance(self):
      return self._balance
   
   def deposit(self, amount):
     if amount < 0:
         raise ValueError("Amount cannot be negative")
     self._balance += amount
```python

```python

# Class
class Car:

    # Class (Static) attributes
    # Variables of a class that are shared between all of its instances. They are
    # variables that are inherited by every object of a class. The value of class attributes remain the same for every new object
    # Attributes hold the internal state of objects
    # If you expose the attributes of a class to your users, then those attributes automatically become part of the class’s public API
    #  They’ll be public attributes, which means that your users will directly access and mutate the attributes in their code.
    wheels = 4  # All cars have 4 wheels

    # Constructor: Constructors are special methods used to initialize new objects
    def __init__( self, manufacturer, model, year ):
        # Instance attributes
        # Owned by one specific instance of the class and are not shared between instances.
        self.manufacturer   = manufacturer
        self.model          = model
        self.year           = year
        # Pseudo-Private variables:
        # Python doesn’t have the notion of access modifiers, such as private, protected, and public, to restrict access
        # to attributes and methods in a class. In Python, the distinction is between public and non-public class members.
        # If you want to signal that a given attribute or method is non-public, then you should use the well-established
        # Python convention of prefixing the name with an underscore (_).
        # Note that this is just a convention. It doesn’t stop you and other programmers from accessing the attributes
        # using dot notation, as in obj._attr. However, it’s bad practice to violate this convention.
        self._mileage       = 0        # Pseudo-Private variable, marked with `_`

    # Getters and Setters
    # If you come from a language like Java or C++, then you’re probably used to writing getter and setter methods for
    # every attribute in your classes. These methods allow you to access and mutate private attributes while maintaining
    # encapsulation. If an attribute is likely to change its internal implementation, then you should use getter and setter methods.

    # Property: Getter for mileage
    # Getter: A method that allows you to access an attribute in a given class
    @property
    def mileage(self):
        return self._mileage

    # Setter for odometer
    # Setter: A method that allows you to set or mutate the value of an attribute in a class
    @mileage.setter
    def mileage(self, parameter_input):
        self._mileage   =   parameter_input
        """
        if parameter_input >= self._mileage:
            self._mileage   = parameter_input
        else:
            print("You can't roll back the mileage!")
        """

    # Usage: `del object.mileage`
    @mileage.deleter
    def mileage(self):
        # Deleter
        del self._mileage


    # Default method: Cannot be called without an object instance being created from the class
    def description(self):
        return f" {self.year} {self.manufacturer} {self.model} "

    # Class method: Can be called `without instantiating an object of this class`
    # In fact, if you define something to be a class method, it is probably because you intend to call it from the class
    # rather than from a class' instance. If your method accesses other variables/methods in your class then use @classmethod
    @classmethod
    def from_string(cls, car_string):
        make, model, year = car_string.split('-')
        return cls(make, model, int(year))

    # @Static method: Can be called without instantiating an object of this class
    # unlike class methods, static methods are immutable via inheritance: the method that knows nothing about the class
    # or instance it was called on. It just gets the arguments that were passed, no implicit first argument.
    # With `static methods`, neither self (the object instance) nor cls (the class) is implicitly passed as the first argument
    # This is useful when you want the method to be a factory for the class
    # A staticmethod isn't useless - it's a way of putting a function into a class (because it logically belongs there),
    # while indicating that it does not require access to the class. if your method does not touches any other parts of the class
    # then use @staticmethod. It does not know the instance or class it is called from.
    @staticmethod
    def is_motor_vehicle():
        return True

# Using the class with properties
my_car = Car("Toyota", "Corolla", 2020)

print(f"my_car: { vars(my_car) }")

# Accessing the property (getter)
print(my_car.mileage)

# Setting a new value (setter)
my_car.mileage = 15000
print(my_car.mileage)

# Data structure types

# Trying to roll back the my_car.mileage = 15000
my_car.mileage = 10000  # This will trigger the print statement in the setter
del my_car.mileage
```

# Misc
## 1. Function return type with multiple values is `tuple`
If you have a function like this:
```python
   function math()
      observation = 1
      info = 2
      return observation, info
```
and you try to assign it to a sinle variable, the resulting data structure of that variable will be `tuple`

```python
tuple_result = math()
```
## 2. Class inheritance
Here `ModifiedCar` inherits all the functionality of parent class `Car`, so it can modify or extend it.
```python
class ModifiedCar( Car ):
```
## 3. Instantiate inherited properties of parent class
```python
class ModifiedCar( Car ):
   
   def __init__(self, params): # Define the constructor function of the current class

      super( Car, self ).__init__() # Initiate the constructor of the parent class. Without this features of `Car` won't be initialized/copied alongside `ModifiedCar`
```
