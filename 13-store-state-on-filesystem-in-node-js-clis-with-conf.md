# 13. Store State on Filesystem in Node.js CLIs with Conf

## Notes

The Conf library provides an unbelievably easy way to persist values to memory in an XDG compliant fashion.

The standard that everyone has agreed on is [the XDG Spec](https://wiki.archlinux.org/index.php/XDG_Base_Directory), which uses 4 environment variables:

- `XDG_CONFIG_HOME` for user-specific configurations (default `$HOME/.config`)
- `XDG_CACHE_HOME` for user-specific non-essential (cached) data (default `$HOME/.cache`)
- `XDG_DATA_HOME` for user-specific data files (default `$HOME/.local/share`)
- `XDG_RUNTIME_DIR` for temporary, non-essential, user-specific data files such as sockets, named pipes (no default)

How it's used:

```javascript
#!/usr/bin/env node
const { prompt } = require("enquirer");
const fs = require("fs");
const Conf = require("conf");
const config = new Conf();

console.log({ configPath: config.path });

(async function() {
  await prompt({
    type: "input",
    name: "name",
    message: "Where is Harvey Dent?",
    default: config.get("name")
  })
    .then(result => {
      config.set("name", result.name);
      return result;
    })
    .then(console.log)
    .catch(console.error);
})();
```

```javascript
#!/usr/bin/env node
const { prompt } = require("enquirer");
const Conf = require("conf");
const config = new Conf();
const colors = require("ansi-colors");
const presets = [
  "apple",
  "grape",
  "watermelon",
  "cherry",
  "strawberry",
  "lemon",
  "orange"
];
const priorChoices = config.get("choices") || [];
const separator = priorChoices &&
  priorChoices.length && { role: "separator", value: colors.dim("────") };
const choices = [
  ...priorChoices,
  separator,
  ...presets.filter(x => !priorChoices.includes(x))
].filter(Boolean);

(async function() {
  await prompt({
    type: "select",
    name: "color",
    message: "Pick your favorite color",
    choices
  })
    .then(result => {
      config.set("choices", [result.color, ...priorChoices].slice(0, 3));
      return result;
    })
    .then(console.log)
    .catch(console.error);
})();
```

## Personal Take

- Offer to persist state when possible to create defaults
