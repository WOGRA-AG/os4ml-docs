# Examples

## Image Classification

1. Prepare a dataset according to the [classification file format]. Make sure that all images have the same format and size.
2. Create a databag with this dataset. This should produce a databag with two columns one for the image and the other for the label.
3. Create a solution and choose the label column as the output column.

[mnist test]: assets/datasets/mnist_test.zip
[classification file format]: /os4ml/file_formats/#images-for-classification

## Example Databags for common Machine Learning Problems

We will give some examples of how you can model your machine learning problem using the multimodal format.

### Image Captioning and Text2Image
| column      | datatype |
|-------------|----------|
| image       | image    |
| description | text     |

If you have a dataset with images and corresponding descriptions, you can train an image captioning model, by specifying the description as the output column.
If you choose the image as the output column you can train a text2image model. However, this is not yet supported by our solvers, but will be a future feature.


### Text classification
| column | datatype |
|--------|----------|
| text   | text     |
| label  | categoy  |

Using a databag with a text column and a category column, you can model text classification tasks such as sentiment analysis.


### Neural Machine Translation
| column    | datatype |
|-----------|----------|
| languageA | text     |
| languageB | text     |

If you have a databag with translations from one language to another, you can train a neural machine translation model by simply selecting the desired language as the output column.
