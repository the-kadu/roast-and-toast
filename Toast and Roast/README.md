# Roast & Toast Machine

Daily Content Creator: applies your comedy guide and a chosen persona to a subject and drafts a ROAST post and a TOAST post.

## Files
- `index.html`: the whole front end (no build step, no dependencies)
- `api/generate.js`: Vercel serverless function; the only code that touches the API key
- `PRD.md`: product requirements

## Deploy (GitHub + Vercel)
1. Create a GitHub repo and push these files (`.env` files are git-ignored). Keep the `api/` folder.
2. In Vercel: Add New Project, import the repo, framework preset "Other", deploy.
3. Vercel > Settings > Environment Variables, add: `PROVIDER`, `API_KEY`, `ACCESS_CODE` (and optionally `MODEL`, `DAILY_LIMIT`, `PER_IP_LIMIT`). See `.env.example`.
4. Redeploy so the variables take effect.
5. Open the URL, type your access code, pick a persona, and generate.

## Notes
- Rate limits are held in server memory, so they are best-effort and reset on cold starts. The access code and a monthly spend cap in your provider dashboard are the real guardrails.
- The archive lives in browser localStorage: device-only, lost if site data is cleared.
- Check that the default model names in `api/generate.js` are current for your provider, or set `MODEL`.
- Add your own personas by adding lines that start with `PERSONA:` in the guide.
