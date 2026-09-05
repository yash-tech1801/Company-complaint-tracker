---
name: github-pages-deploy
description: 'Publish Vite websites to GitHub Pages. Use when pushing a frontend repository to GitHub, configuring Pages actions, validating production builds, or troubleshooting deployment failures.'
argument-hint: 'Repository and deployment details'
---

# GitHub Pages Deployment

## What This Produces

This workflow publishes the Vite production build from the `main` branch to GitHub Pages using GitHub Actions.

## Procedure

1. Check the repository status, current branch, configured remote, and package manager lockfile.
2. Confirm the Vite production `base` matches the repository name, for example `/repository-name/`.
3. Run the repository's production build and lint checks locally when the required package manager is available.
4. Keep `.github/workflows/deploy.yml` enabled with `npm ci`, `npm run build`, Pages artifact upload, and Pages deployment steps.
5. Commit only the intended deployment changes with a clear message.
6. Push the target branch to the configured GitHub remote.
7. Monitor the Actions run and confirm the GitHub Pages environment URL after deployment succeeds.

## Decision Points

- Use GitHub Pages only when the repository's Pages setting can use GitHub Actions as its source.
- Use the repository name as the Vite `base` for project Pages sites; use `/` only for a custom domain or root Pages site.
- Do not overwrite an existing remote or discard unrelated working-tree changes without explicit approval.
- If local dependencies or the package manager are unavailable, rely on the CI build only after checking the lockfile and build script.

## Completion Checks

- The target branch is pushed successfully.
- The GitHub Actions workflow completes its build and deploy jobs.
- The deployed URL loads the app assets from the configured base path.