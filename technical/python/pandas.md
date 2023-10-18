# Pandas best practice

https://github.com/joshlk/pandas_style_guide

- column selection by string
```
# Good
df['column']

# Bad
df.column
```
- reassign is better than in place mutate
  - performance is the same

```
# Good
df = df.drop(columns='A')

# Bad
df.drop(columns='A', inplace=True)
```  

- schem contract
```
# Good (file input)
df = pd.read_csv('data.csv')
df = df[['col1', 'col2', 'col3']]

# Good (collection input)
df = pd.DataFrame.from_records(list_of_dicts)
df = df[['col1', 'col2', 'col3']]

# Good
df = pd.read_csv('data.csv', dtype={'col1': 'str', 'col2': 'int', 'col3': 'float'})
df = df[['col1', 'col2', 'col3']]
```

- merge contract
```
# Good
df_3 = df_1.merge(
    df_2,
    how='inner',
    on='col1',
    validate='1:1'
)

# Bad
df_3 = df_1.merge(df_2)
```
- empty column
```
# Good
df['new_col_float'] = np.nan
df['new_col_int'] = pd.Series(dtype='int')
df['new_col_str'] = pd.Series(dtype='object')

# Bad
df['new_col_int'] = 0
df['new_col_str'] = ''
```

- Dataframe mutability
  - don't pass DF to function and add column for data interchange, should use dataclass
``` 
# Bad
def func_1(df: pd.DataFrame) -> pd.DataFrame:
    df['new_col'] = df['col1'] + 1
    return df

df = func_1(df)
```
