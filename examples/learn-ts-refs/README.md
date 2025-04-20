Root `tsconfig.json`
 
- List all the projects
- Should also extend the defaults? (nx do it)

```json
{
  "extends": "@total-typescript/tsconfig/tsc/no-dom/app",
  "references": [
    { "path": "./packages/api" },
    { "path": "./packages/front" },
    { "path": "./packages/server" }
  ]
}
```

Each package tsconfig:
```json5
// .tsconfig.src.json
{
  "extends": "@tsconfig/node23/tsconfig.json",
  "compilerOptions": {
    "baseUrl": ".",
    // referenced package need this.
    "composite": true,
    // if "composite" used, this is required
    "rootDir": "src",
    "outDir": "dist",
    // for incremental build. will not re-build if not changed
    // also not the filename, the idea is that since src, test and prod can build diffrently, each has it's own .tsbuildinfo file
    "tsBuildInfoFile": "dist/tsconfig.src.tsbuildinfo"
  },
  "include": [
    "src/**/*.ts"
  ],
  "references": [
    // Refs to other projects
    {
      "path": "../../packages/api"
    }
  ]
}
```

Should run with `npx tsc -b`
- `npx tsc -b server/tsconfig.json` - build server
- `npx tsc -b server` - Shortcut. same.
- `npx tsc -b --watch packages/server packages/front` - watch and build both
- `npx nodemon front/dist/index.js` - Watch (from root)

Resources:
- https://nx.dev/blog/typescript-project-references
- https://www.typescriptlang.org/docs/handbook/project-references.html





