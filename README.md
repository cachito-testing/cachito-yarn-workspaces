# cachito-yarn-workspaces

Same as <https://github.com/cachito-testing/cachito-npm-workspaces>, but adapted for yarn.

## Differences from npm

1. If package.json does not include the workspaces as dependencies, yarn.lock will not include
   them *at all*.
2. The dependencies can be specified as e.g. `"bar": "^1.0.0"` in package.json, in which
   case yarn.lock will *still not include them*.

This repo tests the following cases (see [package.json](package.json)):

1. A workspace is not specified as a dependency at all (the "eggs" and "spam" workspaces)
2. A workspace is specified as a version ("foo")
3. A workspace is specified as `file:path` and depends on a workspace specified as a version
   ("bar", depends on "not-baz")

Regardless of whether the workspace is specified as a dependency, and whether it's specified
as a version or as a file, Cachito should report it as a `file:` dependency. Cachito should
properly identify the non-dev dependencies of a workspace as non-dev (again, regardless of
whether the workspace is specified as a dependency).
