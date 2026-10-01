# Rishu Raj — Portfolio + Projects

My portfolio and all six projects on one small Node.js server. Visitors need **no sign-in** anywhere.

| Path | What it is | Needs the AI key? |
|---|---|---|
| `/` | Portfolio (talking intro, projects, skills, contact) | No |
| `/kheti-mitra/` | Kheti Mitra — AI crop doctor for farmers (Hindi / English) | Yes |
| `/saferoute/` | SafeRoute — route guardian landing page | No |
| `/multi-agent/` | Multi-Agent Research Assistant | Yes |
| `/api-hub/` | API Hub — 99 free public APIs (Firebase login) | No |
| `/ultron/` | Ultron — web voice assistant | No |
| `/resume-corrector/` | Resume Corrector | Yes |

The browser never sees the API key. AI pages call `/api/ai` on this server, and the server calls Google Gemini (free tier) or Claude.

## Deploy on Render (free)

1. Free Gemini key: https://aistudio.google.com/apikey → **Create API key**.
2. Upload everything in this folder to a new GitHub repository (for example `rishu-portfolio`). `server.js` must be at the top level of the repo. Do **not** upload any `.env` file.
3. https://render.com → sign in with GitHub → **New → Web Service** → connect the repo.
4. Settings: Runtime **Node**, Build command `npm install`, Start command `node server.js`, Instance **Free**.
5. **Environment Variables** → `GEMINI_API_KEY` = your key → **Deploy Web Service**.
6. Open `https://<your-service>.onrender.com/` — that is your portfolio, with every project working.
7. For the API Hub login: Firebase Console → Authentication → Settings → **Authorized domains** → add `<your-service>.onrender.com`.

## Run on your computer

```bash
cp .env.example .env      # then put your key after GEMINI_API_KEY=
npm start                 # open http://localhost:3000
```

## Settings

| Variable | Default | Meaning |
|---|---|---|
| `GEMINI_API_KEY` | — | Google AI Studio key (use this **or** `ANTHROPIC_API_KEY`) |
| `GEMINI_MODEL` | `gemini-flash-lite-latest` | Gemini model name |
| `ANTHROPIC_API_KEY` | — | Use Claude instead of Gemini (paid) |
| `RATE_LIMIT` | `40` | Max AI requests per visitor every 10 minutes |
| `MAX_OUTPUT_TOKENS` | `8192` | Longest AI answer |

## Good to know

- Render's free plan sleeps after 15 minutes without visitors; the first visit after that takes 30–60 seconds.
- Gemini's free tier has a daily limit. Turn on billing in Google AI Studio if many people use the apps.
