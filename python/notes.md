

# Docorators

Docorators are a powerful and flexible way to modify or extend the behavior of functions or methods. They all you to wrap another function in order to add functionality to it without modifying it's structure.


A decorator is essentially a callable (like a function) that takes another function as an argument and returns a new function that usually extends the behavior of the orginal function

```py
def simple_decorator(func):
    def wrapper():
	print("Before calling the function")
	func()
	print("After calling the function")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello")

# Using the decorated function
say_hello()
```

`simple_decorator` is the decorator function that takes another function `func` as an argument.

Inside `simple_decorator`, we define a nested function `wrapper` that will wrap the original function `func`

`@simple_decorator` is a synatical sugar to apply the decorator to `say_hello` function.
It's equivalent to `say_hello = simple_decorator(say_hello)`

When `say_hello()` is called, it actually calls the `wrapper` function inside `simple_decorator`, which prints
messages before and after calling the original `say_hello` function.


### example 2

```python
def repeat_decorator(times):
    def decorator(func):
	def wrapper(*args, **kwargs):
	    for _ in range(times):
		func(*args, **kwargs)
	return wrapper
    return decorator

@repeat_decorator(3)
def greet(name):
    print(f"Hello {name}!")

# Using the decorated function
greet("Kulang")
```

`repeat_decorator` is a function that takes an argument `times` and returns a `decorator`.

`decorator` is the actual decorator that takes `func` as an argument and returns the `wrapper` function.

`wrapper` calls the original function `func` a specified number of times(`times`)


