# Food Pack Scanner

A full-stack web app that scans food package labels, extracts ingredients with OCR, and uses AI to flag harmful additives, health risks, and who should avoid the product.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.x-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## Demo flow

1. Upload or capture a photo of a food package ingredients label
2. **Tesseract.js** extracts text via OCR
3. **Google Gemini** analyzes ingredients and returns a structured health report
4. View health score, harmful ingredients, warnings, and long-term risks

## Features

- Camera capture and image upload
- OCR-based ingredient extraction
- AI-powered health analysis with structured output
- Health score (1–10) with risk level
- Responsive, mobile-friendly UI
- REST API backend with static frontend serving

## Tech stack

| Layer | Technologies |
|-------|-------------|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Backend | Node.js, Express.js |
| OCR | Tesseract.js |
| AI | Google Gemini API (`gemini-2.0-flash`) |
| Tooling | dotenv, multer, cors |

## Prerequisites

- [Node.js](https://nodejs.org/) 18 or higher
- [npm](https://www.npmjs.com/)
- A [Google AI Studio](https://aistudio.google.com/) API key (Gemini)

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/Sudarshanbhat101/Food-Packet-Analyzer.git
cd Food-Packet-Analyzer
```

### 2. Install dependencies

```bash
cd backend
npm install
```

### 3. Configure environment variables

```bash
cp .env.example .env
```

Edit `.env`:

```env
GEMINI_API_KEY=your_gemini_api_key_here
PORT=3000
```

### 4. Run the application

```bash
npm start
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

For development with auto-reload:

```bash
npm run dev
```

## API endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/test` | Health check |
| `POST` | `/api/scan` | Upload image (multipart) and run OCR + analysis |
| `POST` | `/analyze` | Analyze base64-encoded image |

## Project structure

```
Food-Packet-Analyzer/
├── backend/
│   ├── server.js          # Express server, OCR, Gemini integration
│   ├── package.json
│   └── uploads/           # Temporary upload storage (gitignored)
├── frontend/
│   ├── index.html         # Main entry point
│   ├── scan.html          # Scanning interface
│   ├── results.html       # Results display
│   ├── style.css
│   └── *.js
├── .env.example
├── .gitignore
├── LICENSE
└── README.md
```

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GEMINI_API_KEY` | Yes | Google Gemini API key |
| `PORT` | No | Server port (default: `3000`) |

## Screenshots

> Add screenshots of the scan and results pages here after deployment.

## Future improvements

- [ ] User accounts and scan history
- [ ] Barcode lookup integration
- [ ] Multi-language label support
- [ ] Deploy to cloud (Render / Railway / Vercel)

## Author

**Sudarshan Bhat** — [GitHub](https://github.com/Sudarshanbhat101)

## License

This project is licensed under the [MIT License](LICENSE).
