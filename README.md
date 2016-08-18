# Python good practice

This document show how to write readable source code in Python.

### Variable
I think you should on start now how to write variable name

* You should now mixing camelCase and snake_case style are bad.
* Choose camelCase than snake_case. A lot of people like snake case but this
  style generate long names. If you want write clean and beautiful code use
  camelCase.
* Variables should has short names inform what it contains.

**Bad**
```python
This_is_my_string_variable = "Author: Draqun"
```

**Good**
```python
authorInfo = "Author: Draqun"
```

* Using variable type in name wrong!

**Bad**
```python
myString = "Temporary value"
```

**Good**
```python
tmp = "Temporary value"
```

* If variable need always some value use only if statement

**Very Bad**
```python
if someExpression:
    variable = anotherVariable
else:
    variable = "Default Value"
```

**Not Bad**
```python
variable = anotherVariable if someExpression: else "Default Value"
```

**Good**
```python
variable = "Default Value"
if someExpression:
    variable = anotherVariable
```
### Class
* CamelCase is better for classes and methods name than snake_case.
* Class name should start with capital letter, methods and variables should start
  with small letter.

**Bad**
```python
class my_little_pony(object):
    def run_pony(self):
        ...
```

**Good**
```python
class MyLittlePony(object):
    def runPony(self):
        ...
```

* If class is empty create one-line class

**Bad**
```python
class Donkey(object):
    pass
```

**Good**
```python
class Donkey(object): pass
```

* Always set default values of class variables

**Very bad**
```python
class Horse(object):
    name = "Adolfo"
```

**Bad**
```python
class Horse(object):
    def __init__(self, name):
        if (name):
            self.name = name
        else:
            self.name = "Adolfo"
```
or
```python
class Horse(object):
    name = "Adolfo"

    def __init__(self, name):
        if(name):
            self.name = name
```

**Good**
```python
class Horse(object):
    def __init__(self, name="Adolfo"):
        self.name = name
```

### Function
* Use camelCase for function name

**Bad**
```python
def can_write_to_file(file_handler):
    ...
```

**Good**
```python
def canWriteToFile(fileHandler):
    ...
```

* Use `*args` and `**kwargs` to pass arguments for nested function

**Bad**
```python
def pathIsCorrect(path):
    ...
    return path

def createRelativePathForFile(filename, path):
    path = pathIsCorrect(path)
    ...

...
createRelativePathForFile("shadow", "/etc")
```

**Good**
```python
def pathIsCorrect(path):
    ...
    return path

def createRelativePathForFile(filename, *args, **kwargs):
    path = pathIsCorrect(*args, **kwargs)
    ...

...
createRelativePathForFile("shadow", "/etc")
```

### Lists, tuples and dictionaries
* Use tuples when quantity is constant.

```python
possibleNames = ("John", "Joe", "Katherina")
```

* Use list in other cases.

```python
tastes = ["ugly", "cherry", "strawberry"]
```

* Use dictionary when you have key-value pairs

```python
citiesPopulation = {"Moscow": "1 MLN", "Warsaw": "1.5 MLN"}
```

* Use `in` to check value exists in collection

**Bad**
```python
bandToFind = "Rammstein"
for (band in bands):
    if (bandToFind == band):
        ...
```

**Good**
```python
bandToFind = "Rammstein"
if (bandToFind in bands):
    ...
```

* `in` keyword can be used with dictionary to check element exists in collection

```python
citiesPopulation = {"Moscow": "1 MLN", "Warsaw": "1.5 MLN"}
if ("Warsow" in citiesPopulation)
...
```

### Inheritance

* Always inherit from `object` if you do not have other class.

**Bad**
```python
class Animal():
    ...
```

**Good**
```python
class Animal(object):
    ...
```

* Use duck typing if class are not exceptions

![Duck typing idea](https://cdn.meme.am/instances/67471500.jpg)

**Bad**
```python
class Animal(object): pass

class Horse(Animal):
    def getNoise():
        ...

class Duck(Animal):
    def getNoise():
        ...
```

**Good**
```python
class Horse(object):
    def getNoise():
        ...

class Duck(object):
    def getNoise():
        ...
```

* Use inheritance when you create exceptions tree

```python
class NotAnimalException(BaseException): pass
class NotToyException(BaseException): pass
class NotMyLittlePonyToyException(NotToyException): pass
class NotHamsterException(NotAnimalException): pass
```

### Other
* Always on top file put info about interpreter and encoding

For Python 2 and emacs encoding
```python
#!/usr/bin/env python2.7
#-*- coding:utf-8 -*-
```
or Python 3 and vim encoding
```python
#~/usr/bin/env python3
# vim: set fileencoding=UTF-8 :
```


* Always write file with encoding UTF-8
* Always create file requirements.txt and put there names and version library
  used in project

Eg.
 ```
 Django==1.8.2
 wheel==0.26.0
 ```

 * Create every class in own file
 * Create modules for group of class
 * Use __init__ files for expose public class and for hidding internal modules
 * Do not write code line longer than 80 characters
 * Set last in file empty

 # If you want more go to https://www.python.org/dev/peps/
