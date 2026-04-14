# Contribution Guide

Thanks for your interest in contributing.

This repository contains a general contribution guide I can reuse across projects. The goal is simple: make it easy for people to help, communicate clearly, and keep contributions high-quality without making the process feel heavy.

## Using AI

AI tools are welcome, but there are two rules that matter:

### 1. Don't let an LLM speak for you

Comments, issues, commit messages, and pull request descriptions should sound like a real person. They do not need perfect grammar. They do need honesty and clarity.

If you use AI to polish wording, make sure the final text still reflects what you actually mean. Long, generic, overly polished summaries are usually harder to trust than a short human explanation.

### 2. Don't let an LLM think for you

Using AI to explore ideas, generate code, or draft tests is fine. Submitting code you do not understand is not.

Before opening a PR, make sure you can explain:

- what changed
- why it changed
- how it was tested
- what tradeoffs or limitations remain

Every contribution should have a human behind it who takes responsibility for the result.

## Repository Setup

Most of my projects use `pnpm`, and some use `yarn`.

Typical setup:

1. Install the latest Node.js LTS.
2. Enable Corepack:

```bash
corepack enable
```

3. Install dependencies in the project root:

```bash
pnpm install
```

## Common Commands

### `pnpm dev`

Starts the development environment.

- For Node.js packages, this often runs the build in watch mode.
- For frontend projects, this usually starts the dev server.

### `pnpm play`

Starts a local playground when the repository has one.

### `pnpm build`

Builds the project for production. Output is often written to `dist/`.

### `pnpm lint`

Runs ESLint for linting and formatting.

Use this to auto-fix issues when possible:

```bash
pnpm lint --fix
```

I do not use Prettier in these projects.

### `pnpm test`

Runs the test suite, usually with Vitest.

Useful variations:

```bash
pnpm test --run
pnpm test foo
```

Some repositories may also include commands like:

- `pnpm test:unit`
- `pnpm test:e2e`
- `pnpm typecheck`
- `pnpm docs`
- `pnpm docs:build`

If you are unsure what a project supports, run:

```bash
pnpm run
```

## Before Opening a Pull Request

Please go through this short checklist:

1. Make sure the change is actually ready to review.
2. Run `pnpm lint --fix`.
3. Run the relevant tests.
4. Run type checking if the repository uses it.
5. Run a production build if the project ships packages or apps.

If your change is large or introduces a new feature, opening an issue first is usually the best path. Early discussion saves time for everyone.

## Pull Request Guidelines

### Discuss bigger features first

Bug fixes and small improvements can usually go straight to a PR.

For larger features or API changes, please open an issue first so we can align on whether the idea fits the project and what shape it should take.

### Keep typo fixes bundled

If you are fixing docs or typos, it is better to group several small fixes into one PR instead of opening many tiny ones.

### Use Conventional Commits

Commit messages should follow the Conventional Commits style.

Examples:

```text
feat: add support for workspace config
fix: handle empty input correctly
docs: improve installation instructions
chore: update dev dependencies
```

Only `feat:` and `fix:` are typically used for changelog entries. Documentation-only changes should use `docs:`. Maintenance work that does not affect product behavior should usually use `chore:`.

### Use the same style for PR titles

Your pull request title should also follow the same commit convention.

### Link related issues

If the PR resolves an issue, add a line like this to the PR description:

```text
fix #123
```

That helps GitHub link and close the issue automatically after merge.

### Multiple commits are fine

You do not need to squash everything locally unless the repository explicitly asks for it. A clean PR matters more than a perfectly curated commit graph. Squashing can happen during merge.

## Maintenance Notes

This section is mainly for maintainers or people maintaining their own forks.

### Updating dependencies

Dependencies should be reviewed and updated regularly. I usually prefer manual updates with [`taze`](https://github.com/antfu-collective/taze) instead of relying only on automated bots.

For monorepos, a common workflow is:

```bash
taze major -Ir
pnpm install
pnpm build
pnpm test
```

Update carefully, then verify the project still builds and passes tests before pushing changes.

### Releasing

Before creating a release:

- make sure your branch includes the latest upstream changes
- make sure CI is green

Most of the time, releases are done with:

```bash
pnpm release
```

This usually bumps versions, creates the release commit, and adds a Git tag.

Depending on the project, publishing may happen:

- locally on your machine
- in CI after a version tag is pushed

If publishing happens in CI for your fork, you may need to configure secrets like `NPM_TOKEN`.

## Tooling Notes

### Corepack

Corepack helps ensure contributors use the correct package manager version defined by the repository.

```json
{
  "packageManager": "pnpm@7.1.5"
}
```

Once Node.js is installed, you usually only need to run this once:

```bash
corepack enable
```

### ESLint

ESLint is used for both linting and formatting, often through `@antfu/eslint-config`.

If you use VS Code, enabling ESLint fixes on save is recommended:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true
  }
}
```

### No Prettier

Because ESLint already handles formatting, Prettier is usually unnecessary here. If your editor runs Prettier automatically, it is a good idea to disable it for the project to avoid conflicts.

## Final Note

The best contributions are thoughtful, understandable, and kind to the next person who reads them.

You do not need to be perfect to contribute. You do need to care about what you are changing.
