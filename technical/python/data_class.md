# Data class (documented)
- introduced in python 3.7
```python
from dataclasses import dataclass
from typing import List

@dataclass
class Person():
    name:str ="Peter" # default value
    age: int=10
    coordinates: List[int]

 Person(name="Joe", age=20)   
```

- dataclass default implement
  - `def __repr__(self) # to string
  - comparison
    - `Person()==Person()` #output True
    - implement `__eq__` method
    - if not dataclass, result is False
  
- sorting
```
@dataclass(order=True)
clas Person():
  sort_index: int=field(int=False, repr=False)
  age: int

  def __post_init__(self):
    self.sort_index=self.age
```

- immuatable
- `@databaseclass(frozen=True)`

- dataclass support inheritance
