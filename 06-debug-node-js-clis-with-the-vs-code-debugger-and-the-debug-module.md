# 06. Debug Node.js CLIs with the VS Code Debugger and the Debug module

## Notes

- If you're looking for performance issues rather than code errors, you'll want a robust logging solution. The debug module is best in class and is built into Oclif.

- The CLI uses this module for all of its debugging. If you set the environment variable `DEBUG=\*` it will print all the debug output to the screen.

- Depending on your shell you may need to escape this with `DEBUG=\*.` On Windows you can't set environment variables in line, so you'll need to run set `DEBUG=\*` before running the command.

For example, I can place a break point inside of this run file.

```typescript
const recognizedCommands = ["init", "serve", "build"];
if (process.argv.length > 2 && recognizedCommands.includes(process.argv[2])) {
  require(`../${dev ? "src" : "lib"}`) // break point here
    .run()
    .catch(require("@oclif/errors/handle"));
} else {
  require(`../${dev ? "src" : "lib"}/commands/init`)
    .run()
    .catch(require("@oclif/errors/handle"));
}
```

Running code:

```bash
node --inspect-brk ./bin/run init
```

## Personal Take

- Always test on Windows/Linux OClif provides debug logging by default.
- Log levels help filter for the thing you’re looking for by using a regex.
