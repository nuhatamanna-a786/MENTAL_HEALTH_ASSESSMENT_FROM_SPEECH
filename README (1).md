# 🧠 Mental Health Assessment from Speech

A machine learning project for analyzing speech audio and classifying emotional states from voice recordings using multiple supervised learning models.

This project uses audio feature extraction with `librosa`, label encoding, model training, evaluation, and comparison across three machine learning models.

---

## 📌 Overview

The system processes `.wav` speech audio files, extracts MFCC-based features, and predicts the speaker's emotion class.

The notebook includes:

- Dataset extraction from ZIP upload
- Emotion label parsing from RAVDESS-style filenames
- Exploratory visualization
- Feature extraction using MFCC
- Train/test split
- Training and evaluation of three models
- Confusion matrices
- Model comparison plots

---

## 📂 Dataset

The project uses a speech emotion dataset in `.wav` format.

Dataset files are extracted into:

/content/dataset

### 🎭 Label Extraction

Emotion labels are derived from the filename pattern:

file.split("-")[2]

### Emotion Mapping

01 → Neutral  
02 → Calm  
03 → Happy  
04 → Sad  
05 → Angry  
06 → Fearful  
07 → Disgust  
08 → Surprised  

---

## ⚙️ Workflow

1. Upload and Extract Dataset  
2. Build DataFrame  
3. Visualize Class Distribution  
4. Audio Visualization  
5. Feature Extraction  
6. Preprocessing  
7. Train Models  
8. Evaluate Models  

---

## 🔍 Feature Extraction

- MFCC (40 coefficients)  
- Duration: 3 seconds  
- Offset: 0.5 seconds  

---

## 🤖 Models Used

- Logistic Regression  
- Random Forest  
- XGBoost  

---

## 📊 Evaluation Metrics

- Accuracy  
- Precision  
- Recall  
- F1 Score  
- MSE  
- MAE  
- RMSE  

---

## 📁 Project Structure

project/
├── mhafs2.ipynb
├── dataset.zip
└── dataset/
    └── .wav files

---

## 🌟 Highlights

- Multi-class emotion classification  
- MFCC-based feature extraction  
- Comparison of three ML models  
- End-to-end pipeline  

---

## 📌 Conclusion

This project demonstrates a complete speech emotion recognition workflow using machine learning.
