# Setup Guide for @animeshtripathii Profile README

Everything in this repository belongs in a public GitHub repository named exactly **`animeshtripathii`** (`github.com/animeshtripathii/animeshtripathii`). GitHub renders this magic repo's `README.md` at the top of your GitHub profile.

---

## 1. Quick Local Generation / Preview

All your initial cards, radars, and dot-matrix portrait have been pre-rendered into `assets/`!

To preview everything locally in dark and light themes:
- Open `preview.html` in your browser.

To regenerate artwork with different flags or update projects/skills:
```powershell
# 1. Regenerate Dot-Matrix Portrait from image.jpg
python scripts\dotify.py image.jpg -o assets\portrait --cols 100 --equalize --detail 0.5 --color

# 2. Regenerate Skills Radar (reads assets/skills.json)
python scripts\radar.py --data assets\skills.json -o assets\radar

# 3. Regenerate Language Radar (reads from GitHub API)
python scripts\radar.py --github animeshtripathii -o assets\radar-langs --values

# 4. Regenerate Stat Card and Project Cards (reads assets/projects.json)
python scripts\cards.py --user animeshtripathii --projects assets\projects.json --out assets
```

---

## 2. Push to GitHub

Initialize your repository, commit, and push to your magic profile repo:

```bash
git init
git branch -M main
git add .
git commit -m "feat: setup bespoke developer profile README"
git remote add origin https://github.com/animeshtripathii/animeshtripathii.git
git push -u origin main
```

> ⚠️ **Important**: The repository **must be Public**. If the repo is private, the SVG assets won't load for visitors.

---

## 3. Enable Workflow Write Permissions

For the automated GitHub Action robots to update your contribution graph, language metrics, and stat cards:

1. Go to your repo: `https://github.com/animeshtripathii/animeshtripathii`
2. Click **Settings** → **Actions** → **General**
3. Under **Workflow permissions**, select **Read and write permissions**
4. Click **Save**

---

## 4. Add `METRICS_TOKEN` Secret

`lowlighter/metrics` needs a GitHub Personal Access Token (classic) to generate the 3D isometric contribution calendar, achievements, and detailed stats.

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens) → **Generate new token (classic)**
2. Note: `Profile Metrics Token`
3. Scopes: Check **`read:user`** (and **`repo`** if you want private contributions included in counts)
4. Click **Generate token** and copy the token string
5. Go to your repo → **Settings** → **Secrets and variables** → **Actions**
6. Click **New repository secret**
7. Name: **`METRICS_TOKEN`** (exact match)
8. Value: Paste your token and click **Add secret**

---

## 5. Kick off Workflows (Automated Robots)

Go to the **Actions** tab on your repository:
Enable workflows if prompted, then click each workflow and run via **Run workflow**:

| Workflow | What it builds | Where it saves | Schedule |
|---|---|---|---|
| **Metrics** | 3D Isometric Calendar, Language Breakdown, Achievements | `assets/metrics.*.svg` on `main` | Every 6 hours |
| **Snake** | Snake eating your contribution graph animation | `snake*.svg` on `output` branch | Every 12 hours |
| **Charts and cards** | Radar charts, Stat Card, Project Cards | `assets/radar-*.svg`, `assets/card-*.svg` on `main` | Daily at 03:30 |

> 🐍 Note: The snake animation is served from `https://raw.githubusercontent.com/animeshtripathii/animeshtripathii/output/snake-dark.svg`. It will start rendering as soon as the Snake workflow finishes its first run!
