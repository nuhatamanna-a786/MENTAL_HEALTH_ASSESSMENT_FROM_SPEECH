# 🧠 Mental Health Assessment from Speech

A machine learning project for analyzing speech audio and classifying emotional states from voice recordings using multiple supervised learning models.

This project uses audio feature extraction with `librosa`, label encoding, model training, evaluation, and comparison across **four machine learning models**.

---

## 📌 Overview

The system processes `.wav` speech audio files, extracts MFCC-based features, and predicts the speaker's emotion class.

The notebook includes:

* Dataset extraction from ZIP upload
* Emotion label parsing from RAVDESS-style filenames
* Exploratory visualization
* Feature extraction using MFCC
* Train/test split
* Training and evaluation of four models
* Confusion matrices
* Model comparison plots

---

## 📂 Dataset

The project uses a speech emotion dataset in `.wav` format.

Dataset files are extracted into:

```text
/content/dataset
```

### 🎭 Label Extraction

Emotion labels are derived from the filename pattern:

```python
file.split("-")[2]
```

### Emotion Mapping (Used in Project)

| Code | Emotion |
| ---- | ------- |
| 01   | Neutral |
| 02   | Calm    |
| 03   | Happy   |
| 04   | Sad     |
| 05   | Angry   |
| 06   | Fearful |

---

## ⚙️ Workflow

1. Upload and extract dataset
2. Build DataFrame
3. Visualize class distribution
4. Audio visualization (waveform, spectrogram, MFCC)
5. Feature extraction
6. Preprocessing
7. Train models
8. Evaluate and compare

---

## 🔍 Feature Extraction

* MFCC (40 coefficients)
* Duration: 3 seconds
* Offset: 0.5 seconds

```python
audio, sr = librosa.load(file_path, duration=3, offset=0.5)
mfcc = np.mean(librosa.feature.mfcc(y=audio, sr=sr, n_mfcc=40).T, axis=0)
```

---

## 🔄 Preprocessing

* Silence trimming
* Normalization
* Label encoding using `LabelEncoder`
* Train-test split (80/20)
* Feature scaling using `StandardScaler` (for LR & SVM)

---

## 🤖 Models Used

### 1. Logistic Regression ⭐ (Best Model)

```python
LogisticRegression(max_iter=5000)
```

### 2. Random Forest

```python
RandomForestClassifier(n_estimators=200)
```

### 3. Support Vector Machine (SVM)

```python
SVC(kernel='rbf', C=10, gamma='scale')
```

### 4. XGBoost

```python
XGBClassifier(
    n_estimators=300,
    max_depth=6,
    learning_rate=0.1,
    eval_metric='mlogloss'
)
```

---

## 📊 Evaluation Metrics

* Accuracy
* Precision
* Recall
* F1 Score
* Mean Squared Error (MSE)
* Mean Absolute Error (MAE)
* Root Mean Squared Error (RMSE)

### Additional Outputs

* Classification reports (all models)
* Confusion matrices (all models)
* Accuracy comparison chart
* Metrics comparison plots

---

## 📈 Results Summary

| Model               | Accuracy   | F1 Score   | RMSE     |
| ------------------- | ---------- | ---------- | -------- |
| Logistic Regression | **91.67%** | **0.9178** | **0.50** |
| SVM                 | 91.67%     | 0.9164     | 0.78     |
| Random Forest       | 80.56%     | 0.7964     | 0.78     |
| XGBoost             | 72.22%     | 0.7061     | 1.37     |

📌 These results are consistent with the experimental findings in your report 

---

## 🏆 Best Model

**Logistic Regression** achieved the best overall performance:

* Highest accuracy (~91.67%)
* Best F1-score (balanced classification)
* Lowest error metrics (MSE, MAE, RMSE)
* Minimal misclassification across emotion classes

As noted in your report, the strong performance indicates that **MFCC features are linearly separable**, making simpler models highly effective 

---

## 📊 Visual Outputs

* Emotion distribution plot
* Waveform visualization
* Spectrogram
* MFCC heatmap
* Confusion matrices (all models)
* Model comparison graphs

---

## 📚 Libraries Used

### Core

* numpy
* pandas
* matplotlib
* seaborn

### Audio Processing

* librosa
* librosa.display

### Machine Learning

* scikit-learn
* xgboost

---

## 📁 Project Structure

```text
project/
├── notebook.ipynb
├── dataset.zip
└── dataset/
    └── .wav files
```

---

## 🔁 Model Training Flow

1. Upload dataset ZIP
2. Extract dataset
3. Traverse `.wav` files
4. Parse labels
5. Extract MFCC features
6. Encode labels
7. Scale features (LR, SVM)
8. Train models (LR, RF, SVM, XGB)
9. Evaluate models
10. Compare results

---

## 🌟 Highlights

* Multi-class emotion classification (6 emotions)
* MFCC-based feature extraction
* Comparison of **four ML models**
* Identification of best-performing model
* End-to-end ML pipeline
* Strong visualization support

---

## 🔮 Future Improvements

* Hyperparameter tuning
* Cross-validation
* Deep learning models (CNN, LSTM)
* Real-time speech prediction system
* Deployment (Flask / FastAPI)
* Integration with mental health monitoring systems

---

## 📌 Conclusion

This project demonstrates a complete speech emotion recognition workflow using machine learning.

By comparing Logistic Regression, SVM, Random Forest, and XGBoost, it was observed that **Logistic Regression performs best**, achieving high accuracy and balanced classification.

The system highlights the potential of speech-based analysis as a **supportive tool for early mental health assessment**, offering a scalable and data-driven approach.

---
