# Nitin Sharma — Portfolio

Personal portfolio website with GitHub Actions CI/CD pipeline.

## 🚀 Quick Setup

### 1. Create a GitHub repo
```bash
git init
git add .
git commit -m "feat: initial portfolio"
git remote add origin https://github.com/YOUR_USERNAME/portfolio.git
git push -u origin main
```

### 2. Enable GitHub Pages
- Go to your repo → **Settings** → **Pages**
- Source: **GitHub Actions**
- Save

That's it. Your site deploys automatically on every push.

---

## 📁 File Structure

```
portfolio/
├── index.html                  ← The website
├── data.json                   ← ✏️ EDIT THIS to update content
├── README.md
└── .github/
    └── workflows/
        ├── deploy.yml          ← Auto-deploy on push to main
        └── update-badge.yml    ← Auto-update "last updated" date
```

---

## ✏️ How to Update Content

**All content lives in `data.json`.** You never need to touch `index.html`.

### Add a new project:
```json
{
  "name": "My New Project",
  "company": "Personal",
  "type": "oss",
  "github_url": "https://github.com/...",
  "description": "What it does.",
  "impact": "What it achieved.",
  "stack": ["Python", "FastAPI", "LangChain"]
}
```

### Update a stat:
```json
{ "number": "3+", "label": "Years of experience" }
```

Then just:
```bash
git add data.json
git commit -m "feat: add new project"
git push
```
GitHub Actions deploys it in ~60 seconds. ✅

---

## ⚙️ GitHub Actions Workflows

### `deploy.yml`
**Triggers on:** every push to `main`

**What it does:**
1. Validates `data.json` is valid JSON with all required fields
2. Runs Lighthouse CI performance audit
3. Deploys to GitHub Pages

**What you learn:** CI/CD, job dependencies (`needs:`), permissions, artifacts

---

### `update-badge.yml`
**Triggers on:** every push to `main`

**What it does:**
- Updates the "Last updated: ..." date in the footer automatically
- Commits the change back with `[skip ci]` to avoid infinite loops

**What you learn:** Git operations in Actions, `git config`, committing back from workflows, `[skip ci]` pattern

---

## 🔧 Customization

### Change colors
Open `index.html` and edit the `:root` CSS variables:
```css
:root {
  --accent: #63d6a8;    /* Main green color */
  --accent2: #4fb8f0;   /* Blue accent */
  --accent3: #f0a84b;   /* Amber accent */
}
```

### Update LinkedIn/GitHub links
Edit `data.json`:
```json
"linkedin": "https://linkedin.com/in/YOUR_USERNAME",
"github": "https://github.com/YOUR_USERNAME"
```

---

## 📬 Contact Form

The form currently shows a success state (UI only). To make it functional:

1. Go to [formspree.io](https://formspree.io) → create a free form → get your endpoint
2. In `index.html`, update the `handleSubmit` function:
```javascript
async function handleSubmit(e) {
  e.preventDefault();
  const form = e.target;
  const data = new FormData(form);
  await fetch('https://formspree.io/f/YOUR_FORM_ID', {
    method: 'POST',
    body: data,
    headers: { 'Accept': 'application/json' }
  });
  // ... rest of success handling
}
```
