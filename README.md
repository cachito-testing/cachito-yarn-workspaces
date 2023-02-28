# cachito-yarn-workspaces-happy-path

Same as <https://github.com/cachito-testing/cachito-npm-workspaces/>, but adapted for yarn.

## Caveats

1. If package.json does not include the workspaces as dependencies, yarn.lock will not include
   them *at all*.
2. The dependencies can be specified as e.g. `"bar": "^1.0.0"` in package.json, in which
   case yarn.lock will *still not include them*.

The only way to make yarn.lock look the way we expect is to specify all the workspaces
as `file:` dependencies. That's how this repo does it, hence "happy path."

```json
{
  "dependencies": {
    "foo": "file:foo",
    "bar": "file:bar",
    "not-baz": "file:baz",
    "spam": "file:spam-packages/spam",
    "eggs": "file:eggs-packages/eggs"
  }
}
```

If a user doesn't include the workspaces in `dependencies` at all, then:

1. Cachito will not report the workspaces in any metadata.
2. Cachito's algorithm for identifying dev dependencies will currently mis-identify all
   the dependencies of workspace packages as dev dependencies even when they're not dev.

If a user specifies them as `"name": "version"` rather than `"name": "file:path"`, then:

* Same as above, except Cachito currently dies while trying to identify dev dependencies.
  A dependency from package.json doesn't exist in yarn.lock, which goes against everything
  that Cachito believes in.

*Fun fact: running `npm install` with npm v8 produces a much more reasonable-looking
yarn.lock, even when you don't include anything in `dependencies`. The only problem is
that some of the paths are absolute.*
