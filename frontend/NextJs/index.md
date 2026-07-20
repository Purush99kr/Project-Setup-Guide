# Next.js + TypeScript + pnpm + Husky + shadcn/ui Setup (2026)

## 1. Create Project
```bash
pnpm create next-app@latest my-app
```

Choose:
- ✔ TypeScript
- ✔ ESLint
- ✔ Tailwind CSS
- ✔ App Router
- ✔ Turbopack (Yes)
- ✔ Import Alias (@/*)
- ✔ React Compiler (Optional: Yes)
```

## 2. Move into Project
```bash
cd my-app
```

## 3. Initialize Git
```bash
git init
```

## 4. Install Dependencies
```bash
pnpm install
```

## 5. Install shadcn/ui
```bash
pnpm dlx shadcn@latest init
```

Choose:
- Style: New York
- Base Color: Neutral
- CSS Variables: Yes

Example:
```bash
pnpm dlx shadcn@latest add button input card dialog form sonner
```

## 6. Install Husky
```bash
pnpm dlx husky-init
pnpm install
```

or (latest)

```bash
pnpm dlx husky init
```

## 7. Add Pre-commit Hook
```bash
echo "pnpm lint" > .husky/pre-commit
```

Make executable (Linux/macOS):
```bash
chmod +x .husky/pre-commit
```

## 8. Run Development Server
```bash
pnpm dev
```

## 9. Build Project
```bash
pnpm build
```

## 10. Start Production
```bash
pnpm start
```

---

# Recommended Additional Packages

```bash
pnpm add axios zod react-hook-form @hookform/resolvers sonner next-themes lucide-react clsx class-variance-authority tailwind-merge
```

Development:

```bash
pnpm add -D prettier prettier-plugin-tailwindcss eslint-config-prettier lint-staged
```

---

# Useful Commands

```bash
pnpm dev
pnpm lint
pnpm build
pnpm start
pnpm add <package>
pnpm add -D <package>
pnpm remove <package>
```