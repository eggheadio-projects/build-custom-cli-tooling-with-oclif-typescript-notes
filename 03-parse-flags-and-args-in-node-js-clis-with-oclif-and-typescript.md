# 03. Parse Flags and Args in Node.js CLIs with Oclif and TypeScript

## Notes

- Flag options are non-positional arguments passed to the command.
- Flags can either be option flags which take an argument, or boolean flags which do not. An option flag must have an argument.
- For larger CLIs, it can be useful to declare a custom flag that can be shared amongst multiple commands.

**Arguments** are positional arguments passed to the command.

For example, if this command was run with `mycli arg1 arg2` it would be declared like this:

```js
import Command from '@oclif/command'

export class MyCLI extends Command {
  static args = [
    {name: 'firstArg'},
    {name: 'secondArg'},
  ]

  async run() {
    // can get args as an object
    const {args} = this.parse(MyCLI)
    console.log(`running my command with args: ${args.firstArg}, ${args.secondArg}`)
    // can also get the args as an array
    const {argv} = this.parse(MyCLI)
    console.log(`running my command with args: ${argv[0]}, ${argv[1]}`)

```

Oclif comes with some best practice flag parsing built in:

```js
static flags = {
  name: flags.string({
    char: 'n',                    // shorter flag version
    description: 'name to print', // help description for flag
    env: 'MY_NAME',               // default to value of environment variable
    options: ['a', 'b'],          // only allow the value to be from a discrete set
    parse: input => 'output',     // instead of the user input, return a different value
    default: 'world',             // default value if flag not passed (can be a function that returns a string or undefined)
    required: false,              // make flag required (this is not common and you should probably use an argument instead)
    dependsOn: ['extra-flag'],    // this flag requires another flag
    exclusive: ['extra-flag'],    // this flag cannot be specified alongside this other flag
  }),

  // flag with no value (-f, --force)
  force: flags.boolean({
    char: 'f',
    default: true,                // default value if flag not passed (can be a function that returns a boolean)
    // boolean flags may be reversed with `--no-` (in this case: `--no-force`).
    // The flag will be set to false if reversed. This functionality
    // is disabled by default, to enable it:
    // allowNo: true
  }),
}

```

## Personal Take

- Multiple arguments are fine but when they are different types, that's when you get into issues.
- A good rule of thumb: is 1 type of argument is fine, 2 types are very suspect, and 3 are never good.

## Additional Resources

- [Command Flags](https://oclif.io/docs/args)
- [Command Arguments](https://oclif.io/docs/args])
- [CLI Flags in Practice + How to Make Your Own CLI Command with oclif](https://blog.heroku.com/cli-flags-get-started-with-oclif)
