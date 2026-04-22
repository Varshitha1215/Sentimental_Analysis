# 🚀 Local Development Setup Guide

This guide helps you run the entire Sentiment Analysis Platform locally on your machine.

---

## 📋 Prerequisites

- **Node.js 18+** (for frontend & backend)
- **Python 3.11+** (for ML engine)
- **Git** (for version control)
- **npm** or **yarn** (for Node package management)

---

## 🔧 Step-by-Step Setup

### Step 1: Clone Repository
```bash
git clone https://github.com/Varshitha1215/Sentimental_Analysis.git
cd Sentimental_Analysis
```

### Step 2: Setup Python Engine

#### 2.1 Create Virtual Environment
```bash
cd python-engine
python -m venv .venv

# On Windows:
.venv\Scripts\activate

# On macOS/Linux:
source .venv/bin/activate
```

#### 2.2 Install Python Dependencies
```bash
pip install -r requirements.txt
```

#### 2.3 Configure Environment (Optional)
```bash
# Copy example to .env
cp .env.example .env

# Edit .env if needed (defaults work for local development)
```

#### 2.4 Start Python Engine
```bash
python main.py
# Or with Uvicorn directly:
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

✅ **Python Engine should be running on**: `http://localhost:8000`

---

### Step 3: Setup Backend (Node.js)

#### 3.1 Install Dependencies
```bash
cd ../backend
npm install
```

#### 3.2 Configure Environment (Optional)
```bash
# Copy example to .env
cp .env.example .env

# Edit .env if needed:
# - PYTHON_SERVICE_URL should be http://localhost:8000
# - MONGODB_URI is optional (app works without it)
```

#### 3.3 Start Backend Server
```bash
npm start
# Or for development with auto-reload:
npm run dev
```

✅ **Backend should be running on**: `http://localhost:5000`

---

### Step 4: Setup Frontend (React)

#### 4.1 Install Dependencies
```bash
cd ../frontend
npm install
```

#### 4.2 Configure Environment (Optional)
```bash
# Copy example to .env
cp .env.example .env

# Edit .env if needed:
# - REACT_APP_API_URL should be http://localhost:5000/api
```

#### 4.3 Start Frontend Development Server
```bash
npm start
# App will open automatically at http://localhost:3000
```

✅ **Frontend should be running on**: `http://localhost:3000`

---

## ✅ Verification Checklist

Once all 3 services are running, test the following:

### Test 1: Frontend Loads
- [ ] Open http://localhost:3000 in browser
- [ ] See "Advanced Sentiment Analysis" page
- [ ] Tab buttons visible (Text Analysis, File Upload, Trend Analysis)

### Test 2: Basic Analysis
- [ ] Click "📋 Paste Sample"
- [ ] Click "⚡ Analyze (Parallel)"
- [ ] See sentiment chart with results
- [ ] Success message appears

### Test 3: Performance Comparison
- [ ] Keep sample texts loaded
- [ ] Click "📊 Compare Performance"
- [ ] See parallel vs sequential timing comparison

### Test 4: File Upload
- [ ] Go to "📁 File Upload" tab
- [ ] Upload a CSV/TXT file with text data
- [ ] Analyze texts from file

### Test 5: Trend Analysis
- [ ] Go to "📈 Trend Analysis" tab
- [ ] Generate dataset
- [ ] Click "📈 Analyze Trends"
- [ ] See trend visualization and predictions

---

## 🛠️ Troubleshooting

### Frontend can't connect to Backend
**Error**: "❌ Analysis failed. Make sure the backend server is running."
- [ ] Verify backend is running on port 5000
- [ ] Check `frontend/.env` has `REACT_APP_API_URL=http://localhost:5000/api`
- [ ] Check browser console (F12) for actual error message

### Backend can't connect to Python Engine
**Error**: Backend returns error about Python service
- [ ] Verify Python engine is running on port 8000
- [ ] Check `backend/.env` has `PYTHON_SERVICE_URL=http://localhost:8000`
- [ ] Check Python engine logs for errors

### Python Engine won't start
**Error**: "ModuleNotFoundError" or dependency issues
- [ ] Verify you're in the `.venv` virtual environment
- [ ] Run: `pip install -r requirements.txt --upgrade`
- [ ] On Windows with torch issues: Use Python 3.11 (3.12+ has compatibility issues)

### Port already in use
**Error**: "EADDRINUSE: address already in use :::5000"
- [ ] Find what's using the port: `netstat -ano | findstr :5000` (Windows)
- [ ] Kill the process or change PORT in `.env` files

---

## 📚 Available APIs

All endpoints start with `http://localhost:5000/api`:

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/analyze` | Analyze sentiment of texts |
| POST | `/analyze/compare` | Compare parallel vs sequential |
| POST | `/upload` | Upload and process file |
| POST | `/trend-analysis` | Time-series sentiment analysis |
| POST | `/generate-dataset` | Generate test dataset |
| GET | `/models` | Get available models |
| GET | `/health` | Health check |

---

## 🚀 Production Deployment

To deploy to Render.com (or other platforms):

1. **Python Engine** → See `render.yaml` for configuration
2. **Backend** → See `backend/.env.example` for Render setup
3. **Frontend** → See `frontend/.env.example` for Render setup

The `render.yaml` file contains all deployment configuration for 3 services.

---

## 📖 Additional Documentation

- **[ML Models Documentation](ML_MODELS_DOCUMENTATION.md)** - Deep dive into each model
- **[API Documentation](API_DOCUMENTATION.md)** - Detailed endpoint reference
- **[Accuracy Enhancement](ACCURACY_ENHANCEMENT_UPDATE.md)** - Performance optimization tips
- **[Review Flashpoints](REVIEW_FLASHPOINTS.md)** - Key considerations for reviewers

---

## 💡 Tips

- Use `npm run dev` in backend for auto-reload during development
- Python engine supports live reload with `--reload` flag
- Check browser DevTools (F12) for frontend errors
- Python engine logs appear in terminal where you ran `python main.py`
- MongoDB is optional - app gracefully works without it

---

## 📞 Support

For issues:
1. Check the troubleshooting section above
2. Review error messages in browser console (F12)
3. Check service logs in respective terminals
4. Ensure all 3 services are running
5. Verify environment variables in `.env` files

Happy analyzing! 🎉
