# 🎬 VidSnap — Multi-Platform Video Downloader

Download videos from **YouTube**, **TikTok**, and **Instagram** with quality selection, batch downloading, and live progress tracking.

## Architecture

```
Frontend (Vercel) ──► Backend (Railway/Render/Local)
HTML + CSS + JS         FastAPI + yt-dlp + ffmpeg
```

---

## 🚀 Quick Start (Local)

### 1. Backend

```bash
cd backend

# Install Python deps
pip install -r requirements.txt

# Install ffmpeg (Windows - using chocolatey)
choco install ffmpeg

# OR download from https://ffmpeg.org/download.html and add to PATH

# Run the server
uvicorn main:app --reload --port 8000
```

### 2. Frontend

Open `frontend/index.html` directly in your browser — no build step needed.

Make sure the **API** bar at the top shows `http://localhost:8000` with a green dot.

---

## ☁️ Deploy to Production

### Backend → Railway

1. Push this repo to GitHub
2. Go to [railway.app](https://railway.app) → New Project → Deploy from GitHub
3. Select the `backend/` folder
4. Railway auto-detects the `Dockerfile` and deploys it
5. Copy your Railway URL (e.g. `https://vidsnap-backend.up.railway.app`)

### Frontend → Vercel

1. Connect your GitHub repo to [vercel.com](https://vercel.com)
2. Set **Root Directory** to `frontend/`
3. Deploy
4. In the live site, update the **API** bar to your Railway backend URL

---

## 📡 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET`  | `/` | Health check |
| `POST` | `/api/info` | Get video metadata + formats |
| `POST` | `/api/start` | Start a download, returns `task_id` |
| `GET`  | `/api/progress/{task_id}` | SSE stream with live progress |
| `GET`  | `/api/file/{task_id}` | Download finished file |

### POST /api/info
```json
{ "urls": ["https://youtube.com/watch?v=...", "https://tiktok.com/..."] }
```

### POST /api/start
```json
{ "url": "https://...", "format_id": "137+140", "title": "My Video" }
```

---

## Supported Platforms

| Platform | Videos | Audio-only |
|----------|--------|-----------|
| YouTube  | ✅ Up to 1080p+ | ✅ |
| TikTok   | ✅ | — |
| Instagram Reels/Posts | ✅ | — |
| Twitter/X | ✅ | — |
| Facebook  | ✅ | — |
| + 1000 more sites (yt-dlp) | ✅ | ✅ |

---

## Tech Stack

- **Backend**: Python 3.12, FastAPI, yt-dlp, ffmpeg
- **Frontend**: Vanilla HTML/CSS/JS (no framework, no build step)
- **Hosting**: Vercel (frontend) + Railway/Render (backend)
