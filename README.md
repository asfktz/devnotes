# Dev Notes


# FAQ

### Q: How can I achieve consistent dependency versions between packages and applications in a monorepo?


A1: Use pnpm catalog: https://pnpm.io/catalogs

A2: Use [Syncpack](https://jamiemason.github.io/syncpack/guide/getting-started/). It helps identify version mismatches, enforce version policies, and fix inconsistencies automatically across your monorepo.

Sources: [1](https://www.reddit.com/r/webdev/comments/146rzbh/comment/jntjwjs/), [2](https://turbo.build/repo/docs/crafting-your-repository/managing-dependencies#using-purpose-built-tooling)

### Q: When using Syncpack to fix mismatches, it overrides `workspace:*` with a specific version number, and it breaks installation.

A: Add a `.syncpackrc` file to the root of the project with:  
```json
{
  "versionGroups": [
    {
      "label": "Use workspace protocol when developing local packages",
      "dependencies": ["$LOCAL"],
      "dependencyTypes": ["dev", "prod"],
      "pinVersion": "workspace:*"
    }
  ]
}
```

Sources: [1](https://jamiemason.github.io/syncpack/examples/pnpm-workspace-protocol/#_top)



### Q: Can't get Expo 52+ to work in a monorepo how to fix?

A: Add a `.npmrc` at the root of the project with:

```
node-linker=hoisted
```


---


# Tools

* [Signia](https://github.com/tldraw/signia) - atom-based state management, powering tldraw

* https://github.com/unsplash/ts-namespace-import-plugin

* [Pake](https://github.com/tw93/Pake) - Turn any webpage into a desktop app with Rust.
* https://animejs.com/



# Effect Resources

Purpose of codegen and built-utils in the effect basic
template

https://discord.com/channels/795981131316985866/1358382812146827326


# TS

Q: Why `console.log` is not recognized with preset `@tsconfig/node23/tsconfig.json`

A: Install: `pnpm add @types/node`



# Monorepo

A New Nx Experience for TypeScript Monorepos and Beyond
https://nx.dev/blog/new-nx-experience-for-typescript-monorepos



# Nx
Q: How to remove the need for `.js` in imports?

In `tsconfig.base.json`, replace 
```json
{
    "module": "nodenext",
    "moduleResolution": "nodenext"
}
```

with:
```json
{
    "module": "esnext",
    "moduleResolution": "bundler"
}
```
Source: https://discord.com/channels/1143497901675401286/1143540600252153946/1359111402354118706

Q: When trying to serve an app generated with @nx/node:app
I get:
```
Error [ERR_REQUIRE_ESM]: require() of ES Module /Users/asfktz/dev/project/packages/api/dist/index.js from /Users/asfktz/dev/project/apps/server-app/dist/apps/server-app/src/main.js not supported.
Instead change the require of index.js in /Users/asfktz/dev/project/apps/server-app/dist/apps/server-app/src/main.js to a dynamic import() which is available in all CommonJS modules.
    at Module._load (/Users/asfktz/dev/project/node_modules/@nx/js/src/executors/node/node-with-require-overrides.js:15:31)
    at Object.<anonymous> (/Users/asfktz/dev/project/apps/server-app/dist/apps/server-app/src/main.js:2:18)
```

A: In the app's `package.json`, change:
`nx -> targets -> options`

From:
```json5
{
  "format": ["cjs"],
  "bundle": false,
}
```
To:
```json5
{
  "format": ["esm"],
  "bundle": true,
}
```
