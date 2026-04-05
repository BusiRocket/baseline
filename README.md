# @vibracomet/tsconfig

Shared TypeScript `extends` presets for apps and libraries (Next.js, Astro,
Vite + React, Node).

## Requirements

- Node.js 20+
- TypeScript 5.4+ (align with your project)

## Install

```bash
pnpm add -D @vibracomet/tsconfig@^0.1.0 typescript
```

## Exports

| Subpath          | Use case                          |
| ---------------- | --------------------------------- |
| `./base.json`    | Strict baseline                   |
| `./app.json`     | Browser / app TS                |
| `./nextjs.json`  | Next.js App Router                |
| `./astro.json`   | Astro                             |
| `./vite-react.json` | Vite + React                   |
| `./node.json`    | Node libraries                    |

Example `tsconfig.json`:

```json
{
  "extends": "@vibracomet/tsconfig/nextjs.json",
  "compilerOptions": {
    "paths": { "@/*": ["./src/*"] }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"]
}
```

## Repository

Source and issues: [github.com/VibraComet/tsconfig](https://github.com/VibraComet/tsconfig).

Broader adoption docs: [engineering-baseline](https://github.com/VibraComet/engineering-baseline).
