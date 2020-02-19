# 01. Develop and Publish a Node.js CLI from Scratch

## Notes

A minimum viable CLI can be a simple JS file:

```js
#!/usr/bin/env node
console.log("hello world!");
```

\*nix systems also require you to mark these files as executable before you run them:

```shell
chmod +x foo.js   # mark executable
./foo.js          # run the file

```

You can can handle arguments in whatever way you see fit. For example, one of the typical ways is to do it positionally:

- If I want to have the convention that the first argument is the specified directory: `args[0]`
- and to take a name flag by parsing the name flag: `args[1].slice("--name=")[1]`

To publish just use `npm publish` like any other npm project. This includes a run.cmd script that will automatically be used for Windows users.

```shell
$ npm version (major|minor|patch) # bumps version, updates README, adds git tag
$ npm publish
$ npm install -g mynewcli
$ mynewcli
# OR
$ npx mynewcli
```

## Personal Take

Node.js isn't the only language/environment to write CLI's with. It can be slower than Go or Rust. But it has two advantages:

- JS devs will already have it installed, no extra step needed
- Being able to leverage the vast npm ecosystem

## Additional Resources

These are some CLI's with a great developer experience:

- https://github.com/ChristopherBiscardi/gatsby-theme
- https://github.com/netlify/cli/
- https://github.com/plopjs/plop#why-generators
