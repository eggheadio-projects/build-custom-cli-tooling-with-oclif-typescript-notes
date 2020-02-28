# 12. Prompt Users to Update Your Node.js CLIs with Update-Notifier

## Notes

If your users globally install your CLI's, will they ever update them? How will they know about new features and patches? How do you check for updates without impacting performance? How do you respect user preferences to ignore your updates?

These are all solved problems with the wonderful `update-notifier` library.

```
$ npm install update-notifier
```

Example:

```typescript
const updateNotifier = require("update-notifier");
const pkg = require("./package.json");

// Checks for available update and returns an instance
const notifier = updateNotifier({ pkg });

// Notify using the built-in convenience method
notifier.notify();

// `notifier.update` contains some useful info about the update
console.log(notifier.update);
/*
{
	latest: '1.0.1',
	current: '1.0.0',
	type: 'patch', // Possible values: latest, major, minor, patch, prerelease, build
	name: 'pageres'
}
*/
```

The first time the user runs your app, it will check for an update, and even if an update is available, it will wait the specified `updateCheckInterval` before notifying the user.

You probably want to check for updates in a slightly longer interval, for example weekly.

```javascript
const notifier = updateNotifier({
  pkg,
  updateCheckInterval: 1000 * 60 * 60 * 24 * 7 // 1 week
});

if (notifier.update) {
  console.log(`Update available: ${notifier.update.latest}`);
}
```

## Personal Take

- It's a very good thing to include this by default.

## Additional Resources

There are a bunch projects using it. Check how they implement it.

- [npm](https://github.com/npm/npm) - Package manager for JavaScript
- [Yeoman](http://yeoman.io) - Modern workflows for modern webapps
- [AVA](https://ava.li) - Simple concurrent test runner
- [XO](https://github.com/xojs/xo) - JavaScript happiness style linter
- [Pageres](https://github.com/sindresorhus/pageres) - Capture website screenshots
- [Node GH](http://nodegh.io) - GitHub command line tool
