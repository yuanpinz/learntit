# Pandas

## Resources

[Getting Started](https://pandas.pydata.org/docs/getting_started/index.html#getting-started)

[User Guide](https://pandas.pydata.org/docs/user_guide/index.html#user-guide)

## Notes

### Data structures in Pandas

[tutorial](https://pandas.pydata.org/docs/getting_started/intro_tutorials/01_table_oriented.html#min-tut-01-tableoriented), [user guide](https://pandas.pydata.org/docs/user_guide/dsintro.html#dsintro)

#### DataFrame

```python
# Create a DataFrame from Python dictionary
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss. Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)
```

![Dataframe](imgs/01_table_dataframe.svg)

#### Series

```python
# Create a Series from Scratch
s = pd.Series(data, index=index)
```

- each column in a ```DataFrame``` is a ```Series```

- ```Series``` is both ndarray-like and dict-like

  ```python
  # indexing like an ndarray
  s[0]
  s[:3]
  s[s>s.median()]
  s[4,3,1]
  
  # indexing like a dict
  s["a"]
  index_e_exist = "e" in s
  s.get("f",np.nan)
  
  # operation
  s+s
  s*2
  np.exp(s)
  ```

- Convert to array

  ```python
  # Convert to an ExtensionArray
  pandas_array = s.array
  # Convert to ndarray
  ndarray = s.to_numpy()
  ```

### Read and Write

[tutorial](https://pandas.pydata.org/docs/getting_started/intro_tutorials/02_read_write.html#min-tut-02-read-write), [user guide](https://pandas.pydata.org/docs/user_guide/io.html#io)

![](imgs/02_io_readwrite.svg)

### Indexing

[tutorial](https://pandas.pydata.org/docs/getting_started/intro_tutorials/03_subset_data.html#min-tut-03-subset), [user guide](https://pandas.pydata.org/docs/user_guide/indexing.html#indexing)

