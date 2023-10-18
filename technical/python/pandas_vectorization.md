# Vectorization Pandas

https://tryolabs.com/blog/2023/02/08/top-5-tips-to-make-your-pandas-code-absurdly-fast


-vectorized operation allow operation on whole dataframe or columns instead of using loop

```
def count_loop(X, target: int) -> int:
    return sum(x == target for x in X["column_1"])

def count_vectorized(X, target: int) -> int:
    return (X["column_1"] == target).sum()

def offset_loop(X, days: int) -> pd.DataFrame:
        d = pd.Timedelta(days=days)
    X["column_const"] = [x + d for x in X["column_10"]]
    return X

def offset_vectorized(X, days: int) -> pd.DataFrame:
    X["column_const"] = X["column_10"] + pd.Timedelta(days=days)
    return X
```    
- vectorized function over 50X fasters than loop



```
remove_col = "column_2"
words_to_remove_col = "column_4"

def remove_words(
    remove_from: str, words_to_remove: str, min_include_word_length: int = 4
) -> str:
    words_to_exclude = set(words_to_remove.split(" "))
    no_html = re.sub("<.*?>", " ", remove_from)
    include_words = [
        x
        for x in re.findall(r"\w+", no_html)
        if (len(x) >= min_include_word_length) and (x not in words_to_exclude)
    ]
    return " ".join(include_words)


def loop(df: pd.DataFrame, remove_col: str, words_to_remove_col: str) -> list[str]:
    res = []
    i_remove_col = df.columns.get_loc(remove_col)
    i_words_to_remove_col = df.columns.get_loc(words_to_remove_col)
    for i_row in range(df.shape[0]):
        res.append(
            remove_words(
                df.iat[i_row, i_remove_col], df.iat[i_row, i_words_to_remove_col]
            )
        )
    return result

```

1. use apply (1.9X faster)
   ```
   def apply(df: pd.DataFrame, remove_col: str, words_to_remove_col: str) -> list[str]:
    return df.apply(
        func=lambda x: remove_words(x[remove_col], x[words_to_remove_col]), axis=1
    ).tolist()
    ```

2. limit the subset of apply (2.1X faster)
    - each iteration generate the df, thus cutting the input df will help
  ```
  def apply_only_used_cols(df: pd.DataFrame, remove_col: str, words_to_remove_col: str) -> list[str]:
    return df[[remove_col, words_to_remove_col]].apply(
        func=lambda x: remove_words(x[remove_col], x[words_to_remove_col]), axis=1
    )
  ```
3. itertuples + list comprehension (4.6X faster)
    - list comprehension is 2 to 3 times faster than loop
  
   ```
   def itertuples_only_used_cols(df: pd.DataFrame, remove_col: str, words_to_remove_col: str) -> list[str]:
    return [
        remove_words(x[0], x[1])
        for x in df[[remove_col, words_to_remove_col]].itertuples(
            index=False, name=None
        )
    ]
    ```
4. zip + list comprehension (4.6X faster)
    ```
    def zip_only_used_cols(df: pd.DataFrame, remove_col: str, words_to_remove_col: str) -> list[str]:
        return [remove_words(x, y) for x, y in zip(df[remove_col], df[words_to_remove_col])]
    ```

5. to_dict + list comprehension (3.9X faster)
   ```
   def to_dict_only_used_columns(df: pd.DataFrame) -> list[str]:
        return [
            remove_words(row[remove_col], row[words_to_remove_col])
            for row in df[[remove_col, words_to_remove_col]].to_dict(orient="records")
        ]
   ```



## https://plainenglish.io/blog/pandas-how-you-can-speed-up-50x-using-vectorized-operations   

- Iterrows
  - avoid to use becaus slow

```
for index, row in df.iterrows():
```

- Series Apply
```
def some_fun(series: pd.Series, other_argument: float) -> pd.Series:
    

df['col']=df['col'].apply(some_fun, args=(1.2))
```
- Series Map
  - a bit faster than series apply
```
df['col']=df['col'].map(lambad x: some_fun(x, other_argument=1.2))
```

- vectorized series
  - vectorized using Numpy
  - using optimzied compiled C code to perform operation, apply instruction on multiple elements at the same time
```
 df['col']=df['col']-np.mean(df['col'])/np.std(df['col'])
```

- vectoriezed array (fastest)
  - using numpy array directly

```
numpy_array: np.array=df['col'].values 
df['col']=numpy_array-np.mean(numpy_array)/np.std(numpy_array)
```
