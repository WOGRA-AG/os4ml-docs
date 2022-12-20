# Tutorial

## Run Fast-lane

1. Open get started dialog in the bottom left
2. Choose a name for the databag
3. Upload the dataset file
   - Either upload the file directly of pass a valid url to it
   - See [File formats] for more information on the supported file formats.
4. Proceed and wait until the dataset is uploaded and inspected (this may take a while)
5. Select the column you want to predict
6. Choose a name and a solver for the Solution. See [Solvers] for more information on the available solvers.
7. Wait until the solver is done


## Download Model
After a solution is successfully created, you can download the trained model.

You can load the extracted zip file with the following code to get the LudwigModel:

```python
from ludwig.api import LudwigModel

path_to_extracted_zip = './model.os4ml/'
model = LudwigModel.load(path_to_extracted_zip)
```

Use the `model.predict()` method to make predictions.


[Solvers]: solvers.md
[File formats]: file_formats.md