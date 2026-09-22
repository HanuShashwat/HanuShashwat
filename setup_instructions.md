# GitHub Profile Setup Guide for Hanu Shashwat

This guide walks you through deploying your new terminal-style README to your GitHub profile and enabling the automatic daily statistics workflow.

---

## 1. Create Your Profile Repository on GitHub

GitHub provides a special feature: when you create a public repository with the exact same name as your GitHub username, GitHub displays its `README.md` on your user profile page.

1. Navigate to [GitHub New Repository](https://github.com/new).
2. Repository name: **`HanuShashwat`** (must match your username exactly).
3. Set visibility to **Public**.
4. Check **Add a README file** (or leave it unchecked if you will push directly).
5. Click **Create repository**.

---

## 2. Generate a Personal Access Token (PAT)

The workflow needs a GitHub token to query the GraphQL API for your commits, lines of code, and stars.

1. Go to **Settings** → **Developer Settings** → **Personal Access Tokens** → **Fine-grained tokens** (or [click here](https://github.com/settings/tokens?type=beta)).
   * *(Alternatively, classic tokens also work: `repo`, `read:user` permissions).*
2. Token name: `README_STATS_TOKEN`.
3. Resource owner: `HanuShashwat`.
4. Repository access: **All repositories** (or select all public & private repos you want included in stats).
5. Repository permissions:
   * **Commit statuses**: Read-only
   * **Contents**: Read-only
   * **Metadata**: Read-only
   * **Pull requests**: Read-only
6. Account permissions:
   * **Followers**: Read-only
   * **Starring**: Read-only
   * **Watching**: Read-only
7. Generate token and copy the secret string (`github_pat_...`).

---

## 3. Add `ACCESS_TOKEN` Secret to Your Repository

1. Open your repository: `https://github.com/HanuShashwat/HanuShashwat`.
2. Go to **Settings** → **Secrets and variables** → **Actions**.
3. Click **New repository secret**.
4. Name: **`ACCESS_TOKEN`**.
5. Secret: Paste the token you generated in Step 2.
6. Click **Add secret**.

---

## 4. Push Files to GitHub

From this folder (`c:\Users\hanus\Python\readme`), initialize git and push to your `HanuShashwat` repository:

```bash
git init
git add README.md dark_mode.svg light_mode.svg today.py .github/ cache/ setup_instructions.md
git commit -m "Initialize terminal profile README and daily telemetry"
git branch -M main
git remote add origin https://github.com/HanuShashwat/HanuShashwat.git
git push -u origin main
```

---

## 5. Test the Automation

1. In your GitHub repository, click on the **Actions** tab.
2. Select **Profile README Daily Build** on the left.
3. Click **Run workflow** → **Branch: main** → **Run workflow**.
4. The workflow will execute `today.py`, recalculate your total lines of code, commits, repositories, and stars, and push the updated SVGs back to your repository automatically.
