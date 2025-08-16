# Task 6 — GitHub Pages Static Site

**Purpose:** Publish a simple static web page with **GitHub Pages** and submit the **live URL** and the **repository link**.

---

## What you will submit
- ✅ **Live website link:** `https://saeedzawarudo-afk.github.io/Task6/`
- ✅ **GitHub repository:** `https://github.com/saeedzawarudo-afk/Task6`

(Screenshots are optional; a short checklist is included below.)

---

## Option A — Do everything in the GitHub Web UI (easiest)

1. **Create the repo**
   - Go to GitHub → **New repository** → name it **Task6** → keep it **Public** → **Create repository**.

2. **Add the site files**
   - Click **Add file → Create new file** → name it **`index.html`** and paste the content below (see *Sample index.html*).
   - *(Optional)* Add **`styles.css`** (see sample below) via **Add file → Create new file**.
   - Commit directly to the **main** branch.

3. **Enable GitHub Pages**
   - Repo **Settings → Pages**.
   - **Build and deployment → Source:** *Deploy from a branch*.
   - **Branch:** `main` and **/ (root)** → **Save**.

4. **Open your live site**
   - Wait ~30–60 seconds for the build, then open the link shown at the top of the Pages section, or browse to:
     - `https://saeedzawarudo-afk.github.io/Task6/`

5. **Add a README**
   - Back on the repo root, click **Add file → Create new file** → name it **`README.md`** and paste this document (or your own).

---

## Option B — Do it from your Azure Linux VM (terminal)

> Use this if you prefer to create files and push from the VM.

```bash
# 1) Create project folder and files
mkdir -p ~/Task6 && cd ~/Task6

# index.html
cat > index.html <<'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Task 6 — GitHub Pages Demo</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <h1>Task 6 — GitHub Pages</h1>
  <p>Hello from GitHub Pages!</p>
</body>
</html>
EOF

# styles.css (optional)
echo "body{font-family:system-ui,Arial,sans-serif;margin:24px}" > styles.css

# 2) Initialize git and commit
sudo apt-get update && sudo apt-get install -y git
git init
git config user.name  "saeedzawarudo-afk"
git config user.email "you@example.com"
git add .
git commit -m "Task6: initial static site"

# 3) Create an empty repo named Task6 on GitHub (UI). Then set the remote.

# --- SSH method (recommended) ---
# Generate a key ONCE if you don't have one:
ssh-keygen -t ed25519 -C "vm-task6" -N "" -f ~/.ssh/id_ed25519
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
# Show public key; copy it to GitHub → Settings → SSH and GPG keys → New SSH key
cat ~/.ssh/id_ed25519.pub

git remote add origin git@github.com:saeedzawarudo-afk/Task6.git
git branch -M main
git push -u origin main

# --- OR HTTPS + Personal Access Token (PAT) ---
# git remote add origin https://github.com/saeedzawarudo-afk/Task6.git
# git branch -M main
# git push -u origin main   # use your PAT when prompted (not your password)
```

4) **Enable GitHub Pages**
   - Same as Option A: **Settings → Pages → Deploy from a branch → Branch main / root → Save**.
   - Open your live site: `https://saeedzawarudo-afk.github.io/Task6/`.

---

## Sample `index.html` (copy–paste)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Task 6 — GitHub Pages Demo</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <header>
    <h1>Task 6 — GitHub Pages Demo</h1>
    <p>Deployed via GitHub Pages 🚀</p>
  </header>
  <main>
    <h2>Welcome!</h2>
    <p>If you can read this at <strong>https://saeedzawarudo-afk.github.io/Task6/</strong>, your Task 6 is live.</p>
  </main>
</body>
</html>
```

## Sample `styles.css` (optional)

```css
* { box-sizing: border-box; }
body { font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; margin: 0; color: #222; }
header { background: #f6f8fa; padding: 24px; text-align: center; }
main { max-width: 800px; margin: 24px auto; padding: 0 16px; }
```

---

## Screenshot checklist (optional but nice to include)

Place in `docs/screenshots/`:
1. **Pages settings** — Settings → Pages (shows “Deploy from a branch”, `main`/`root`, and the published URL).
2. **Live site** — Browser at `https://saeedzawarudo-afk.github.io/Task6/`.
3. **Repo root** — File list showing `index.html` (and `styles.css` if used).
4. *(Optional)* **Commit history**.

Suggested names:
```
docs/screenshots/01-pages-settings.png
docs/screenshots/02-live-site.png
docs/screenshots/03-repo-files.png
docs/screenshots/04-commit-history.png
```

---

## Troubleshooting

- **404 / page not found**  
  Re-check **Settings → Pages**. Source must be **Deploy from a branch**, **Branch: main / root**. Give it ~1–2 minutes after enabling or pushing changes.

- **Permission denied (publickey) when pushing**  
  You’re using SSH without adding your VM’s public key to GitHub. Add `~/.ssh/id_ed25519.pub` to **Settings → SSH and GPG keys**, or switch the remote to HTTPS and use a **Personal Access Token**.

- **Assets not loading / CSS missing**  
  Keep files in repo root and link them with relative paths (e.g., `styles.css`).

- **Wrong URL**  
  Project pages live at `https://<username>.github.io/<repo-name>/` (not just the username).

---

## Repo structure (final)

```
Task6/
├─ index.html
├─ styles.css        # optional
└─ README.md         # this file
```

Good luck! Once your site is live, copy the **live URL** and your **repo link** for submission.
