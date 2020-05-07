# Python good practices

This document show how to write readable source code in Python.

### Shebang
#### Always start main python file with correct shebang

```python
#!/usr/bin/env python3
```

### Module level dunders
#### Always write module level dunders
#### Before dunders use only imports from __future__
#### Other import should be after dunders
```python
#!/usr/bin/env python3

 from __future__ import * # Before dunders use only imports from future
 
 __all__ = ["a", "b"] # All data which can be imported from module
__version__ = '1.0'
__author__ = 'John Smith'
__email__ = 'john.smith@example.com'
__copyright___ = "Copyright (c) 2018 John Smith"

import sys # Other imports
```


### Variable
#### You should not mix camelCase and snake_case styles.
#### Use snake_case for name variable as suggested in PEP8
#### Variables should have short names that inform what they contains.
#### Write code in English language and avoid UTF8 chars.

**Very very bad**
```python
My_String = "Temporary value"
```

**Very bad**
```python
MyString = "Temporary value"
```

**Bad**
```python
This_is_my_string_variable = "Author: Draqun"
```

**Good**
```python
author_info = "Author: Draqun"
```

#### Using variable type in name is wrong!

**Bad**
```python
my_string = "Temporary value"
```

**Good**
```python
tmp = "Temporary value"
```

#### If variable need always some value use only if statement

**Very Bad**
```python
def func(some_value):
    if some_example_function(some_value):
        variable = another_variable
    else:
        variable = "Default Value"
```

**Not Bad**
```python
def func(some_value):
    variable = another_variable if some_example_function(some_value): else "Default Value"
```

**Good**
```python
def func(some_value):
    variable = "Default Value"
    if some_example_function(some_value):
        variable = another_variable
```

### If statement

#### Avoid comparison with True and False

**Bad**
```python
is_pony = True
...
if is_pony == True:
    ...
```

or

```python
is_hungry = False
...
if is_hungry == False:
    ...
```


**Good**
```python
is_pony = True
...
if is_pony:
    ...
```

or

```python
is_hungry = False
...
if not is_hungry:
    ...
```

#### Group expression using parentheses

**Bad**
```python
if len(groups) == 9 and cities and len(cities) == 7 and "Warsaw" in cities:
    pass
```

**Good**
```python
if (len(groups) == 9) and cities and (len(cities) == 7) and ("Warsaw" in cities):
    pass
```

### Class
#### CamelCase is better for class names than snake_case.
#### Class name should start with capital letter.

**Bad**
```python
class my_little_pony:
    def run_pony(self):
        ...
```

**Good**
```python
class MyLittlePony:
    def run_pony(self):
        ...
```

#### If class is empty create one-line class

**Bad**
If there is no docstring
```python
class Donkey:
    pass
```

**Good**
```python
class Donkey: pass
```
or
```python
class Donkey:
    """This is Donkey which eat grass"""
    pass
```

#### The names of the classes should be written in singular if they are not containers.
If you want add horses to your application create class for single entity.

**Bad**
```python
class Horses:
  """ This is horse class """
    pass
```

**Good**
```python
class Horse:
  """ This is horse class """
    pass
```

If you want create container class use plural names

**Bad**
```python
class HorsesConatiner:
    """ Horses container """
    pass
```

**Good**
```python
class Horses:
    """ Horses container """
    pass
```

#### Always set default values of class variables

**Very bad**
```python
class Horse:
    name = "Adolfo"
```

**Bad**
```python
class Horse:
    def __init__(self, name):
        if (name):
            self.name = name
        else:
            self.name = "Adolfo"
```
or

```python
class Horse:
    name = "Adolfo"

    def __init__(self, name):
        if(name):
            self.name = name
```

**Good**
```python
class Horse:
    def __init__(self, name="Adolfo"):
        self.name = name
```

#### Use single underscore as prefix of protected variable and double underscore as prefix of private variable.

```python
class Horse:
    def __init__(self):
        self.name = "Rafaello"  # Public variable
        self._stud = "Warsaw"  # Protected variable
        self.__medal_winner = False  # Private variable
```

#### Use the same rule to methods

```python
class Dog(Animal):
    def bark(self): # Public method
        ...

    def _owners_name(self): # Protected method
        ...

    def __vaccination_card_number(self): # Private method
        ...
```


### Function and methods
#### Use snake_case for function name and methods.

**Bad**
```python
def canWriteToFile(fileHandler):
    ...
```

**Good**
```python
def can_write_to_file(file_handler):
    ...
```

#### Use `*args` and `**kwargs` to pass arguments for nested (wrapped) function

**Bad**
```python
def path_is_correct(path):
    ...
    return path

def create_relative_path_for_file(filename, path):
    path = path_is_correct(path)
    ...

...
create_relative_path_for_file("shadow", "/etc")
```

**Good**
```python
def path_is_correct(path):
    ...
    return path

def create_relative_path_for_file(filename, *args, **kwargs):
    path = path_is_correct(*args, **kwargs)
    ...

...
create_relative_path_for_file("shadow", "/etc")
```

### Lists, tuples and dictionaries
#### Use tuples when quantity is constant.

```python
possible_names = ("John", "Joe", "Katherina")
```

#### Use list in other cases.

```python
tastes = ["ugly", "cherry", "strawberry"]
```

#### Use dictionary when you have key-value pairs

```python
cities_population = {"Moscow": "1 MLN", "Warsaw": "1.5 MLN"}
```

### Operators

#### Use `in` operator to check element is in container

**Good**
```python
if "Warsaw" in cities:
    pass
```

#### Use `not in` to ckeck element is not in container

**Good**
```python
if "Warsaw" not in cities:
    pass
```

#### Avoid negation of `in` and `not in` operators

**Bad**
```python
if not "Warsaw" in cities:
    pass
```

**Bad**
```python
if not "Warsaw" not in cities:
    pass
```

#### `in` keyword can be used with dictionary to check element exists in collection as a key

```python
cities_population = {"Moscow": "1 MLN", "Warsaw": "1.5 MLN"}
if "Warsow" in cities_population:
    pass
```

### Sets

#### If you want check some value is in a big group use sets instead lists or tuples

**Bad**
```python
cities = ["Warsaw", "Berlin", "Moscow", "New York", "London", "Madrit", ...]

if city in cities:
    pass
```

**Good**
```python
cities = set(["Warsaw", "Berlin", "Moscow", "New York", "London", "Madrit", ...])

if city in cities:
    pass
```

#### Use duck typing if class are not exceptions

![Duck typing idea](https://cdn.meme.am/instances/67471500.jpg)

**Bad**
```python
class Animal: pass

class Horse(Animal):
    def get_noise():
        ...

class Duck(Animal):
    def get_noise():
        ...
```

**Good**
```python
class Horse:
    def get_noise():
        ...

class Duck:
    def get_noise():
        ...
```

#### Use inheritance when you create exceptions tree

```python
class NotAnimalException(BaseException): pass
class NotToyException(BaseException): pass
class NotMyLittlePonyToyException(NotToyException): pass
class NotHamsterException(NotAnimalException): pass
```

### Exceptions

#### Use try except block only for part of code which raises exceptions

**Bad**
```python
def send_message(message):
    ... # some action before try except
    try:
        message_striped = message.strip()
        ... # Some action for sending
    except AttributeError:
        ... # Some error handling
```

**Good**
```python
def send_message(message):
    ... # some action before try except
    try:
        message_striped = message.strip()
    except AttributeError:
        ... # Some error handling
    else:
        ... # Some action for sending
```
### Other
#### Always on top file put info about interpreter and encoding

For Python 2 and emacs encoding
```python
#!/usr/bin/env python2.7
#-*- coding:utf-8 -*-
```
or Python 3 and vim encoding
```python
#!/usr/bin/env python3
```


#### Always write file with encoding UTF-8
#### Always create file requirements.txt and put there names and version library
  used in project

Eg.
 ```
 Django==1.8.2
 wheel==0.26.0
 ```

#### Create every class in own file
#### Create modules for group of class
#### Use __init__ files for expose public class and for hidding internal modules
#### Do not write code line longer than 80 characters
#### Set last in file empty

#### Instead print debuging use pdb module

 # If you want more go to https://www.python.org/dev/peps/
