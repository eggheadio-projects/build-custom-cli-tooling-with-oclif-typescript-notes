# 08. Design Beautiful, Intuitive and Secure Node.js CLI User Input Experiences with Enquirer

## Notes

[Enquirer](https://github.com/enquirer/enquirer) is a great foundation to build Interactive CLIs that don't leak tokens and passwords.

These are the [built in prompts](https://www.npmjs.com/package/enquirer#built-in-prompts) you get:

- [AutoComplete Prompt](https://github.com/enquirer/enquirer#autocomplete-prompt)
- [BasicAuth Prompt](https://github.com/enquirer/enquirer#basicauth-prompt)
- [Confirm Prompt](https://github.com/enquirer/enquirer#confirm-prompt)
- [Form Prompt](https://github.com/enquirer/enquirer#form-prompt)
- [Input Prompt](https://github.com/enquirer/enquirer#input-prompt)
- [Invisible Prompt](https://github.com/enquirer/enquirer#invisible-prompt)
- [List Prompt](https://github.com/enquirer/enquirer#list-prompt)
- [MultiSelect Prompt](https://github.com/enquirer/enquirer#multiselect-prompt)
- [Numeral Prompt](https://github.com/enquirer/enquirer#numeral-prompt)
- [Password Prompt](https://github.com/enquirer/enquirer#password-prompt)
- [Quiz Prompt](https://github.com/enquirer/enquirer#quiz-prompt)
- [Survey Prompt](https://github.com/enquirer/enquirer#survey-prompt)
- [Scale Prompt](https://github.com/enquirer/enquirer#scale-prompt)
- [Select Prompt](https://github.com/enquirer/enquirer#select-prompt)
- [Sort Prompt](https://github.com/enquirer/enquirer#sort-prompt)
- [Snippet Prompt](https://github.com/enquirer/enquirer#snippet-prompt)
- [Toggle Prompt](https://github.com/enquirer/enquirer#toggle-prompt)

Installing:

```bash
yarn add enquirer
```

A basic enquirer prompt looks like this:

```js
const { prompt } = require("enquirer");

// assuming you are in an async block
const response = await prompt({
  type: "input",
  name: "username",
  message: "What is your username?"
});

console.log(response); // { username: 'jonschlinkert' }
```

Once you're familiar with the [prompt options API](https://github.com/enquirer/enquirer#prompt-options) you can use them pretty much everywhere:

```js
{
  // required
  type: string | function,
  name: string | function,
  message: string | function | async function,

  // optional
  initial: string | function | async function, // The default value to return if the user does not supply a value.
  format: function | async function, // Function to format user input in the terminal.
  result: function | async function, // Function to format the final submitted value before it's returned.
  validate: function | async function, // Function to validate the submitted value before it's returned. This function may return a boolean or a string. If a string is returned it will be used as the validation error message.

  // each command will also recognize additional options
  // e.g. `limit`, `choices`, `hint`, `fields`
}
```

Adding AutoComplete prompt:

```js
const { prompt } = require("enquirer");

// inside async block
const response = await prompt({
  type: "autocomplete",
  name: "flavor",
  message: "Pick your favorite flavor",
  limit: 10,
  choices: [
    "Almond",
    "Apple",
    "Banana",
    "Blackberry",
    "Blueberry",
    "Cherry",
    "Chocolate",
    "Cinnamon",
    "Coconut",
    "Cranberry",
    "Grape",
    "Nougat",
    "Orange",
    "Pear",
    "Pineapple",
    "Raspberry",
    "Strawberry",
    "Vanilla",
    "Watermelon",
    "Wintergreen"
  ]
});
```

## Personal Take

Principles to help your CLI be CI friendly:

- Every prompt should have a corresponding flag that skips the prompt
- Every prompt should inform the user about what flag they can use to skip the prompt (nice to have)
