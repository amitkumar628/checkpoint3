# 🛠️ WORKFLOWS DOCUMENTATION

## 1. CI Pipeline (`.github/workflows/ci.yml`)

**Purpose:**  
Ensures code quality and project stability. It runs on every push and pull request to check code style, run tests, and build the project.

**Triggers:**  
- `on: push` to `main` and `develop` branches  
- `on: pull_request` to `main`

**Jobs:**
- **Lint:** Runs ESLint and Prettier to enforce coding standards.  
- **Test:** Runs Jest unit tests and checks code coverage (must be ≥ 80%).  
- **Build:** Builds the project and uploads build artifacts.

**Secrets:**  
- None required.

**Troubleshooting Tips:**  
- If linting fails → Run `npm run lint -- --fix`  
- If tests fail → Run `npm run test` locally and debug errors  
- If build fails → Ensure all dependencies are installed with `npm ci`

---

## 2. Dependency Audit (`.github/workflows/dependency-check.yml`)

**Purpose:**  
Performs a daily security audit of project dependencies and alerts you if vulnerabilities are found.

**Triggers:**  
- `on: schedule` (daily at 00:00 UTC)  
- `on: push` to `main`

**Jobs:**
- **Audit:** Uses `npm audit` to check for vulnerabilities and uploads the audit report as an artifact.

**Secrets:**  
- None required.

**Troubleshooting Tips:**  
- If job fails → Run `npm audit` locally to debug  
- If vulnerabilities exist → Upgrade or patch affected packages

---

## 3. Deployment (`.github/workflows/deploy.yml`)

**Purpose:**  
Automatically deploys the built project to GitHub Pages whenever code is pushed to the `main` branch.

**Triggers:**  
- `on: push` to `main`

**Jobs:**
- **Build and Deploy:** Installs dependencies, builds the project, and deploys the `dist/` folder to GitHub Pages.

**Secrets Required:**  
- `GH_PAGES_TOKEN` → Your GitHub Personal Access Token for deployment.

**Troubleshooting Tips:**  
- 403 error: Check that your `GH_PAGES_TOKEN` is valid and added to **Settings > Secrets**  
- Build errors: Ensure the `npm run build` command works locally  
- No page deployed: Verify `publish_dir: ./dist` matches your actual build folder

---

## 📊 Workflow Dependencies Overview

| Workflow | Trigger | Depends On | Secrets |
|----------|--------|------------|----------|
| CI Pipeline | Push/PR | None | None |
| Dependency Audit | Push/Schedule | None | None |
| Deploy | Push | Build job success | `GH_PAGES_TOKEN` |

---

✅ **You should now have:**

- `ci.yml` – Continuous Integration  
- `dependency-check.yml` – Security Audit  
- `deploy.yml` – Deployment  
- `README.md` – Project badges & overview  
- `WORKFLOWS.md` – Documentation (this file)

---

## 📁 Final Checklist for Part 3

- [x] Repository with 3+ workflow files  
- [x] Screenshot of successful workflow runs  
- [x] Actions tab showing ✅ green checks  
- [x] `README.md` with badges  
- [ ] ✅ `WORKFLOWS.md` with purpose, triggers, jobs, secrets, troubleshooting

---

### ✅ Final Step: Commit & Push

Once you’ve created and saved `WORKFLOWS.md`, run:

```bash
git add WORKFLOWS.md
git commit -m "Add WORKFLOWS.md documentation for Part 3"
git push origin main
