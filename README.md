# Mental Health Audio Prediction App

A full-stack mental health audio analysis project with:

- React frontend
- Flask backend API
- MongoDB database
- Trained audio classification model
- Browser audio recording support

The application lets a user:

- view a landing page
- upload an audio file
- record audio in the browser
- send audio to the Flask backend for prediction
- store prediction history in MongoDB
- review previous predictions in a history page

## Tech Stack

### Frontend

- React
- Vite
- React Router
- Fetch API

### Backend

- Flask
- Flask-Cors
- PyMongo
- python-dotenv

### Machine Learning / Audio

- scikit-learn
- librosa
- numpy
- joblib
- pydub
- ffmpeg

### Database

- MongoDB

## Project Structure

```text
mental-health-app/
├── README.md
├── .gitignore
├── backend/
│   ├── app.py
│   ├── config.py
│   ├── requirements.txt
│   ├── .env.example
│   ├── model.pkl
│   ├── model_metadata.json
│   ├── train_model.py
│   ├── dataset_RAVDESS_Audio_Song/
│   ├── uploads/
│   │   └── .gitkeep
│   ├── services/
│   │   └── predictor.py
│   └── venv/
└── frontend/
    ├── index.html
    ├── package.json
    ├── vite.config.js
    ├── .env.example
    ├── src/
    │   ├── main.jsx
    │   ├── App.jsx
    │   ├── styles.css
    │   ├── api/
    │   │   └── client.js
    │   ├── components/
    │   │   └── Layout.jsx
    │   └── pages/
    │       ├── Home.jsx
    │       ├── UploadAudio.jsx
    │       ├── Result.jsx
    │       └── History.jsx
```

## Features

- Dark themed professional UI
- Upload audio files in:
  - MP3
  - WAV
  - M4A
  - OGG
  - AAC
  - FLAC
  - WEBM
- Record audio directly in the browser
- Enforce a single active audio source before upload
- Save uploaded files to the backend
- Predict emotion class from extracted audio features
- Store predictions in MongoDB
- View prediction history

## Model Used

The backend uses a trained `RandomForestClassifier` from `scikit-learn`.

### Training Dataset

- RAVDESS Audio Song dataset
- expected dataset path:
  - `backend/dataset_RAVDESS_Audio_Song/`

### Classes Used

The current model maps these classes:

- `Happy`
- `Sad`
- `Angry`
- `Neutral`

### Features Extracted

Audio features are extracted using `librosa`:

- MFCC
- Chroma STFT
- Mel Spectrogram

### Model Files

- `backend/model.pkl`
- `backend/model_metadata.json`

## Libraries Used

### Backend Python Libraries

- `Flask==3.1.0`
- `Flask-Cors==5.0.1`
- `python-dotenv==1.0.1`
- `pymongo==4.10.1`
- `Werkzeug==3.1.3`
- `setuptools==80.9.0`
- `wheel==0.45.1`
- `librosa==0.10.1`
- `numpy==1.26.4`
- `numba==0.60.0`
- `llvmlite==0.43.0`
- `scikit-learn==1.4.2`
- `joblib==1.3.2`
- `pydub==0.25.1`

### Frontend Libraries

- `react`
- `react-dom`
- `react-router-dom`
- `vite`
- `@vitejs/plugin-react`

### System Dependency

- `ffmpeg`

`ffmpeg` is required so the backend can decode browser-recorded `WEBM/Opus` and `OGG` audio through `pydub`.

## Database Used

This project uses MongoDB.

### Database Name

- `mental_health_app`

### Collection Name

- `predictions`

Each stored prediction includes fields such as:

- original filename
- stored filename
- file path
- file size
- prediction
- confidence
- audio type
- uploaded timestamp

## How Database Connection Is Made

MongoDB connection is created in `backend/app.py`.

### Flow

1. Environment variables are loaded in `backend/config.py`
2. `MONGO_URI` and `MONGO_DB_NAME` are read from the environment
3. `MongoClient(config.mongo_uri)` creates the MongoDB client
4. `database = mongo_client[config.mongo_db_name]`
5. `predictions_collection = database["predictions"]`

### Relevant Environment Variables

```env
MONGO_URI=mongodb://localhost:27017/
MONGO_DB_NAME=mental_health_app
```

## Backend API

### `GET /api/health`

Returns:

```json
{
  "status": "ok"
}
```

### `GET /api/history`

Returns all stored predictions from MongoDB in reverse chronological order.

### `POST /api/upload-audio`

Uploads an audio file, generates a prediction, stores the result in MongoDB, and returns:

```json
{
  "message": "Audio uploaded successfully",
  "result": {
    "id": "mongo-document-id",
    "filename": "sample.wav",
    "prediction": "Happy",
    "confidence": 0.92,
    "uploaded_at": "2026-03-25T09:30:00.000000"
  }
}
```

## How Prediction Works

1. User uploads or records audio in the frontend
2. Frontend sends the file to `POST /api/upload-audio`
3. Backend saves the file in `backend/uploads/`
4. Backend loads the trained model from `backend/model.pkl`
5. Audio features are extracted in `backend/services/predictor.py`
6. For `.webm` and `.ogg`, backend converts audio with `pydub + ffmpeg`
7. Model predicts class probabilities
8. Prediction and confidence are stored in MongoDB
9. Response is returned to the frontend

## Setup Instructions

## Prerequisites

- Node.js 18+
- Python 3.10+
- MongoDB running locally or via Atlas
- Homebrew installed on macOS if you need to install `ffmpeg`

## Backend Setup

```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python3 app.py
```

Backend default URL:

```text
http://127.0.0.1:5000
```

### Example `backend/.env`

```env
FLASK_ENV=development
PORT=5000
MONGO_URI=mongodb://localhost:27017/
MONGO_DB_NAME=mental_health_app
UPLOAD_FOLDER=uploads
MAX_CONTENT_LENGTH=16777216
```

## Frontend Setup

```bash
cd frontend
npm install
cp .env.example .env
npm run dev -- --host 127.0.0.1
```

Frontend default URL:

```text
http://127.0.0.1:5173
```

### Example `frontend/.env`

```env
VITE_API_BASE_URL=http://localhost:5000
```

## Model Training

The project includes a training script in `backend/train_model.py`.

### Train the Model

```bash
cd backend
source venv/bin/activate
python3 train_model.py
```

### Training Output

- `backend/model.pkl`
- `backend/model_metadata.json`

## Browser Recording Notes

- uploaded files support:
  - MP3
  - WAV
  - M4A
  - OGG
  - AAC
  - FLAC
  - WEBM
- browser recording output depends on the browser
- most browsers record as `WEBM` or `OGG`
- backend decoding for recorded audio is handled with:
  - `pydub`
  - `ffmpeg`

## Important Files

### Backend

- `backend/app.py`
  - Flask app, routes, MongoDB write logic
- `backend/config.py`
  - environment configuration
- `backend/train_model.py`
  - model training pipeline
- `backend/services/predictor.py`
  - model loading, audio decoding, feature extraction, prediction

### Frontend

- `frontend/src/App.jsx`
  - application routes
- `frontend/src/pages/UploadAudio.jsx`
  - file upload and browser recording flow
- `frontend/src/pages/Result.jsx`
  - prediction display
- `frontend/src/pages/History.jsx`
  - prediction history page
- `frontend/src/api/client.js`
  - frontend API calls

## Common Issues

### Port 5000 Already In Use

Run the backend on another port:

```bash
PORT=5001 python3 app.py
```

### Browser Recording Upload Fails

Make sure:

- Flask backend is running
- MongoDB is running
- `ffmpeg` is installed
- `pydub` is installed in the backend virtual environment

### MongoDB Connection Fails

Make sure MongoDB is listening on:

```text
mongodb://localhost:27017/
```

## Current Status

The current project includes:

- working frontend pages
- dark UI/UX
- upload and browser recording flow
- trained backend prediction model
- MongoDB storage
- history page
- WEBM/OGG recorded-audio decoding support
