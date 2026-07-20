# Next.js + TypeScript + pnpm Setup Guide
## ESLint + Prettier + Husky + lint-staged (2026)

This guide configures a professional code quality workflow for a **Next.js + TypeScript** project using **pnpm**.

---

# Tech Stack

- Next.js
- TypeScript
- pnpm
- ESLint
- Prettier
- Husky
- lint-staged
- Git

---

# Project Structure

```text
my-app/
│
├── .husky/
│   └── pre-commit
│
├── .vscode/
│   └── settings.json
│
├── app/
├── components/
├── lib/
├── public/
│
├── .prettierrc
├── .prettierignore
├── eslint.config.mjs
├── package.json
├── tsconfig.json
├── pnpm-lock.yaml
└── next.config.ts
```

---

# Step 1 - Install Dependencies

Install ESLint, Prettier, Husky and lint-staged.

```bash
pnpm add -D eslint eslint-config-next typescript @types/node prettier eslint-config-prettier prettier-plugin-tailwindcss husky lint-staged eslint-plugin-import eslint-plugin-unused-imports
```

---

# Step 2 - Initialize Husky

```bash
pnpm exec husky init
```

This creates

```text
.husky/
```

---

# Step 3 - Update package.json

Add the following scripts.

```json
{
  "scripts": {
    "dev": "next dev",

    "build": "next build",

    "start": "next start",

    "lint": "next lint",

    "lint:fix": "next lint --fix",

    "format": "prettier --write .",

    "format:check": "prettier --check .",

    "prepare": "husky"
  }
}
```

---

# Step 4 - Configure lint-staged

Add this to package.json.

```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix"
    ],
    "*.{js,jsx,ts,tsx,json,css,scss,md}": [
      "prettier --write"
    ]
  }
}
```

---

# Step 5 - Configure Husky

Open

```text
.husky/pre-commit
```

Replace everything with

```sh
pnpm exec lint-staged
```

---

# Step 6 - Create .prettierrc

```json
{
  "semi": true,
  "singleQuote": false,
  "tabWidth": 2,
  "useTabs": false,
  "printWidth": 100,
  "trailingComma": "all",
  "arrowParens": "always",
  "bracketSpacing": true,
  "endOfLine": "lf",
  "plugins": [
    "prettier-plugin-tailwindcss"
  ]
}
```

---

# Step 7 - Create .prettierignore

```text
node_modules

.next

out

coverage

dist

pnpm-lock.yaml

package-lock.json

*.log

public

*.svg
```

---

# Step 8 - Configure ESLint

If your project was created with **create-next-app**, it already includes an `eslint.config.mjs`. Update it as needed.

Example:

```javascript
import { dirname } from "path";
import { fileURLToPath } from "url";
import { FlatCompat } from "@eslint/eslintrc";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

const compat = new FlatCompat({
  baseDirectory: __dirname,
});

export default [
  ...compat.extends(
    "next/core-web-vitals",
    "next/typescript",
    "prettier",
  ),

  {
    rules: {
      "no-console": "warn",

      "@typescript-eslint/no-unused-vars": "warn",

      "prefer-const": "error",

      "no-var": "error",

      "eqeqeq": "error"
    }
  }
];
```

---

# Step 9 - VS Code Settings

Create

```text
.vscode/settings.json
```

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "editor.formatOnSave": true,

  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "always"
  },

  "eslint.validate": [
    "javascript",
    "typescript",
    "javascriptreact",
    "typescriptreact"
  ]
}
```

---

# Step 10 - Recommended VS Code Extensions

Install

```
ESLint
```

```
Prettier
```

```
Tailwind CSS IntelliSense
```

```
Error Lens
```

```
Path IntelliSense
```

```
GitLens
```

---

# Step 11 - Verify Setup

Run ESLint

```bash
pnpm lint
```

Fix automatically

```bash
pnpm lint:fix
```

Run Prettier

```bash
pnpm format
```

Check formatting

```bash
pnpm format:check
```

---

# Step 12 - Test Husky

```bash
git add .

git commit -m "test"
```

Expected flow

```
git commit
      │
      ▼
Husky
      │
      ▼
lint-staged
      │
      ├── ESLint --fix
      └── Prettier --write
      │
      ▼
Commit
```

---
<br>
<br>

# Push Project to GitHub (pnpm Project)

## Step 1 - Check Git Status

```bash
git status
```

Expected:

```
On branch main
nothing to commit, working tree clean
```

---

## Step 2 - Verify Remote

```bash
git remote -v
```

If nothing appears, add the GitHub repository.

---

## Step 3 - Add Remote Repository

```bash
git remote add origin https://github.com/PurushottamPortfolio-Repo/SEE
```

Verify:

```bash
git remote -v
```

Expected:

```
origin  https://github.com/PurushottamPortfolio-Repo/SEE.git (fetch)

origin  https://github.com/PurushottamPortfolio-Repo/SEE.git (push)
```

---

## Step 4 - Rename Branch to main (Recommended)

```bash
git branch -M main
```

Verify

```bash
git branch
```

Expected

```
* main
```

---

## Step 5 - Push Code

```bash
git push -u origin main
```

The `-u` flag sets `origin/main` as the default upstream branch.

You only need this command once.

---

## Step 6 - Verify on GitHub

Refresh your repository.

```
SEE/
├── app/
├── components/
├── public/
├── package.json
├── pnpm-lock.yaml
├── next.config.ts
├── tsconfig.json
└── ...
```

---

# Future Workflow

After making changes:

## Check changes

```bash
git status
```

---

## Stage changes

```bash
git add .
```
---

## Commit

```bash
git commit -m "Add hero section"
```

Husky will automatically run:

- ESLint
- Prettier
- lint-staged

If there are linting errors, the commit will stop until you fix them.

---

## Push

```bash
git push
```
<br>

## Daily Development Workflow

```text
Write Code
     │
     ▼
pnpm dev
     │
     ▼
Save File
     │
     ▼
ESLint + Prettier (VS Code)
     │
     ▼
git status
     │
     ▼
git add .
     │
     ▼
git commit -m "Meaningful commit message"
     │
     ▼
Husky
     │
     ▼
lint-staged
     │
     ├── ESLint
     ├── Prettier
     └── Validation
     │
     ▼
Commit Successful
     │
     ▼
git push
     │
     ▼
GitHub
     │
     ▼
Vercel Auto Deploy (if connected)
```
---
<br>

## Common Git Commands

## Check current branch

```bash
git branch
```

## View remotes

```bash
git remote -v
```

## View commit history

```bash
git log --oneline
```

## Pull latest changes

```bash
git pull origin main
```

## Push latest changes

```bash
git push
```

## Check differences

```bash
git diff
```

## View staged files

```bash
git diff --cached
```

## Remove a file from staging

```bash
git restore --staged <file-name>
```

## Create a new branch

```bash
git checkout -b feature/navbar
```

## Switch branches

```bash
git checkout main
```

## Merge a branch

```bash
git merge feature/navbar
```

# Useful pnpm Commands

Install packages

```bash
pnpm add package-name
```

Install dev dependency

```bash
pnpm add -D package-name
```

Remove package

```bash
pnpm remove package-name
```

Update package

```bash
pnpm update
```

List packages

```bash
pnpm list
```

Install all

```bash
pnpm install
```

Approve build scripts

```bash
pnpm approve-builds
```

Clean install

```bash
rm -rf node_modules

rm pnpm-lock.yaml

pnpm install
```

---

# Common Issues

## Husky doesn't run

Run

```bash
pnpm exec husky init
```

Check

```bash
package.json
```

contains

```json
"prepare": "husky"
```

---

## lint-staged not found

Use

```bash
pnpm exec lint-staged
```

instead of

```bash
npx lint-staged
```

---

## Prettier not formatting

Check

```
Prettier VS Code extension
```

Enable

```
Format On Save
```

---

## Tailwind classes not sorting

Install

```bash
pnpm add -D prettier-plugin-tailwindcss
```

Add plugin

```json
{
  "plugins": [
    "prettier-plugin-tailwindcss"
  ]
}
```

---

## pnpm blocks build scripts

Run

```bash
pnpm approve-builds
```

Select required packages

Press

```
Space
```

Then

```
Enter
```

---

# Recommended Workflow

```
Developer
      │
      ▼
Write Code
      │
      ▼
Save File
      │
      ▼
ESLint Fix
      │
      ▼
Prettier Format
      │
      ▼
Git Add
      │
      ▼
Git Commit
      │
      ▼
Husky
      │
      ▼
lint-staged
      │
      ├── ESLint
      ├── Prettier
      └── Validation
      │
      ▼
Commit Success
      │
      ▼
Push to GitHub
      │
      ▼
Vercel Deployment
```

---

# Best Practices

- Use **pnpm** consistently (avoid mixing with npm or yarn).
- Keep **ESLint** responsible for code quality and potential bugs.
- Use **Prettier** only for code formatting.
- Let **Husky** enforce checks before every commit.
- Use **lint-staged** to lint and format only staged files for faster commits.
- Enable **format on save** in VS Code for an automated workflow.
- Run `pnpm lint` and `pnpm format:check` in your CI pipeline before deployment.
- Commit the `pnpm-lock.yaml` file to version control.