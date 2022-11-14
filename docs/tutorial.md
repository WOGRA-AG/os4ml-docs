# Tutorial

TODO fast-lane

## Download Model
After a solution is successfully created, you can download the trained model.

You can load the extracted zip file with the following code to get the LudwigModel:

```python
from ludwig.api import LudwigModel

path_to_extracted_zip = './model.os4ml/'
model = LudwigModel.load(path_to_extracted_zip)
```

Use the `model.predict()` method to make predictions.