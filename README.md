# Shubham Dhangar — Portfolio Website

Static single-page portfolio site. No build step, no npm install required.

## Project structure
```
.
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Actions — auto-deploys to GitHub Pages on push to main
├── assets/
│   └── Shubham_Dhangar_Resume.pdf   # downloadable CV, linked from the site
├── Dockerfile                # containerize and serve via nginx
├── nginx.conf                 # nginx config used inside the container
├── index.html                 # the entire site (HTML + CSS + JS in one file)
└── README.md
```

## Run locally

**Option A — just open it**
Open `index.html` directly in a browser. The Download CV / contact form / all links work as-is.

**Option B — local server**
```
python3 -m http.server 8000
```
Visit http://localhost:8000

**Option C — Docker**
```
docker build -t shubham-portfolio .
docker run -p 8080:80 shubham-portfolio
```
Visit http://localhost:8080

## Deploy

**GitHub Pages (automatic)**
Push this repo to GitHub with the default branch named `main`. The included workflow (`.github/workflows/deploy.yml`) builds and publishes the site to GitHub Pages automatically — enable Pages under **Settings → Pages → Source: GitHub Actions** once.

**Vercel**
`vercel deploy` in this folder, or drag-and-drop the folder at vercel.com/new

**Netlify**
Drag-and-drop the folder at app.netlify.com/drop

**Any Docker host (Fly.io, Render, a VPS, etc.)**
Build the image from the included `Dockerfile` and deploy it — nginx serves the site on port 80.

## Edit content
All text (summary, skills, experience, projects, education, contact) lives directly in `index.html` — search for the relevant section id (`#about`, `#skills`, `#experience`, `#projects`, `#education`, `#contact`) and edit in place.

To swap the CV, replace `assets/Shubham_Dhangar_Resume.pdf` with a new file of the same name (or update the three `href="assets/..."` references in `index.html` if you rename it).

## Customize colors
All colors are CSS variables at the top of the `<style>` block in `index.html`, under `:root` — change `--cyan`, `--amber`, `--bg`, etc.
