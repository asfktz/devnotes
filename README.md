# Dev Notes


Q: How can I achieve consistent dependency versions between packages and applications in a monorepo?

A: Use [Syncpack](https://jamiemason.github.io/syncpack/guide/getting-started/). It helps identify version mismatches, enforce version policies, and fix inconsistencies automatically across your monorepo.

Sources:
[1](https://www.reddit.com/r/webdev/comments/146rzbh/comment/jntjwjs/)
[2](https://turbo.build/repo/docs/crafting-your-repository/managing-dependencies#using-purpose-built-tooling)


Q: When using Syncpack to fix mismatches, it ovverides `workspace:*` with specific verstion number and it breaks installtion.
A: Add `.syncpackrc` file to the root of the project with:
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

Sourcs: [1](https://jamiemason.github.io/syncpack/examples/pnpm-workspace-protocol/#_top)


Q: Kind get Expo to work in a monorepo.
A: add
