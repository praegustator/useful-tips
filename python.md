## Jupyter Notebook Hacks

* Auto reload modules with every second cell run:
```python
%load_ext autoreload
%autoreload 2
```

* Do not truncate values in the dataframe `df`:
```python
with pandas.option_context('display.max_colwidth', -1): 
    display(df)
```