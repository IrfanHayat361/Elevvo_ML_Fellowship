# Traffic Sign Recognition System

A deep learning project that automatically identifies traffic signs from images. I built this to see if I could teach a computer to recognize different traffic signs - turns out it's harder than it looks, especially when signs are similar or in different conditions!

## What this project does

- [The challenge](#the-challenge)
- [The data](#the-data)
- [Two different approaches](#two-different-approaches)
- [What I learned](#what-i-learned)
- [Results](#results)
- [How to run it](#how-to-run-it)

## The challenge

Building a traffic sign recognition system sounds simple - just classify images into their corresponding signs - but it's actually pretty tricky. Traffic signs can look very similar to each other, vary in size, color, or orientation, and some appear very rarely in the dataset.

I wanted to see if I could build a system that could accurately identify different traffic signs, especially since this has real-world applications in autonomous vehicles and smart transportation.

## The data

I used the GTSRB (German Traffic Sign Recognition Benchmark) dataset, which has:
- **39,209 training images** and **12,630 test images**
- **43 different traffic sign classes** including speed limits, warnings, and directional signs
- Images of varying sizes that needed to be standardized

The dataset covers everything from speed limit signs (20km/h to 120km/h) to warning signs like "Dangerous curve" and directional signs like "Turn right ahead". Some signs were much more common than others, which created a class imbalance problem.

## Two different approaches

I tried two completely different ways to solve this problem:

### Approach 1: Custom CNN
- **Architecture**: Built from scratch with 3 convolutional blocks
- **Features**: Batch normalization, max pooling, dropout layers
- **Parameters**: About 1.2 million trainable parameters
- **Training**: Trained from scratch on the traffic sign data

### Approach 2: Transfer Learning with MobileNetV2
- **Base model**: Pre-trained MobileNetV2 on ImageNet
- **Approach**: Froze the base model and added custom layers on top
- **Benefits**: Leverages existing knowledge from ImageNet
- **Efficiency**: Faster training and potentially better performance

## What I learned

The most surprising thing was how well the custom CNN performed compared to the transfer learning approach. I expected MobileNetV2 to do better since it was pre-trained on millions of images, but the custom CNN actually achieved much higher accuracy.

Data preprocessing was crucial. The images came in different sizes and formats, so I had to:
- Resize everything to 32×32 pixels
- Convert to consistent RGB format
- Normalize pixel values to 0-1 range
- Apply data augmentation (rotation, zoom, shifting)

Data augmentation made a huge difference. By rotating, zooming, and shifting the training images, I was able to create more diverse examples and make the model more robust to real-world variations.

Some traffic signs were much harder to classify than others. Speed limit signs that looked similar (like 30km/h vs 50km/h) were frequently confused, which makes sense since they're visually very similar.

## Results

Here's how the two approaches compared:

| Model | Test Accuracy | Training Time | Best at | Struggles with |
|-------|---------------|---------------|---------|----------------|
| **Custom CNN** | **98.93%** | Longer | Most sign types | Similar speed limits |
| MobileNetV2 | 28.85% | Faster | General features | Traffic sign specifics |

### Custom CNN Results (98.93% accuracy)
- **Excellent performance** on most traffic sign types
- **Fast convergence** with good validation accuracy
- **Robust** to variations in lighting and orientation
- **Struggles** with visually similar signs (different speed limits)

### MobileNetV2 Results (28.85% accuracy)
- **Poor performance** - much lower than expected
- **Fast training** but didn't learn traffic sign specifics well
- **Transfer learning** didn't help as much as I thought it would
- **May need** more fine-tuning or different approach

The confusion matrices showed that the custom CNN was much better at distinguishing between different sign types, while MobileNetV2 struggled to learn the specific patterns of traffic signs.

## How to run it

You'll need these libraries:
```bash
pip install opendatasets scikit-learn tensorflow opencv-python matplotlib seaborn
```

The notebook downloads the GTSRB dataset automatically, so just run all the cells:

1. **Data loading**: Downloads and extracts the German Traffic Sign dataset
2. **Preprocessing**: Resizes images and normalizes pixel values
3. **Data augmentation**: Creates variations of training images
4. **Custom CNN training**: Builds and trains the custom model
5. **MobileNetV2 training**: Implements transfer learning approach
6. **Evaluation**: Compares both models and shows results

## Key insights

The most important thing I learned is that transfer learning isn't always the answer. While MobileNetV2 worked great on ImageNet, it didn't transfer well to traffic signs. The custom CNN, designed specifically for this problem, performed much better.

Data augmentation was crucial for success. By creating variations of the training images, I was able to make the model more robust to real-world conditions like different lighting, angles, and weather.

The 32×32 pixel size was a good balance between detail and computational efficiency. Larger images might have given better results but would have been much slower to train.

Class imbalance was a real issue. Some signs appeared much more frequently than others, which could bias the model toward more common signs. This is something to consider in real-world applications.

## Challenges faced

- **Memory limitations**: Had to adjust batch sizes and simplify the network
- **Class imbalance**: Some signs appeared much less frequently than others
- **Similar signs**: Speed limit signs that looked alike were hard to distinguish
- **Transfer learning**: MobileNetV2 didn't work as well as expected

## Next steps
