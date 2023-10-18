# *args vs ** kwargs

- *args
  - variable length variable
  - process as tuple in the function
```
def sum(*num):
    for n in num:
        print(n)

sum(1, 2, 3)
```

    - can also spread the list in the argument
```
def sum(a,b)

l=[1,2]
sum(*l)
```

- **kwargs
  - keyword arguments
  - pass as dictionary key word
  
```
def fun(**data):
    for key, value in data.items():
        print(f"{key} {value}"")

fun(name="abc", last_name="def")
```


