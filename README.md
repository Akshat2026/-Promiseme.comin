# promiseme.com — Source Code

Webtoon-style manga platform: high-resolution comic uploads, vertical reader, Reddit-style community, live chat, Voice Studio, aur owner social tools. **Koi bhi user verification nahi chahiye** (no email, OTP, account, ID).

## Kya-kya hai

- `/` — home (hero, trending, top 10, voices, community highlights)
- `/comics` — library (search, genre filter, sorting)
- `/rankings` — weekly chart
- `/comics/[id]` — series page + episodes
- `/read/[episodeId]` — vertical full-quality reader
- `/upload` — New series / Add episode (20 MB per panel, max 20 panels)
- `/voice` — audio upload ya browser se recording
- `/community` — Reddit-style threads, votes, nested comments
- `/chat` — live chat rooms (real-time polling)
- `/about` — owner profile + social handle management

## Local me chalane ke steps

```bash
npm install

# .env banayein (template ready hai)
cp .env.example .env
# .env me apna DATABASE_URL daalein (PostgreSQL)

# Tables banayein
npx drizzle-kit push --force

# Dev server
npm run dev
```

Pehli page request automatically starter content seed kar degi.

## GitHub pe push karna (2 tareeke)

### Tareeka 1 — GitHub web se (sabse easy)
1. GitHub pe jao → **New repository** → naam rakho `promiseme` (public ya private) → **Create** (README mat add karna, khaali rakho).
2. Repo page par **uploading an existing file** / **Drag and drop files** karo.
3. Is zip se **extract kiye gaye folder ka CONTENT** (files) select karke upload karo — folder khud nahi, uske andar ki files.
4. **Commit changes** dabao.

### Tareeka 2 — Terminal se
```bash
git init
git add .
git commit -m "promiseme.com initial commit"
git remote add origin https://github.com/YOUR_USERNAME/promiseme.git
git push -u origin main
```

## Permanent live deploy (Vercel)

1. Managed PostgreSQL banao (Neon / Supabase / Vercel Postgres / Railway).
2. Vercel me repo import karo (`vercel.json` already hai).
3. Environment variables:
   - `DATABASE_URL` = production DB connection string
   - `NEXT_PUBLIC_SITE_URL` = `https://promiseme.com`
   - `OWNER_EDIT_KEY` = koi lambi random string (sirf About page ke owner tools lock karta hai; users pe koi effect nahi)
4. Ek baar: `npx drizzle-kit push --force` (production DB pe).
5. Vercel → Domains me `promiseme.com` + `www.promiseme.com` add karo, registrar me DNS records daalo.

Poori details: `DEPLOYMENT.md` · Ownership clarity: `OWNERSHIP.md`

## Important

- `.env` zip me nahi hai — apna `DATABASE_URL` khud daalna hoga.
- Uploaded comics/voices/bytes database me store hote hain; same DB rakho to content permanent rahega.
- Sirf wo art/audio upload karo jiske rights tumhare paas hain.
