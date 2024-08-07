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

* Unfold lists to separate columns in the pandas dataframe:
```python
def unfold_columns(df, columns=[], strict=False):
    assert isinstance(columns, list), "Columns should be a list of column names"
    if len(columns) == 0:
        columns = [
            column for column in df.columns 
            if df.applymap(lambda x: isinstance(x, list)).all()[column]
        ]
    else:
        assert(all([(column in df.columns) for column in columns])), \
            "Not all given columns are found in df"
    columns_order = df.columns
    for column_name in columns:
        if df[column_name].apply(lambda x: isinstance(x, list)).all():
            if strict:
                assert len(set(df[column_name].apply(lambda x: len(x)))) == 1, \
                    f"Lists in df['{column_name}'] are not of equal length"
            unfolded = pd.DataFrame(df[column_name].tolist())
            unfolded.columns = [f'{column_name}_{x}' for x in unfolded.columns] if (len(unfolded.columns) > 1) else [column_name]
            columns_order = [
                *columns_order[:list(columns_order).index(column_name)], 
                *unfolded.columns, 
                *columns_order[list(columns_order).index(column_name)+1:]
            ]
            df = df.drop([column_name], axis=1).join(unfolded)
    return df[columns_order]
```

* Show foldable JSON
```python
import uuid
import json
from IPython.display import display_javascript, display_html, display
from bson import ObjectId

class render_json(object):
    def __init__(self, json_data):
        self.uuid = str(uuid.uuid4())
        self.json_str = self.serialize(json_data)
       
    def serialize(self, data):
        """Convert data to JSON string, handling special types."""
        def custom_serializer(obj):
            if isinstance(obj, ObjectId):
                return str(obj)
            raise TypeError(f"Type {type(obj).__name__} not serializable")
       
        try:
            if isinstance(data, dict) or isinstance(data, list):
                return json.dumps(data, default=custom_serializer)
            else:
                raise ValueError("Input data must be a dictionary or list.")
        except TypeError as e:
            raise ValueError(f"Error serializing data: {e}")

    def _ipython_display_(self):
        display_html(f'<div id="{self.uuid}" style="height: 600px; width:100%;"></div>', raw=True)
        display_javascript(f"""
        require(["https://rawgit.com/caldwell/renderjson/master/renderjson.js"], function() {{
          document.getElementById('{self.uuid}').appendChild(renderjson({self.json_str}))
        }});
        """, raw=True)
```

## Python Environments

* Find where global `site-packages` per user are located:
```bash
python -m site --user-site
```

* Find where `site-packages` are located in activated virtual environment:
```bash
python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())"
```
