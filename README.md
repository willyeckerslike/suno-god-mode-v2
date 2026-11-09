# Suno God Mode

Static web app plus Vercel functions that use [OpenRouter](https://openrouter.ai/) to create song concepts, lyrics, style prompts and slider recommendations. This version has **no Udio integration, no Kie.ai integration, and no audio-generation API integration**. Use the generated material in Suno separately.

## Deploy on Vercel

1. Push this folder to a GitHub repository.
2. Import the repository in [Vercel](https://vercel.com).
3. Add `OPENROUTER_API_KEY` in Project → Settings → Environment Variables. This is required.
4. Optionally set `OPENROUTER_MODEL`. If unset, the app defaults to `openai/gpt-4o-mini`. The API also sends fallback models so an unavailable model does not necessarily fail the request.
5. Optionally set `OPENROUTER_SITE_URL` for the OpenRouter `HTTP-Referer` header. It defaults to your Vercel URL.
6. Deploy.

The app uses:

- `/api/models` for the live OpenRouter model catalogue.
- `/api/generate` for song concept generation.
- `/api/generate-stream` for streaming song generation.
- `/api/history` for optional saved generations.

## Generation history

- Without a database, history is stored in browser `localStorage` (up to 100 items).
- With Postgres, link a Postgres database in Vercel Storage and provide a direct `POSTGRES_URL` or `DATABASE_URL` connection string. The `generations` table is created on first use.
- **Privacy:** the history API has no per-user authentication. Anyone who can access a public deployment may be able to read or delete its stored rows. Do not use a public deployment for private history.

## Local development

```bash
npm install
npm i -g vercel
vercel link
vercel env pull .env.local
# Ensure OPENROUTER_API_KEY is set in .env.local
vercel dev
```

Open the local URL shown by Vercel, usually `http://localhost:3000`.

## Push to GitHub

```bash
git init
git add .
git commit -m "Suno God Mode without Udio or Kie integrations"
git branch -M main
git remote add origin https://github.com/YOUR_USER/YOUR_REPO.git
git push -u origin main
```
