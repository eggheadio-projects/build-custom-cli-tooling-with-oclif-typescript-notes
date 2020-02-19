# 09. Create Highly Configurable Node.js CLIs with Cosmiconfig and Oclif

## Notes

Cosmiconfig will start where you tell it to start and search up the directory tree:

- a `package.json` property
- a JSON or YAML, extensionless "rc file"
- an "rc file" with the extensions `.json, .yaml, .yml, or .js`.
- a `.config.js` CommonJS module

If your module's name is "myapp", cosmiconfig will search up the directory tree for configuration in the following places:

- a `myapp` property in package.json
- a `.myapprc` file in JSON or YAML format
- a `.myapprc.json` file
- a `.myapprc.yaml`, `.myapprc.yml`, or `.myapprc.js` file
- a `myapp.config.js` file exporting a JS object

Installing:

```bash
yarn add cosmiconfig
```

Result:

```js
const { cosmiconfigSync } = require("cosmiconfig");
const explorerSync = cosmiconfigSync("myfirstcli");
const searchedFor = explorerSync.search();
const loaded = explorerSync.load(pathToConfig);
```

## Personal Take

Comsiconfig is [very configurable](https://github.com/davidtheclark/cosmiconfig#cosmiconfigoptions) - you can modify where it searches and where it stops and how it loads.

## Additional Resources

See the docs for [async search](https://github.com/davidtheclark/cosmiconfig#usage) as well.
