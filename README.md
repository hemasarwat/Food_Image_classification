# Transfer Learning for Food Image Classification

Hey there! This project shows how we can use **transfer learning** to classify food images with just a small dataset. We're using EfficientNet models to tell apart pizza, steak, and sushi — think of it as teaching a smart model to recognize new foods by building on what it already knows.

## Dataset

We worked with a tiny but mighty dataset: pizza, steak, and sushi images. It's a subset of the bigger Food101 dataset, perfect for quick experiments. Each class has about 225 pictures for training and 75 for testing. Total? Around 750 images. Small, but enough to see transfer learning in action!

## Model Architecture

We tried two versions of EfficientNet:
- **EfficientNet-B0**: A lightweight model with a 1280-dimensional feature space.
- **EfficientNet-B2**: A bit bigger, with 1408 dimensions for potentially better accuracy.

Both models have the same basic structure: a feature extractor (the "brain" that learns patterns) and a classifier head (the "decision maker" for our 3 food classes). The classifier is simple: a dropout layer for stability, followed by a linear layer that outputs 3 scores (one per class).

## Transfer Learning Approach

Here's the magic: We loaded pretrained EfficientNet models trained on ImageNet (millions of images). Instead of training from scratch, we froze the feature extractor — keeping all that learned knowledge intact. Then, we swapped out the classifier to fit our 3-class problem and only trained that small part. This "feature extraction" method is great for small datasets because it leverages existing knowledge without overfitting.

## Metrics

To see how well our models did, we tracked:
- **Accuracy**: What percentage of images were classified correctly?
- **Loss curves**: How training and test losses changed over epochs (should go down smoothly).
- **Confusion matrix**: A heatmap showing where the model got confused (e.g., did it mix up pizza and steak?).

We also looked at the most confident wrong predictions to understand failure modes.

## Performance Comparison

We compared B0 and B2 side by side:

| Model          | Total Params | Trainable Params | Epochs | Key Notes |
|----------------|--------------|------------------|--------|-----------|
| EfficientNet-B0 | ~4M         | ~4K             | 10     | Fast, good for small tasks |
| EfficientNet-B2 | ~7M         | ~6K             | 5      | More accurate, but needs more memory |

Both models learned super quickly thanks to pretraining — no need for hundreds of epochs! B2 often edges out B0 in accuracy because of its larger feature space, but B0 is simpler and trains faster. For this tiny dataset, B0 was usually enough, but B2 showed how scaling up can help.
