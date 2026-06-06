# Food Pack Scanner

> Collaborative project — scan food packaging, extract ingredients via OCR, analyze health risks with AI, and get a structured safety report.

**Live demo:** [food-packet-analyzer-app.vercel.app](https://food-packet-analyzer-app.vercel.app)  
**Partner repo:** [shripoornasunilpetkar/Food-Packet-Analyzer-App](https://github.com/shripoornasunilpetkar/Food-Packet-Analyzer-App)

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.x-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## Contributors

| Name | GitHub |
|------|--------|
| Sudarshan Bhat | [@Sudarshanbhat101](https://github.com/Sudarshanbhat101) |
| Shripoorna Sunil Petkar | [@shripoornasunilpetkar](https://github.com/shripoornasunilpetkar) |

## What it does

1. User uploads or captures a food package label image (`scan.html`)
2. Frontend sends base64 image to `POST /analyze`
3. Backend runs **Tesseract.js** OCR on the image
4. Extracted text is sent to **Google Gemini** (`gemini-2.0-flash`)
5. `parseAnalysis()` converts Gemini's text into a structured JSON object
6. Result is stored in `localStorage` and shown on `results.html` with **Chart.js**

## Tech stack

| Layer | Technology | Role |
|-------|------------|------|
| Frontend | HTML, CSS, Vanilla JS | Scan UI, camera/upload, results dashboard |
| Frontend | Chart.js (CDN) | Health score doughnut chart |
| Backend | Node.js + Express | API server, serves `frontend/` statically |
| OCR | Tesseract.js | Ingredient text extraction from images |
| AI | Google Gemini API | Ingredient health analysis |
| Upload | multer | Alternate `POST /api/scan` multipart route |

## Project structure

```
Food-Packet-Analyzer/
├── backend/
│   ├── server.js           # Express app, OCR, Gemini, parseAnalysis()
│   ├── eng.traineddata     # Tesseract English language data
│   └── package.json
├── frontend/
│   ├── index.html          # Landing page
│   ├── scan.html + scan.js # Camera / upload → POST /analyze
│   ├── results.html + results.js  # Reads localStorage, renders report
│   └── style.css
├── script.js               # UI effects (legacy helper)
├── .env.example
└── package.json
```

## API reference

### `POST /analyze` (main flow used by frontend)

**Request**
```json
{
  "image": "data:image/jpeg;base64,..."
}
```

**Success response** — built by `parseAnalysis()` in `backend/server.js`:
```json
{
  "healthScore": 6,
  "healthRating": "Good",
  "riskLevel": "Moderate",
  "harmfulIngredients": [
    { "name": "Sodium Benzoate", "severity": "Moderate", "description": "..." }
  ],
  "warnings": [
    { "group": "People with asthma", "description": "..." }
  ],
  "longTermRisks": [
    { "name": "Metabolic issues", "severity": "Low", "description": "..." }
  ],
  "totalHarmful": 2,
  "criticalIngredients": 0,
  "highRiskGroups": 1,
  "criticalRisks": 0
}
```

**Severity values:** `Critical` | `Moderate` | `Low`  
**Health rating:** `Excellent` (8+) | `Good` (6+) | `Fair` (4+) | `Poor` (<4)

### Other endpoints

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/test` | Health check |
| `POST` | `/api/scan` | Multipart image upload (returns raw `text` + `analysis` string) |

## Setup

```bash
git clone https://github.com/Sudarshanbhat101/Food-Packet-Analyzer.git
cd Food-Packet-Analyzer
cd backend && npm install
```

Create `backend/.env`:
```env
GEMINI_API_KEY=your_gemini_api_key_here
PORT=3000
```

Get a Gemini key from [Google AI Studio](https://aistudio.google.com/).

```bash
npm start
# Open http://localhost:3000
```

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GEMINI_API_KEY` | Yes | Google Gemini API key (used by `server.js`) |
| `PORT` | No | Server port (default `3000`) |

> Note: The code uses `GEMINI_API_KEY`, not Google Cloud Vision.

## License

MIT — see [LICENSE](LICENSE).
