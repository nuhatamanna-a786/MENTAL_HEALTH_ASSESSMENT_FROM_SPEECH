# MENTAL_HEALTH_ASSESSMENT_FROM_SPEECH

# Mental Health Assessment from Speech

**Course:** BIG DATA ANALYTICS  

This project is a **full-stack Big Data Analytics platform** for **assessing mental health from speech recordings**. Users can **record or upload audio**, and the system predicts emotions while storing and analyzing historical data to extract trends and insights.

## Key Features

- **Big Data Audio Processing:** Efficient handling of large-scale audio datasets with feature extraction (MFCC, Chroma, Mel Spectrogram).  
- **ML-Powered Emotion Analytics:** Uses a `RandomForestClassifier` trained on the RAVDESS dataset for scalable emotion prediction.  
- **Real-Time & Historical Analysis:** Predictions are stored in MongoDB for trend tracking and historical insights.  
- **Interactive Frontend:** React + Vite interface with recording/uploading, results display, and history dashboards.  
- **Backend Analytics Pipeline:** Flask APIs handle audio preprocessing, feature extraction, model inference, and database storage.



## Tech Stack

- **Frontend:** React, React Router, Vite  
- **Backend:** Flask, Flask-Cors, Python (librosa, scikit-learn, pydub, numpy)  
- **Database:** MongoDB  
- **System Tools:** ffmpeg (required for browser-recorded audio)



## Setup & Usage

### Backend
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python3 app.py
