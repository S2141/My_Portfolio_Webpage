# Shubham Dhangar — Portfolio

Premium, single-page static portfolio. No backend, no database — everything
runs client-side or through free third-party endpoints, exactly as requested.

## ✅ What's included

- Dark/Light theme toggle (saved in localStorage)
- Animated AWS architecture, Kubernetes cluster, and CI/CD pipeline diagrams (inline SVG)
- 3D tilt effect on project cards (CSS transforms, mouse-tracked)
- GitHub live stats (via the free `github-readme-stats` image API — no server needed)
- Working contact form (via [FormSubmit.co](https://formsubmit.co) — no server needed)
- Resume download button (PDF bundled in `/assets/resume`)
- Fully responsive, keyboard-accessible, respects `prefers-reduced-motion`
- Dockerfile + nginx config (containerize and run anywhere)
- GitHub Actions workflow to auto-deploy to Vercel on every push to `main`

## ⚙️ Before you deploy — 2 things to edit

1. **GitHub username** — in `index.html`, search for `username=shubhamr-dhangar`
   (two places, inside the GitHub section) and replace with your real GitHub username.
2. **Contact form email** — it's already set to `shubhamr.dhangar2141@gmail.com`.
   The **first** time someone submits the form, FormSubmit sends a one-time
   confirmation link to that inbox — click it once to activate the form. After
   that, every submission arrives normally, no dashboard or signup required.

## 🚀 Deploy to Vercel (no GitHub Actions needed)

**Fastest way:**
1. Go to [vercel.com](https://vercel.com) → sign up.
2. "Add New → Project" → drag and drop this whole folder (or just `index.html` + `assets/`).
3. Deploy. You get a live URL in ~30 seconds.

**Auto-deploy on every push (uses the included GitHub Action):**
1. Push this folder to a new GitHub repo.
2. On [vercel.com](https://vercel.com), get your `VERCEL_TOKEN`
   (Account Settings → Tokens), and your `ORG_ID` / `PROJECT_ID`
   (run `vercel link` locally once, they appear in `.vercel/project.json`).
3. In your GitHub repo → Settings → Secrets and variables → Actions, add:
   - `VERCEL_TOKEN`
   - `VERCEL_ORG_ID`
   - `VERCEL_PROJECT_ID`
4. Push to `main` — the workflow in `.github/workflows/deploy.yml` deploys automatically.

## 🐳 Run with Docker (local or any container host)

```bash
docker build -t shubham-portfolio .
docker run -p 8080:80 shubham-portfolio
# open http://localhost:8080
```

## ☁️ Optional: deploy to AWS (since you're an AWS engineer)

Static hosting on S3 + CloudFront, entirely within the free tier for a low-traffic site:

```bash
aws s3 mb s3://shubham-portfolio-site
aws s3 sync . s3://shubham-portfolio-site --exclude ".git/*" --exclude ".github/*"
aws s3 website s3://shubham-portfolio-site --index-document index.html
# then put a CloudFront distribution in front of the bucket for HTTPS + caching
```

## 📁 Structure

```
.
├── index.html                 # the entire site (HTML/CSS/JS, self-contained)
├── assets/resume/*.pdf         # downloadable resume
├── Dockerfile
├── nginx.conf
├── .github/workflows/deploy.yml
└── README.md
```

## Notes on the "no backend / no database" constraint

There is intentionally no custom server or database here. The contact form
and GitHub stats both work through free, public, no-signup third-party
endpoints (FormSubmit and github-readme-stats), so the form genuinely sends
you email without you running or paying for any backend infrastructure.
