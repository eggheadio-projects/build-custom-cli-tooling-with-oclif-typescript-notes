# 14. Create Node.js CLI's that Intelligently Adapt to Usage with Frecency

## Notes

- Recency biases towards newer entries being more likely to be what you are looking to do.
- Frequency biases towards betting on you doing the same thing you've always done.
- A good example of this is in Slack or other similar interfaces!

## Personal Take

Frecency is made for the browser, so in Node it assumes the localStorage API:

```javascript
const Conf = require("conf");
const path = require("path");
import { LocalStorage } from "node-localstorage";

const config = new Conf();
const storageProviderFrecencyFilePath = path.join(
  path.basedir(config.path),
  "frecency"
);
const storageProvider = new LocalStorage(storageProviderFrecencyFilePath);
const Fruitcency = new Frecency({
  key: "fruits",
  // idAttribute: '_id', // unique identifier, defaults to '_id'
  storageProvider
});
```

Now when your user makes selections:

```js
onSelect: (searchQuery, selectedResult) => {
  // ...
  Fruitcency.save({
    searchQuery, // an object, with _id in it
    selectedId: selectedResult._id
  });
  // ...
};
```

And before you display:

```js
onSearch: (searchQuery) => {
  ...
  // Search results received from a search API.
  const searchResults = [
    { _id: 'Apple'},
    { _id: 'Banana' },
    // ...
  ];

  return Fruitcency.sort({
    searchQuery,
    results: searchResults
  });
```

## Additional Resources

- Plugin to add frecency to search results. Original blog post on Frecency by Slack:
  https://slack.engineering/a-faster-smarter-quick-switcher-77cbc193cb60
