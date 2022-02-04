# Data Structures in Python
## Types and Sequences (Data Structures)<br/>
int, float, complex, bool, NoneType<br/>
str, bytes<br/>
bytearray, list, tuple, set, frozenset, dict<br/>

| mutable   | immutable             |
| ----------| --------------------  |
|           | int                   |   
|           | float                 |
|           | bool                  |
|           | complex               |
|           | NoneType              |
|           | str                   |
| bytearray | bytes                 |
| list      | tuples                |
| set       | frozenset             |
| dict      | mappingproxy          |
| array     |                       |
| class     |                       |
| dataclass | dataclass(frozen=True)|

np.array<br/>
pd.Series<br/>
pd.DataFrame<br/>
pd.SparseArray<br/>

## Python Arrays

### List:
- Used in JSON format
- Useful for Array operations
- Used in Databases

Listy mogą zawierać te same wartości wiele razy możemy dodawać elementy 
```python
List = ['Milk', 'Bread', 'Eggs', 'Eggs', True, False, {}, (), ['a', 'b', 'c']]
```

### Tuple:
- Used to insert records in the database through SQL query at a time.Ex: (1.’sravan’, 34).(2.’geek’, 35)
- Used in parentheses checker
  
Krotki są stałe po definicji nie możemy dodać następnych elementów
```python
Tuples = ('Milk', 'Bread', 'Eggs',)
```

### Set:
- Finding unique elements
- Join operations

Jest to zbiór danych które nie mogą się powtarzać 
```python
Sets = {'Milk', 'Bread', 'Eggs'}
String = "Python for Everybody True"
```

### Dictionary:
- Used to create a data frame with lists
- Used in JSON

Słowniki key-value pairs
```python
Dict = {
    'Milk': 'Goats Milk',
    'Eggs': 'Free Range Eggs',
}
```

## Computational complexity
- list - O(n)
- tuple - O(n)
- set - O(1)
- dict - O(1) - in keys

- memory complexity<br/>
- cognitive complexity (and, or, not)<br/>
- branches (if, try, for, while)<br/>
- bytes<br/>
    - for low level operations (sockets, files in binary mode)<br/>
    - if you open a picture<br/>
    - if transfer data over internet<br/>
## str - is unicode

## Singletons
```python
True
False
None
```
## you create an instance of a class dict
```python
data = dict()
data = tuple()
data = list()
data = set()
data = frozenset()
data = str()
data = int()
data = float()
```

## syntactic sugar
```python
data = {}
data = ()
data = []
data = ''
data = 0
data = 0.0
from array import array
data = array('B')
```
```python
from collections import namedtuple
from dataclasses import dataclass
from typing import NamedTuple, TypedDict
```

## identifier and a scalar -> value
```python
point1_x = 1
point1_y = 2
point1_z = 3
point2_x = 4
point2_y = 5
point2_z = 6
## value and relation -> data
point1 = (1, 2, 3)
point2 = (4, 5, 6)


## data and contex -> information
point1 = {'x': 1, 'y': 2, 'z': 3}
point2 = {'x': 4, 'y': 5, 'z': 6}


## information and meaning -> classes
class Point:
x: int
y: int
z: int

def show(self):
return self.x, self.y, self.z


class Point(TypedDict):
x: int
y: int
z: int


## class
class Point:
x: int
y: int
z: int

point = Point()
point.x = 1
point.y = 2
point.z = 3
## init
class Point:
x: int
y: int
z: int

def __init__(self, x: int, y: int, z: int):
self.x = x
self.y = y
self.z = z


## dataclass
@dataclass
class Point:
x: int
y: int
z: int
```

## ARC - Automatic Reference Counting