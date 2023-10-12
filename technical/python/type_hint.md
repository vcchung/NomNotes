# Type Hint (documented)

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
