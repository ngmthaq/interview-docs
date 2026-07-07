# 4. What is npm and package.json? (Fresher)

**npm** (Node Package Manager) installs and manages third-party libraries. **`package.json`** is the manifest describing your project and its dependencies.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "start": "node index.js",
    "test": "vitest"
  },
  "dependencies": {
    "express": "^4.19.0"
  },
  "devDependencies": {
    "typescript": "^5.4.0"
  }
}
```

**Key concepts:**

- **`dependencies`** ship to production; **`devDependencies`** are for build/test only (`npm i -D`).
- **`scripts`** are run with `npm run <name>` (`start`/`test` need no `run`).
- **`package-lock.json`** pins exact resolved versions for reproducible installs.
- **Semver ranges:** `^1.2.3` allows minor updates, `~1.2.3` only patches, `1.2.3` is exact.

**Key point:** `package.json` declares metadata, scripts, and dependency ranges; `package-lock.json` locks the exact tree so every install is identical.
