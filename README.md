# Private Method Decorator
```python
def private_method(method):
    def wrapper(self, *args, **kwargs):
        if not isinstance(self, method.__qualname__.split('.')[0]):
            raise AttributeError(f"{method.__name__} cannot be called outside of its class.")
        return method(self, *args, **kwargs)
    return wrapper

class MyClass:
    @private_method
    def my_private_method(self, arg1, arg2):
        return arg1 + arg2

# This will work fine
obj = MyClass()
result = obj.my_private_method(3, 4)
print(result)  # Output: 7

# This will raise an AttributeError
try:
    MyClass.my_private_method(3, 4)
except AttributeError as e:
    print(e)  # Output: my_private_method cannot be called outside of its class.
```
