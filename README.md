# English Accent Detection using Machine Learning & Deep Learning

## Project Overview
[cite_start]This project aims to construct a model capable of identifying and categorizing various English accents using short speech samples[cite: 11]. [cite_start]By analyzing acoustic characteristics that distinguish accents, we seek to improve Automatic Speech Recognition (ASR) inclusivity for speakers of diverse linguistic backgrounds[cite: 10, 15].

[cite_start]The project implements a **Progressive Performance Strategy**, moving from statistical baselines to advanced Transfer Learning to handle data scarcity and complexity[cite: 34].

---

## Dataset
[cite_start]**Source:** [The Speech Accent Archive (Kaggle)](https://www.kaggle.com/datasets/rtatman/speech-accent-archive) [cite: 28]
* [cite_start]**Content:** Over 2,000 speech samples from 177 countries[cite: 28, 29].
* [cite_start]**Structure:** Each speaker reads the *same* scripted paragraph to control for word choice and focus purely on phonetics[cite: 21, 30].
* [cite_start]**Modifications:** We expanded the dataset by adding custom field recordings of Italian/Sicilian speakers to increase diversity[cite: 13, 36].

---

## Methodology
[cite_start]We implemented a three-stage pipeline to rigorously evaluate performance[cite: 34].

### Step 1: Baseline Modeling (MFCC + SVM)
* [cite_start]**Goal:** Establish a baseline performance metric using fundamental acoustic features[cite: 39].
* **Process:**
    1.  [cite_start]Audio cleaning and normalization[cite: 37].
    2.  [cite_start]Extraction of **Mel-Frequency Cepstral Coefficients (MFCCs)** to represent speech envelopes[cite: 38].
    3.  [cite_start]Training a **Support Vector Machine (SVM)** classifier[cite: 40].

### Step 2: Deep Learning (Spectrograms + CNN)
* [cite_start]**Goal:** Capture complex time-frequency variations associated with specific accents[cite: 43].
* **Process:**
    1.  [cite_start]Converted audio clips into **Log-Mel Spectrograms** (visual representations of sound)[cite: 42].
    2.  [cite_start]Trained a custom **Convolutional Neural Network (CNN)** to identify visual patterns in the spectrograms[cite: 43].
    3.  [cite_start]Applied data augmentation (noise injection, pitch shifting) to improve robustness[cite: 44].

### Step 3: Transfer Learning (YAMNet Embeddings)
* [cite_start]**Goal:** Leverage pre-trained models to improve accuracy on limited data[cite: 48].
* **Process:**
    1.  Utilized **YAMNet** (trained on AudioSet) as a feature extractor.
    2.  [cite_start]Extracted high-level **Embeddings** (1024-dimensional vectors) representing timbre and pitch[cite: 49].
    3.  [cite_start]Trained a lightweight neural network classifier on these embeddings[cite: 49].

---

## Results & Interpretation

| Model | Technique | Accuracy |
| :--- | :--- | :--- |
| **Baseline** | SVM + MFCCs | **59.70%** |
| **Deep Learning** | CNN + Spectrograms | **85.82%** |
| **Transfer Learning** | YAMNet Embeddings | **64.68%** |

### Analysis of Results

**1. The "Too Good" CNN Score (85.82%)**
While the CNN achieved the highest accuracy, detailed error analysis suggests this is a case of **Overfitting**.
* **Reason:** Deep Learning models require massive datasets to generalize well. [cite_start]With a smaller dataset like the Speech Accent Archive, the CNN likely "memorized" non-accent features (such as background noise or microphone quality) specific to certain speakers[cite: 45].
* **Implication:** This model is likely "brittle"—it performs well on the test set but would struggle with brand new, real-world audio.

**2. The Real Winner: Transfer Learning (64.68%)**
The Transfer Learning model represents the most scientifically valid improvement.
* **Robustness:** Because the YAMNet feature extractor was pre-trained on millions of external audio files, it cannot "cheat" by memorizing our specific dataset's noise.
* **Improvement:** It achieved a **~5% improvement** over the baseline. In machine learning, a 5% gain over a strong baseline is statistically significant and indicates that the model is truly learning to distinguish accent features rather than just memorizing data.

**3. The Baseline Floor (59.70%)**
[cite_start]The SVM proved that accents have distinguishable mathematical features (MFCCs) but lack the complexity to handle the subtle nuances between similar accents (e.g., Spanish vs. Italian)[cite: 58].

---

## Usage
To reproduce these results using the provided notebook:
1.  **Download Data:** The script uses `kagglehub` to automatically fetch the dataset.
2.  **Run Pipeline:** Execute the cells sequentially to preprocess data, extract features, and train all three models.
3.  [cite_start]**Visualize:** Use the provided visualization functions to generate Confusion Matrices and Loss Curves for detailed error analysis[cite: 50].

---

## Team
[cite_start]**Team 3** - DS-620 ML & DL Fall 2025 [cite: 3, 4]
* Jeff Anderson
* Jeff Mobley
* Megha Narendra Simha
* [cite_start]Sai Mani Ritish [cite: 2]
