# Transfer Learning
In machine learning, often existing models are used for training for a new task instead of training a new model from scratch.
This speeds up the training process and can lead to better results.
This is called Transfer Learning.

With Os4ML you have two options for transfer learning.
Either you choose a pre-defined model or you choose on of your own solutions.

## Pre-defined models

Currently the follwoing models from [HuggingFace] are available for text inputs:

- BERT: a bidrectional transformer developed by Google
- DistilBERT: a smaller and faster BERT variant
- ALBERT: BERT with lower memory usage

The following models from [TorchVision] are available for image inputs:

- ResNet: commonly known architecture for computer vision tasks
- VisionTransformer: transformer architecture for vision tasks
- MobileNet V3: model optimized for mobile, so it uses less memory and computational resources

[HuggingFace]: https://huggingface.co/
[TorchVision]: https://pytorch.org/vision/stable/models.html#classification
