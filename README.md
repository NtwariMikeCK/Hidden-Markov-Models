# Human Activity Recognition Using Hidden Markov Models (HMM)

##  Project Overview

This project implements a **Human Activity Recognition (HAR)** system using **Hidden Markov Models (HMMs)** to classify human motion from smartphone sensor data. The system uses accelerometer and gyroscope signals collected from a mobile device to recognize four activities:

- Standing  
- Walking  
- Jumping  
- Still (no movement)

The goal is to transform raw time-series sensor data into meaningful activity predictions using probabilistic sequence modeling.

---

## Objectives

- Collect real-world smartphone motion sensor data  
- Preprocess and synchronize accelerometer and gyroscope signals  
- Extract meaningful time-domain and frequency-domain features  
- Train a Hidden Markov Model using the Baum–Welch algorithm  
- Decode activity sequences using the Viterbi algorithm  
- Evaluate performance on unseen data  
- Visualize transitions and model behavior  

---

## Project Structure

```text
.
├── data/
│   ├── jumping/                  # Original recordings
│   ├── walking/
│   ├── standing/
│   ├── still/
│   ├── cleaned/              # Preprocessed & synchronized data
│
├── features.csv             # Extracted feature dataset
├── hmm_model.ipynb          # Main implementation notebook
├── README.md                # Project documentation
│
├── plots/
│   ├── transition_matrix.png
│   ├── confusion_matrix.png
│   ├── emission_distributions.png
│   └── prediction_timeline.png
```
## Data Collection

Sensor data was collected using an iPhone 13 with the Sensor Logger app.

Activities recorded:
  - Standing
  - Walking
  - Jumping
  - Still
Dataset details:
  . 52 total recordings (~13 per activity)
  . Duration: 9–12 seconds per recording
  . Sampling rate: 100 Hz (10 ms interval)
  . Sensors used:
    - Accelerometer (x, y, z)
    - Gyroscope (x, y, z)

Each recording was stored in a separate folder containing CSV sensor logs.

---

## Data Preprocessing

The following preprocessing steps were applied:

- Trimmed all recordings to first 9 seconds
- Synchronized accelerometer and gyroscope data using timestamps
- Removed uncalibrated sensor readings
- Merged sensor streams into a unified dataset
- Assigned activity labels to each recording
- Standardized dataset structure for feature extraction

---

## Windowing Strategy

To capture temporal patterns, data was segmented using:

- Window size: 2 seconds (200 samples)
- Overlap: 50%
- Step size: **1 second (100 samples)**

Each window represents one observation for the HMM.

## Feature Engineering

Each window is converted into a feature vector using:

#### Time-domain features:
- Mean, variance, standard deviation
- Root Mean Square (RMS)
- Maximum and minimum values
- Signal Magnitude Area (SMA)
- Correlation between axes
#### Frequency-domain features:
- Dominant frequency (FFT)
- Spectral energy
- FFT peak magnitude

All features are normalized using Z-score standardization.

## Hidden Markov Model

The system uses a Gaussian Hidden Markov Model:

#### Model components:
- Hidden states: Standing, Walking, Jumping, Still
- Observations: Feature vectors
- Transition matrix (A): Learned activity transitions
- Emission probabilities (B): Gaussian distributions
- Initial probabilities (π): Starting state distribution
#### Training algorithm:
- Baum–Welch (Expectation-Maximization)
#### Decoding:
- Viterbi algorithm for most likely state sequence

---

## Model Evaluation

The model was evaluated on unseen test recordings (entire sessions excluded from training).

#### Metrics used:
- Accuracy
- Sensitivity (Recall)
- Specificity
- Confusion Matrix
#### Visualizations:
- Transition probability heatmap
- Emission feature distributions
- Prediction timeline
- Confusion matrix

---

## Results Summary

- Strong performance on dynamic activities (walking, jumping)
- Slight confusion between low-motion states (standing vs still)
- Transition matrix reflects realistic human behavior patterns
- Frequency-domain features significantly improved classification

---

## Key Insights

- Human motion is highly sequential and benefits from probabilistic modeling
- HMM effectively captures transitions between activities
- Frequency-domain features are critical for distinguishing periodic movements
- Proper windowing improves model stability and performance

---

## Future Improvements
- Increase dataset size and diversity
- Add additional sensors (e.g., magnetometer)
- Experiment with LSTM / deep learning models
- Optimize window size dynamically
- Deploy real-time activity recognition system

---

## Author

Name: **Ntwari Mike Chris Kevin**

---

##License

- This project is for educational purposes.
