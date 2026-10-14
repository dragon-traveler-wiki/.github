# Contributing to Dragon Traveler Wiki

## Pull requests

Use a short-lived feature or fix branch and open a pull request into the repository's default branch. Keep each change focused and describe the resulting behavior and why it is needed. Source changes must go through a pull request and the repository's required CI checks, including changes by administrators. Resolve review conversations before merging. Squash merges are recommended for focused changes; use the merge methods enabled by the repository. Merged branches are deleted automatically where configured.

## Project documentation and checks

Start with the project's README Contributing section and `docs/development.md` for setup, architecture, formatting, and checks. The data pipeline also keeps game-update, asset-synchronization, and recovery instructions in `docs/operations.md`. Follow any local agent instructions. Run the relevant checks before opening a pull request, and state anything that could not be verified. Keep package lockfiles or pinned dependencies synchronized with dependency changes. Dependency and GitHub Actions updates are reviewed weekly; upgrades that must happen together should remain grouped.

## GitHub workflows

Use `.yml` files with kebab-case names. Standard entry points are `ci.yml` (CI), `checks.yml` (Checks, when reusable), and `deploy-pages.yml` (Deploy Pages); name project-specific workflows by their task. Keep required status-check names stable when refactoring, and update workflow-name triggers, cross-repository dispatches, badges, tests, and documentation together when renaming files or workflows.

Use pinned Actions commits, explicit timeouts, read-only default repository permissions, and scoped write permissions for publishing jobs. Read-only checkouts should not retain credentials. Cancel superseded CI runs, but serialize publishing workflows that share output. Filter expensive deployments to relevant changes while retaining manual dispatch.

## Game data and compatibility

Published game data lives on `main` of the private `dragon-traveler-data` repository. Data mined from the game client and hand-maintained files under `data/manual/` are committed through pull requests like source changes. The scheduled event workflow is the one exception: it commits refreshed event data directly to `main`, so do not edit its output by hand. Binary assets are published to Cloudflare R2; Git tracks only `assets/manifest.json`.

The Pydantic schemas in `dragon_traveler_data.schemas` define the published data contract. When that contract changes, update the wiki's feature types and validation in the same release window, add representative regression coverage, and verify the wiki builds against the new data before merging it into `main`, which redeploys the wiki.

## Issues and security

Report bugs and propose features through issues in the affected repository. Wiki content suggestions can also be submitted from the site. For a vulnerability, use the repository's private vulnerability-reporting mechanism when enabled instead of posting sensitive details publicly.

## Maintaining documentation

Keep READMEs focused on purpose, the live site, quick start, and documentation links. Put project-specific development and operations details in `docs/`; use the README's Contributing section to link them and this shared policy. A local `CONTRIBUTING.md` is unnecessary when those links cover the project. GitHub uses this organization-level file as the default contribution guide when a repository has none of its own.

Each topic should have one authoritative home. The data contract lives in the data repository's schemas, and user-facing help lives on the wiki itself. Update links, package manifests, examples, and documentation checks when moving files. Verify commands against current scripts and workflows, and document relevant failure and recovery behavior.

## Shared community repository

The `dragon-traveler-wiki/.github` repository hosts this guide, the default `PULL_REQUEST_TEMPLATE.md`, and the organization profile in `profile/README.md`. Templates and guidance are inherited where a repository has no local override. Its `.github/rulesets/main.json` describes protection for this repository alone; it does not configure other repositories automatically.

This repository contains community documents rather than application code and currently has no CI workflow. Review Markdown links and content before merging its required PRs. Changes to shared guidance should remain applicable across projects; keep project commands and data contracts in the affected repository.
