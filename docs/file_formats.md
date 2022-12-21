# File formats

The following file formats are supported:

## Tabular data

| type  | suffix                                | example                 |
|-------|---------------------------------------|-------------------------|
| csv   | .csv                                  | [Titanic dataset csv]   |
| Excel | .xls, .xlsx, .xlsm, .xlsb, .odf, .ods | [Titanic dataset excel] |

- The first row contains the names of the columns.
- Only the first sheet of the Excel file is used.


## Images for classification

| type     | suffix | example     |
|----------|--------|-------------|
| zip file | .zip   | [Mnist zip] |

- The unpacked zip file should contain one folder (mnist_test in the example below)
- This folder should contain one folder for each label (0, 1)
- The label folders should contain the corresponding images
- Supported image files are: .jpg, .jpeg, .png, .tiff

```
mnist_test
├── 0
│   ├── 114.jpg
...
├── 1
│   ├── 102.jpg
│   ├── 104.jpg
...
```

## Scripts

| type          | suffix | example         |
|---------------|--------|-----------------|
| python script | .py    | [Python script] |

You can also upload python scripts that create a [pandas dataframe].
The script should save the dataframe as a csv without index in the location specified by the `--output` arg.


[Titanic dataset csv]: assets/datasets/titanic.csv
[Titanic dataset excel]: assets/datasets/titanic.xlsx
[Mnist zip]: assets/datasets/mnist_test.zip
[Python script]: assets/datasets/dataframe_script.py

[pandas dataframe]: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html
