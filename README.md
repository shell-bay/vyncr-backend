# VYNCR - AI Forensic Identity Platform

VYNCR is an advanced code forensics platform that detects AI-generated fingerprints and verifies human logic through entropy analysis. It analyzes GitHub repositories to provide trust scores based on pattern entropy and temporal flow analysis.

## Features

- Real-time GitHub repository analysis
- AI vs Human code detection using entropy analysis
- Temporal flow analysis for commit patterns
- Self-healing backend architecture
- Progressive Web App (PWA) support
- Beautiful glassmorphic UI with dark mode
- Live backend health monitoring

## Tech Stack

### Frontend
- Next.js 14
- React 18
- TypeScript
- Tailwind CSS
- Framer Motion
- SWR for data fetching
- Lucide React for icons

### Backend
- FastAPI
- Python 3.9+
- Asyncio for async operations
- httpx for GitHub API integration
- Forensic AI engine for code analysis

## Project Structure

```
vyncr/
├── backend/              # Python FastAPI backend
│   ├── main.py          # Main application entry
│   ├── service.py       # Forensic AI and Self-Healing services
│   ├── requirements.txt # Python dependencies
│   └── .env.example     # Environment template
├── pages/               # Next.js pages
│   ├── _app.tsx        # App wrapper
│   └── index.tsx       # Home page
├── src/                # React components
│   ├── index.tsx       # Main application component
│   └── global.css      # Global styles
├── public/             # Static assets
│   ├── manifest.json   # PWA manifest
│   └── service-worker_.js # Service worker
└── package.json        # Node dependencies
```

## Setup Instructions

### Prerequisites

- Node.js 18+ and npm
- Python 3.9+
- Git

### Frontend Setup

1. Install dependencies:
```bash
npm install
```

2. Configure environment variables:
```bash
cp .env.example .env.local
```

Edit `.env.local`:
```
NEXT_PUBLIC_BACKEND_URL=http://localhost:8000
```

3. Run the development server:
```bash
npm run dev
```

The frontend will be available at `http://localhost:3000`

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install Python dependencies:
```bash
pip install -r requirements.txt
```

4. Run the backend server:
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend API will be available at `http://localhost:8000`

### Running Both Servers

You can run both frontend and backend simultaneously:

**Terminal 1 (Backend):**
```bash
cd backend
source venv/bin/activate  # On Windows: venv\Scripts\activate
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 2 (Frontend):**
```bash
npm run dev
```

## API Endpoints

### Health Check
```
GET /health
```
Returns backend health status and uptime.

Response:
```json
{
  "status": "operational",
  "uptime_seconds": 123.45,
  "node": "Oracle-Cloud-A1"
}
```

### Repository Scan
```
POST /api/v1/scan/project
```

Request body:
```json
{
  "repo_url": "https://github.com/username/repository"
}
```

Response:
```json
{
  "score": 85.5,
  "confidence_level": "High",
  "breakdown": {
    "originality": 85.5,
    "complexity": 85,
    "temporal_flow": "Consistent"
  },
  "repo_details": {
    "name": "repository",
    "owner": "username",
    "scanned_at": "2024-01-15T10:30:00"
  }
}
```

## How It Works

### Forensic AI Engine

The platform uses two main analysis techniques:

1. **Entropy Analysis**: Examines code structure for "human noise" - varied line lengths and unconventional naming patterns that indicate human authorship versus AI-generated code.

2. **Temporal Analysis**: Analyzes commit patterns and timing. AI-generated code often appears in large dumps with minimal time gaps, while human-written code shows more organic commit patterns.

### Self-Healing Architecture

The backend includes a self-healing mechanism that monitors system health and automatically recovers from failures. The frontend displays real-time status updates showing whether the system is "Stable" or "Healing".

## Error Handling

The application includes comprehensive error handling:

- Network failures are caught and displayed to users
- Invalid repository URLs are validated
- GitHub API errors are handled gracefully
- Loading states provide feedback during operations
- Error messages are clear and actionable

## PWA Features

VYNCR is installable as a Progressive Web App:

- Offline-capable UI shell
- Network-first strategy for real-time data
- App icons for home screen installation
- Standalone display mode

## Building for Production

### Frontend
```bash
npm run build
npm start
```

### Backend
```bash
# Using Gunicorn with Uvicorn workers
gunicorn -k uvicorn.workers.UvicornWorker main:app --bind 0.0.0.0:8000
```

## Environment Variables

### Frontend (.env.local)
- `NEXT_PUBLIC_BACKEND_URL`: Backend API URL (default: http://localhost:8000)

### Backend (.env)
- `GITHUB_TOKEN`: Optional GitHub API token for higher rate limits

## Deployment

### Frontend (Vercel)
1. Push to GitHub
2. Connect repository to Vercel
3. Set environment variable: `NEXT_PUBLIC_BACKEND_URL`
4. Deploy

### Backend (Render/Railway/Heroku)
1. Push backend code to GitHub
2. Connect to hosting platform
3. Set Python version to 3.9+
4. Set start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`

## Development Notes

- The frontend uses SWR for efficient data fetching and caching
- Health checks run every 3 seconds for real-time monitoring
- All API calls include proper error boundaries
- TypeScript provides type safety throughout
- Tailwind CSS enables rapid UI development

## Troubleshooting

### Backend won't start
- Ensure Python 3.9+ is installed
- Activate virtual environment
- Install all requirements: `pip install -r requirements.txt`

### Frontend shows "Healing" status
- Check backend is running on port 8000
- Verify `NEXT_PUBLIC_BACKEND_URL` is correct
- Check CORS settings in backend

### GitHub API rate limit
- Add a GitHub personal access token to backend/.env
- Token increases rate limit from 60 to 5000 requests/hour

## License

MIT License

## Contributing

Contributions welcome! Please open an issue or submit a pull request.
