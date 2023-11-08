# File formats

The following file formats are supported:

## Tabular data

| type  | suffix                                | example                 |
|-------|---------------------------------------|-------------------------|
| csv   | .csv                                  | [Titanic dataset csv]   |
| Excel | .xls, .xlsx, .xlsm, .xlsb, .odf, .ods | [Titanic dataset excel] |

- The first row contains the names of the columns.
- Only the first sheet of the Excel file is used.

### csv format
All common delimiters, including commas, colons, semicolons and tabs, are supported.
For floating point numbers, please use dots as the decimal separator.
Below is an example of a valid CSV file:

```
name,number,double
"Ford, Henry",1.4,2.8
"Benz, Carl",7.5,15.0
```

### Load additional files (e.g. images)
To load additional files such as images, create a column in the tabular dataset (csv or excel) with the file names. 
Create a zip file of the tabular file along with the additional files.
The zip file should contain only one csv file.
The system will automatically detect that the column contains file names, and if they are present in the zip file, they will be loaded into your data bag.

| type     | suffix | example     |
|----------|--------|-------------|
| zip file | .zip   | [Mnist zip] |

Example structue of a zip file:
```
mnist
├── 10.jpg
├── 20.jpg
├── 24.jpg
└── mnist.csv
```

Content of the mnist.csv:
```
image,digit
10.jpg,3
20.jpg,4
24.jpg,1
```
- Supported image files are: .jpg, .jpeg, .png, .tiff
- Currently only image files are supported, but in the future other files will be supported as well

## Scripts

| type          | suffix | example         |
|---------------|--------|-----------------|
| python script | .py    | [Python script] |

You can also upload python scripts that create a [pandas dataframe].
The script should save the dataframe as a csv without index in the location specified by the `--output` arg.

## Examples for common Machine Learning Problems
We will give some examples of how you can model your machine learning problem using the multimodal format.

### Image Classification
Upload a zip file containing your images and a csv file with the image names and labels. The csv should look like this:
```
image,digit
10.jpg,3
20.jpg,4
24.jpg,1
```

### Image Captioning and Text2Image
```
image,description
tree.jpg,this is a tree in front of a house
ball.jpg,a blue and white ball
flowers.jpg,some flowers on a balcony
```
If you have a dataset with images and corresponding descriptions, you can train an image captioning model, by specifying the description as the output column.
If you choose the image as the output column you can train a text2image model. However, this is not yet supported by our solvers, but will be a future feature.


### Text classification
```
text,sentiment
he is a good boy,positive
he is rude, negative
```

Using a databag with a text column and a category column, you can model text classification tasks such as sentiment analysis.

### Neural Machine Translation
```
english,deutsch
boy,Junge
italian,italienisch
```

If you have a databag with translations from one language to another, you can train a neural machine translation model by simply selecting the desired language as the output column.


[Titanic dataset csv]: assets/datasets/titanic.csv
[Titanic dataset excel]: assets/datasets/titanic.xlsx
[Mnist zip]: assets/datasets/mnist_test.zip
[Python script]: assets/datasets/dataframe_script.py

[pandas dataframe]: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html

[mnist test]: assets/datasets/mnist_test.zip
[classification file format]: file_formats.md#load-additional-files-eg-images
