# 🎙️ DebatePal

**DebatePal** is a free, AI-powered debate and communication skills training
platform built with Python and Streamlit. Practice debating, public speaking,
and mock interviews against an AI opponent/coach — completely free using
open AI APIs.

---

## ✨ Features

- 🗣️ **AI Debate Partner** — debate any topic, AI argues the opposite (or same) side, adjustable difficulty (Beginner → Expert)
- 🎤 **Public Speaking Trainer** — submit speech text or audio, get scored on structure, confidence, flow, word choice, engagement
- 💼 **Mock Interview Simulator** — Technical, HR, College Admission, Job interview modes with dynamic AI questions
- 📊 **AI Scoring System** — 1–100 scores across logic, confidence, rebuttal strength, communication, vocabulary, overall
- 🎙️ **Voice Mode** — speech-to-text input and text-to-speech AI replies (push-to-talk)
- 📈 **Performance Dashboard** — progress graphs, strengths/weaknesses, weekly analytics
- 💡 **Topic Generator** — curated + AI-generated debate topics across 8 categories
- 🏆 **Leaderboard & Badges** — local leaderboard, skill levels (Novice → Master Debater)
- 📄 **PDF Reports** — downloadable session summaries with feedback and learning resources
- 🌙 **Dark/Light Theme** — modern UI inspired by ChatGPT/Claude/Perplexity, with smooth animations

---

## 📁 Project Structure

```
DebatePal/
├── app/
│   ├── main.py              # App entry point (run this with streamlit)
│   ├── database.py          # SQLite database layer
│   ├── ai_client.py          # AI provider integrations (free APIs)
│   ├── report_generator.py  # PDF report generation
│   ├── voice_utils.py        # Speech-to-text / text-to-speech
│   ├── styles.py             # Custom CSS (dark/light themes)
│   ├── topics.py             # Static topic bank
│   └── pages_modules/
│       ├── debate_page.py
│       ├── speech_page.py
│       ├── interview_page.py
│       ├── dashboard_page.py
│       ├── topics_page.py
│       └── leaderboard_page.py
├── data/                     # SQLite database file (auto-created)
├── reports/                  # Generated PDF reports (auto-created)
├── requirements.txt
├── .env.example              # Copy to .env and configure
└── README.md
```

---

## 🚀 Setup Instructions

### 1. Install Python dependencies

```bash
cd DebatePal
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Configure your free AI provider

Copy the example env file:

```bash
cp .env.example .env
```

Choose **ONE** free option and edit `.env`:

#### Option A — Ollama (100% free, local, no signup) ⭐ Recommended for beginners
1. Install Ollama from [ollama.com](https://ollama.com)
2. Run: `ollama pull llama3`
3. Set in `.env`:
   ```
   AI_PROVIDER=ollama
   OLLAMA_MODEL=llama3
   ```

#### Option B — OpenRouter (free models, requires free signup)
1. Sign up at [openrouter.ai](https://openrouter.ai) and create an API key
2. Set in `.env`:
   ```
   AI_PROVIDER=openrouter
   OPENROUTER_API_KEY=your_key_here
   OPENROUTER_MODEL=meta-llama/llama-3.1-8b-instruct:free
   ```

#### Option C — Google Gemini Free Tier
1. Get a free key at [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
2. Set in `.env`:
   ```
   AI_PROVIDER=gemini
   GEMINI_API_KEY=your_key_here
   ```

#### Option D — Hugging Face Inference API (free)
1. Get a free token at [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
2. Set in `.env`:
   ```
   AI_PROVIDER=huggingface
   HF_API_KEY=your_token_here
   ```

### 3. Run the app

```bash
streamlit run app/main.py
```

The app opens at `http://localhost:8501`. Sign up for an account and start training!

---

## 🎙️ Voice Mode Notes

- **Speech-to-text** uses the free Google Web Speech API via the `SpeechRecognition`
  library (no API key needed, requires internet).
- **Text-to-speech** uses `gTTS` (free Google TTS).
- Voice features require a working microphone and browser permissions for `st.audio_input`.
- If voice features fail, all text-based features still work fully.

---

## 🗄️ Database Schema (SQLite)

- **users**: id, username, password_hash, created_at, skill_level, total_xp
- **sessions**: id, user_id, session_type, topic, difficulty, stance, created_at
- **messages**: id, session_id, role, content, created_at
- **scores**: id, session_id, user_id, logic, confidence, rebuttal_strength,
  communication, vocabulary, clarity, persuasiveness, professionalism, overall,
  feedback, created_at
- **badges**: id, user_id, badge_name, earned_at

The database file is auto-created at `data/debatepal.db` on first run.

---

## 🌐 Deployment Guide

### Streamlit Community Cloud (free)
1. Push this project to a public/private GitHub repo
2. Go to [share.streamlit.io](https://share.streamlit.io) and connect your repo
3. Set the main file path to `app/main.py`
4. Add your `.env` values as **Secrets** in the Streamlit Cloud dashboard
   (Settings → Secrets), formatted as TOML:
   ```toml
   AI_PROVIDER = "gemini"
   GEMINI_API_KEY = "your_key_here"
   ```
5. Note: Ollama (local models) won't work on Streamlit Cloud — use
   OpenRouter, Gemini, or Hugging Face for cloud deployment.

### Running locally (recommended for beginners)
Just follow the **Setup Instructions** above — no deployment needed to use
DebatePal on your own machine.

---

## 🛠️ Troubleshooting

- **"AI request failed"** — check your `.env` provider settings and API key.
  Try switching `AI_PROVIDER=ollama` for a fully local, free fallback.
- **Voice features not working** — ensure microphone permissions are granted
  in your browser, and that `SpeechRecognition`/`gTTS` installed correctly.
- **Database errors** — delete `data/debatepal.db` to reset (this erases all data).

---

## 📜 License

Free to use and modify for personal, educational, and non-commercial purposes.
