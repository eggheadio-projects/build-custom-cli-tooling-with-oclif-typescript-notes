# 05. Create a Hybrid Single-Multi Command Node.js CLI with Oclif and TypeScript

## Notes

To support multi commands in your CLI:

Go into the bin directory of the oclif command, `packages/mycli/bin/run`.

And check out the `run` file. This is where we actually get some insight into how oclif works with TypeScript under the hood and initializes its commands.

```javascript
#!/usr/bin/env node

const fs = require("fs");
const path = require("path");
const project = path.join(__dirname, "../tsconfig.json");
const dev = fs.existsSync(project);

if (dev) {
  require("ts-node").register({ project });
}

require(`../${dev ? "src" : "lib"}`)
  .run()
  .catch(require("@oclif/errors/handle"));
```

## Personal Take

You can actually have a list of recognized commands, for example `init`, `serve`, and `build`. Then we can put an if block saying that if there's a `process.argv`, if the length is more than two, which means that there is an additional multi-command selected and it's a `recognizedCommand`, then we run the multi-command code.
