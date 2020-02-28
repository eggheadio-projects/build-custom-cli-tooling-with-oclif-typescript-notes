# 11. Spawn and Manage Child Processes and Node.js Streams with execa

## Notes

Add an extra level of power by runnigng multiple concurrent child processes.

Two ways to implement this: with `execa` and with a dedicated `yarn-or-npm` utility.

Node child process API:

```javascript
const { spawn } = require("child_process");
const ls = spawn("ls", ["-lh", "/usr"]); // calling a *nix command and passing args

ls.stdout.on("data", data => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on("data", data => {
  console.error(`stderr: ${data}`);
});

ls.on("close", code => {
  console.log(`child process exited with code ${code}`);
});
```

And for `execa` run:

```
yarn add execa
```

```javascript
const execa = require("execa");

const subprocess = execa("echo", ["foo"]);

subprocess.stdout.pipe(process.stdout);
// or subprocess.all.pipe(process.stdout); // both stdout and stderr
// or subprocess.stdout.pipe(fs.createWriteStream('stdout.txt')) // write to file

// or
// const subprocess = execa(execPath, args, { stdio: 'inherit' }) // pass on all std streams

// close this process when subprocess closes
subprocess.on("close", code => process.exit(code));
subprocess.on("SIGINT", process.exit);
subprocess.on("SIGTERM", process.exit);
```

## Additional Resources

- [List of Node exit codes](https://stackoverflow.com/a/47163396) if you'd like to stick to convention.
