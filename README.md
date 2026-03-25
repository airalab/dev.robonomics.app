# Dev dApp ROBONOMICS NETWORK

**Development / Preview environment** for the [robonomics.app](https://robonomics.app) project

---

### About this repository

This repository contains the **development version** of robonomics.app.
It automatically publishes the content of the `dev` branch from the main repository.

- **Production website:** https://robonomics.app
- **Development / Preview website:** https://dev.robonomics.app

### Why do we need this repository?

- It allows you to quickly view new features, changes, and fixes **before** they are released to the main domain.
- Convenient for demonstrating work to clients, testers, or the team.
- Does not affect the stable version of the site.

### How it works

1. You make changes in the `dev` branch of the **main repository**.
2. GitHub Actions automatically builds the project.
3. The build result is published to this repository on the `main` branch.
4. The site becomes immediately available at **https://dev.robonomics.app**.

### Updating the dev version

Simply push your changes to the `dev` branch in the main repository — the preview site will update automatically within 1–2 minutes.

### Related repositories

- **Main repository** — [airalab/robonomics.app](https://github.com/airalab/robonomics.app) (`master` branch → production)

---

### Tech Stack

- Deployed via GitHub Actions + GitHub Pages

---

**Important:**
This repository is **not intended** for direct code editing.
All changes should be made only in the main repository in the `dev` branch.

---

If you have any questions or feedback regarding the dev version, please open an Issue in the [main repository](https://github.com/airalab/robonomics.app/issues).
