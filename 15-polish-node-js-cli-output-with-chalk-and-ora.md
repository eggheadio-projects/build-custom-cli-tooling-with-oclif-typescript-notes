# 15. Polish Node.js CLI Output with Chalk and Ora

## Notes

CLI output can look extremely unfriendly and confusing. These libraries help create a better experience:

- Chalk
- CLI-UX
- Ora

### Chalk

Library for terminal string styling:

```bash
npm install chalk
```

Example of API:

```js
const chalk = require("chalk");

console.log(chalk.blue("Hello world!"));
```

### CLI-UX

```bash
npm install cli-ux
```

CLI-UX is oclif's first party utility library. It includes prompting, and other cool tools:

- `cli.url(text, uri)`: Create a hyperlink (if supported in the terminal)
- `cli.open`: Open a url in the browser
- `cli.annotation`: Shows an iterm annotation
- `cli.wait`: Waits for 1 second or given milliseconds
- `cli.action`: Shows a spinner
- `cli.table`: Displays tabular data

```js
import { Command } from "@oclif/command";
import { cli } from "cli-ux";
import axios from "axios";

export default class Users extends Command {
  static flags = {
    ...cli.table.flags()
  };

  async run() {
    const { flags } = this.parse(Users);
    const { data: users } = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );

    cli.table(
      users,
      {
        name: {
          minWidth: 7
        },
        company: {
          get: row => row.company && row.company.name
        },
        id: {
          header: "ID",
          extended: true
        }
      },
      {
        printLine: this.log,
        ...flags // parsed flags
      }
    );
  }
}
```

- `cli.tree`: Generate a tree and display it

```
├─ foo
└─ bar
   └─ baz
```

### Ora

Ora is THE spinner library. Much of your CLI time will be spent doing asynchronous tasks.
