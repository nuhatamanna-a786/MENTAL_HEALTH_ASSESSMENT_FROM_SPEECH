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


```text
/content/dataset
```

### 🎭 Label Extraction

Emotion labels are derived from the filename pattern:

```python
file.split("-")[2]
```

### Emotion Mapping

| Code | Emotion    |
|------|------------|
| 01   | Neutral    |
| 02   | Calm       |
| 03   | Happy      |
| 04   | Sad        |
| 05   | Angry      |
| 06   | Fearful    |
| 07   | Disgust    |
| 08   | Surprised  |

---

## ⚙️ Workflow

1. Upload and extract dataset  
2. Build DataFrame  
3. Visualize class distribution  
4. Audio visualization  
5. Feature extraction  
6. Preprocessing  
7. Train models  
8. Evaluate and compare  

---

## 🔍 Feature Extraction

- MFCC (40 coefficients)  
- Duration: 3 seconds  
- Offset: 0.5 seconds  

### Example

```python
audio, sample_rate = librosa.load(file_path, duration=3, offset=0.5)
mfcc = np.mean(librosa.feature.mfcc(y=audio, sr=sample_rate, n_mfcc=40).T, axis=0)
```

---

## 🔄 Preprocessing

- Features stored in `X`  
- Labels stored in `y`  
- Label encoding using `LabelEncoder`  
- Train-test split:

```python
train_test_split(X, y, test_size=0.2, random_state=42)
```

---

## 🤖 Models Used

### 1. Logistic Regression
```python
LogisticRegression(max_iter=5000)
```

### 2. Random Forest
```python
RandomForestClassifier(n_estimators=200)
```

### 3. XGBoost
```python
XGBClassifier(
    n_estimators=300,
    max_depth=6,
    learning_rate=0.1
)
```

---

## 📊 Evaluation Metrics

- Accuracy  
- Precision  
- Recall  
- F1 Score  
- Mean Squared Error (MSE)  
- Mean Absolute Error (MAE)  
- Root Mean Squared Error (RMSE)  

### Additional Outputs

- Classification report (Logistic Regression)  
- Confusion matrices (all models)  
- Accuracy comparison chart  
- Metrics comparison table  

---

## 📚 Libraries Used

### Core
- numpy  
- pandas  
- matplotlib  
- seaborn  

### Audio Processing
- librosa  
- librosa.display  

### Machine Learning
- scikit-learn  
- xgboost  

### Metrics
- accuracy_score  
- precision_score  
- recall_score  
- f1_score  
- mean_squared_error  
- mean_absolute_error  
- classification_report  
- confusion_matrix  

---

## 📁 Project Structure

```text
project/
├── mhafs2.ipynb
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
7. Train-test split  
8. Train models (LR, RF, XGB)  
9. Evaluate models  
10. Compare results  

---

## 📊 Visual Outputs

- Emotion distribution plot  
- Waveform plot  
- Spectrogram plot  
- Confusion matrices  
- Model comparison charts  

---

## 🌟 Highlights

- Multi-class emotion classification  
- MFCC-based feature extraction  
- Comparison of three ML models  
- End-to-end ML pipeline  
- Strong visualization support  

---

## 🔮 Future Improvements

- Save best-performing model  
- Add cross-validation  
- Hyperparameter tuning  
- Deploy with Flask/FastAPI  
- Build frontend for real-time prediction  
- Extend to deeper mental health analysis  

---

## 📌 Conclusion

This project demonstrates a complete speech emotion recognition workflow using machine learning.

By comparing Logistic Regression, Random Forest, and XGBoost, it provides a strong baseline for emotion classification from speech.
