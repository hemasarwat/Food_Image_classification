# Transfer Learning for Food Image Classification

This project shows how we can use **transfer learning** to classify any images dataset, we're using food dataset. We're using EfficientNet models to tell apart pizza, steak, and sushi think of it as teaching a smart model to recognize new foods.

## Dataset

We worked with a tiny but mighty dataset: pizza, steak, and sushi images. It's a subset of the bigger Food101 dataset Each class has about 225 pictures for training and 75 for testing.

## Model Architecture

We tried two versions of EfficientNet:
- **EfficientNet-B0**: A lightweight model with a 1280-dimensional feature space.
- **EfficientNet-B2**: A bit bigger, with 1408 dimensions for better accuracy.

Both models have the same basic structure: a feature extractor and a classifier head --> "decision maker" for our 3 food classes. The classifier is simple: a dropout layer for stability, followed by a linear layer that outputs 3 scores (one per class).

## Transfer Learning Approach

Here's the magic: We loaded pretrained EfficientNet models trained on ImageNet (millions of images). Instead of training from scratch, we froze the feature extractor — keeping all that learned knowledge intact. Then, we swapped out the classifier to fit our 3-class problem and only trained that small part. This "feature extraction" method is great for small datasets because it leverages existing knowledge without overfitting.

## Metrics

To see how well our models did, we tracked:
- **Accuracy**
- **Loss curves**
- **Confusion matrix**

We also looked at the most confident wrong predictions to understand failure modes.

## Performance Comparison

We compared B0 and B2 side by side:

| Model          | Total Params | Trainable Params | Epochs | Key Notes |
|----------------|--------------|------------------|--------|-----------|
| EfficientNet-B0 | ~4M         | ~4K             | 10     | Fast, good for small tasks |
| EfficientNet-B2 | ~7M         | ~6K             | 5      | More accurate, but needs more memory |

Both models learned fast and very accurate that goes to pretraining, B2 often edges out B0 in accuracy because of its larger feature space, but B0 is simpler and trains faster. For this tiny dataset, B0 was usually enough, but B2 showed how scaling up can help.
