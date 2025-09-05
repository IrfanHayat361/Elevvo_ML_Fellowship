# Music Genre Classification System

A machine learning project that automatically categorizes music into different genres based on audio features. I built this to see if I could teach a computer to distinguish between musical styles - turns out it's harder than it sounds!

## What this project does

- [The challenge](#the-challenge)
- [The data](#the-data)
- [Two different approaches](#two-different-approaches)
- [What I learned](#what-i-learned)
- [Results](#results)
- [How to run it](#how-to-run-it)

## The challenge

Classifying music genres sounds simple - just figure out which genre a track belongs to - but it's actually pretty tricky. The biggest problem is that genres aren't always well-defined. Two songs in the same genre can sound completely different, while tracks from separate genres can sometimes share a lot of common elements.

I wanted to see if I could build a system that could actually distinguish between different musical styles using just the audio data.

## The data

I used the GTZAN dataset, which has:
- 10 different genres: blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock
- 100 songs per genre (1,000 total)
- 30-second audio clips in WAV format

The dataset was a good size - large enough to cover variety but not so big that it became unmanageable. I noticed that certain genres like classical were much easier to distinguish, while others like rock and metal had significant overlap.

## Two different approaches

I tried two completely different ways to solve this problem:

### Approach 1: Traditional Machine Learning
- **Feature extraction**: Used librosa to extract audio features like MFCCs, spectral centroid, rolloff, bandwidth, tempo, etc.
- **Model**: Random Forest classifier trained on these hand-crafted features
- **Features used**: 42 different audio characteristics per song

### Approach 2: Deep Learning
- **Spectrograms**: Converted audio to visual spectrograms (like turning sound into images)
- **Model**: Convolutional Neural Network (CNN) that learns directly from the spectrogram images
- **Input**: 128x128 pixel images representing the audio

## What I learned

The most surprising thing was that the CNN approach didn't perform as well as I expected. I thought the deep learning method would be superior, but the Random Forest actually did better.

Feature extraction was more important than I realized. I had to experiment with different audio features to find the right combination. MFCCs (Mel-frequency cepstral coefficients) turned out to be really useful - they capture the timbre and texture of music in a way that's hard to describe but works well for classification.

Some genres were consistently harder to classify. Rock and metal got confused with each other a lot, which makes sense since they share similar characteristics. Classical music was surprisingly easy to identify, probably because it has such distinct acoustic properties.

The spectrogram approach was interesting but had limitations. While it's cool to think of audio as images, the CNN struggled to learn meaningful patterns from the visual representation. Maybe the spectrograms weren't detailed enough, or the dataset was too small for the CNN to really learn.

## Results

Here's how the two approaches compared:

| Model | Accuracy | Best at | Struggles with |
|-------|----------|---------|----------------|
| **Random Forest** | **69%** | Classical, Jazz, Metal | Rock vs Metal confusion |
| CNN | 51% | Metal, Pop | Most genres |

### Random Forest Results (69% accuracy)
- **Classical**: 83% precision, 100% recall - really good at identifying classical music
- **Jazz**: 88% precision, 70% recall - solid performance
- **Metal**: 80% precision, 80% recall - consistent results
- **Blues**: 50% precision, 100% recall - catches all blues but has false positives

### CNN Results (51% accuracy)
- **Metal**: 70% precision, 70% recall - best performance
- **Pop**: 70% precision, 70% recall - also good
- **Classical**: 53% precision, 80% recall - decent but not as good as Random Forest

The confusion matrices showed that rock and metal were the most commonly confused genres, which makes sense given their similarities.

## How to run it

You'll need these libraries:
```bash
pip install librosa scikit-learn matplotlib seaborn numpy pandas tensorflow
```

The notebook downloads the GTZAN dataset from Kaggle, so you'll need to:
1. Upload your Kaggle API key (kaggle.json)
2. Run all the cells to see both approaches

The notebook covers:
- **Data loading**: Downloads and explores the GTZAN dataset
- **Feature extraction**: Extracts 42 audio features using librosa
- **Random Forest training**: Trains and evaluates the traditional ML approach
- **Spectrogram generation**: Creates visual representations of audio
- **CNN training**: Trains and evaluates the deep learning approach
- **Comparison**: Shows results from both methods

## Key insights

The most important thing I learned is that genre classification isn't just about labeling tracks - it's about understanding what makes genres unique while recognizing that the boundaries are often fuzzy.

Traditional machine learning with carefully chosen features can actually outperform deep learning in some cases, especially with smaller datasets. The Random Forest was able to learn meaningful patterns from the hand-crafted features, while the CNN struggled to extract useful information from the spectrograms.

Some genres are inherently easier to classify than others. Classical music has such distinct acoustic properties that it's almost always identified correctly, while rock and metal share enough characteristics that they're frequently confused.

The feature engineering process was crucial. I had to experiment with different combinations of audio features to find what worked best. MFCCs, spectral features, and tempo information turned out to be the most useful.

