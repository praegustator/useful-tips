## Jupyter Notebook Hacks

```python
import pandas as pd
```

---

* Auto reload modules with every second cell run:
```python
%load_ext autoreload
%autoreload 2
```

---

* Do not truncate values in the dataframe `df`:
```python
with pd.option_context('display.max_colwidth', -1): 
    display(df)
```

* Show all columns in the dataframe `df`:
```python
with pd.option_context('display.max_columns', None): 
    display(df)
```

* Show all rows in the dataframe `df`:
```python
with pd.option_context('display.max_rows', None): 
    display(df)
```

* Combination of three above:
```python
with pd.option_context('display.max_colwidth', -1,
                       'display.max_rows', None,
                       'display.max_columns', None): 
    display(df)
```

* Pretty JSON print with russian characters:
```python
print(json.dumps(data, indent=4, ensure_ascii=False))
```