# Contribution Guide

Thanks for your interest in contributing ❤️

This repository contains a reusable contribution guide that can be applied across different projects. The goal is simple: make contributing easy, keep communication clear, and maintain high-quality changes without unnecessary friction.

---

## Using AI

AI tools are welcome, but there are two principles that really matter:

### 1. Don’t let an LLM speak for you

Comments, issues, commit messages, and pull request descriptions should sound like a real person.

They don’t need perfect grammar — but they should be clear, honest, and specific.

If you use AI to improve wording, make sure the final result still reflects what *you* actually mean. Overly polished, generic text is often less trustworthy than a short, imperfect human explanation.

---

### 2. Don’t let an LLM think for you

Using AI to explore ideas, generate code, or draft tests is fine. Submitting code you don’t understand is not.

Before opening a PR, make sure you can explain:

* what changed
* why it changed
* how it was tested
* what tradeoffs or limitations remain

Every contribution should have a human behind it who takes responsibility for the result.

---

## Repository Setup

Most projects use `pnpm`, some use `yarn`.

### Typical setup

1. Install the latest Node.js LTS
2. Enable Corepack:

```bash
corepack enable
```

3. Install dependencies:

```bash
pnpm install
```

---

## Common Commands

### `pnpm dev`

Starts the development environment.

* For Node.js packages: usually runs the build in watch mode
* For frontend projects: usually starts the dev server

---

### `pnpm play`

Starts a local playground (if available).

---

### `pnpm build`

Builds the project for production. Output is typically written to `dist/`.

---

### `pnpm lint`

Runs ESLint for linting and formatting.

Auto-fix issues when possible:

```bash
pnpm lint --fix
```

> Prettier is not used in these projects.

---

### `pnpm test`

Runs the test suite (usually with Vitest).

Examples:

```bash
pnpm test --run
pnpm test foo
```

Some repositories may also include:

* `pnpm test:unit`
* `pnpm test:e2e`
* `pnpm typecheck`
* `pnpm docs`
* `pnpm docs:build`

If you're unsure what’s available:

```bash
pnpm run
```

---

## Before Opening a Pull Request

Please go through this checklist:

* Ensure the change is ready for review
* Run `pnpm lint --fix`
* Run relevant tests
* Run type checking (if used)
* Run a production build (for apps/packages)

If your change is large or introduces a new feature, opening an issue first is usually the best path. Early discussion saves time.

---

## Pull Request Guidelines

### Discuss bigger features first

Bug fixes and small improvements can usually go straight to a PR.

For larger features or API changes, open an issue first so we can align on direction and scope.

---

### Keep typo fixes bundled

If you're fixing documentation or typos, group multiple fixes into a single PR instead of opening many small ones.

---

### Use Conventional Commits

Commit messages should follow the Conventional Commits format:

```text
feat: add support for workspace config
fix: handle empty input correctly
docs: improve installation instructions
chore: update dev dependencies
```

* `feat:` and `fix:` usually appear in changelogs
* `docs:` is for documentation-only changes
* `chore:` is for maintenance work that doesn’t affect behavior

---

### Use the same style for PR titles

Your pull request title should follow the same convention.

---

### Link related issues

If your PR resolves an issue, include:

```text
fix #123
```

This allows GitHub to automatically close the issue after merge.

---

### Multiple commits are fine

You don’t need to squash commits unless explicitly required.

A clear PR matters more than a perfectly clean commit history. Squashing can always be done during merge.

---

## Maintenance Notes

*(Mostly for maintainers or fork maintainers)*

---

### Updating dependencies

Dependencies should be reviewed and updated regularly.

For monorepos, a common workflow:

```bash
taze major -Ir
pnpm install
pnpm build
pnpm test
```

Update carefully and verify everything still builds and passes tests before pushing.

---

### Releasing

Before creating a release:

* ensure your branch is up to date with upstream
* ensure CI is passing

Typical release command:

```bash
pnpm release
```

This usually:

* bumps versions
* creates a release commit
* creates a Git tag

Publishing may happen:

* locally
* or in CI after a tag is pushed

If publishing from CI, you may need to configure secrets like `NPM_TOKEN`.

---

## Tooling Notes

### Corepack

Corepack ensures contributors use the correct package manager version:

```json
{
  "packageManager": "pnpm@7.1.5"
}
```

Usually, you only need to run:

```bash
corepack enable
```

once after installing Node.js.

---

### ESLint

ESLint is used for both linting and formatting.

For VS Code, enable auto-fix on save:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true
  }
}
```

---

### No Prettier

Since ESLint handles formatting, Prettier is unnecessary here.

If your editor runs Prettier automatically, consider disabling it for this project to avoid conflicts.

---

## Final Note

The best contributions are:

* thoughtful
* understandable
* considerate to future readers

You don’t need to be perfect to contribute.

You *do* need to care about what you’re changing.
