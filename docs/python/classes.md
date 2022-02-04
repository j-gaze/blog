## Static and Dynamic fields
```python
class Astronaut:
    firstname = 'Mark'
    lastname = 'Watney'

    def __init__(self):
        self.firstname = 'Mark'
        self.lastname = 'Watney'
```

## @staticmethod
Klasy statyczne - nie wymagają tworzenia obiektu 
```python
class Uni:
  @staticmethod
  def hello():
      print("Hello")
```
## @classmethod
Klasycznie 
```python
class Student(object):

    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

scott = Student('Scott',  'Robinson')
```
Można zastąpić classmethod
```python
class Student(object):

    # Constructor removed for brevity

    @classmethod
    def from_string(cls, name_str):
        first_name, last_name = map(str, name_str.split(' '))
        student = cls(first_name, last_name)
        return student

    @classmethod
    def from_json(cls, json_obj):
        # parse json...
        return student

    @classmethod
    def from_pickle(cls, pickle_file):
        # load pickle file...
        return student
```        

## @dataclass
fields may optionally specify a default value, using normal Python syntax:
```python
@dataclass
class C:
    a: int       # 'a' has no default value
    b: int = 0   # assign a default value for 'b'
```
In this example, both a and b will be included in the added __init__() method, which will be defined as:
```python
def __init__(self, a: int, b: int = 0):
```
TypeError will be raised if a field without a default value follows a field with a default value. This is true whether this occurs in a single class, or as a result of class inheritance.