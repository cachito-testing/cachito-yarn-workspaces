# cachito-npm-workspaces

This repo is for testing the npm workspaces feature in [Cachito](https://github.com/containerbuildsystem/cachito).<br> 
The main package is named npm_test. There are several workspaces defined, each with a single unique dependency.

An example of the commands needed to create the main package and one of the workspaces is:

```
npm init -y
npm init -w foo
npm install abbrev -w foo
npm install
```
Note: The workspaces defined with a relative path and glob pattern required manual edits to package.json


The following test cases are included in this repo:
```
"workspaces": ["package-name"],
"dependencies": {
  "package-name": {
    "version": "file:package-name"
  }
}
"workspaces": ["package-path"],
"dependencies": {
  "package-name-which-is-different-from-package-path": {
    "version": "file:package-path"
  }
}
"workspaces": ["./package-name"],
"dependencies": {
  "package-name": {
    "version": "file:package-name"
  }
}
"workspaces": ["my-packages/package-name"],
"dependencies": {
  "package-name": {
    "version": "file:my-packages/package-name"
  }
}
"workspaces": ["my-packages/*"],
"dependencies": {
  "package-name": {
    "version": "file:my-packages/package-name"
  }
}
```
