# Type Hint 

```python
def sample_function(name: str)-> str:
    return f'Hi {name}'
```

- python interpretor ignore type hint totally
- require static type check tool: `mypy`
  - `pip install mypy`
  - `mypy app.py`

- Union Type
  - `def add(x: Uniton[float, int])-> Uniton[float, int]`
- Type alias
  - `number=Union[int, float]`
  - `def add(x: number)->number`

- Built in types
  - `List[int]`
  - `Tuple[int]`
  - `Dict[str, str]`
  - `Set[int]`
  - Frozenset
  - Sequence
  - Mapping
  - ByteString
  - None

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
 
