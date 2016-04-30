---
gallery: true
categories:
- access control
summary: By using this rule you'll be able to prevent access during weekends.
---

## Allow Access during weekdays for a specific App

This rule is used to prevent access during weekends for a specific app.

```js
function (user, context, callback) {

  if (context.clientName === 'TheAppToCheckAccessTo') {
    var d = new Date().getDay();

    if (d === 0 || d === 6) {
      return callback(new UnauthorizedError('This app is available during the week'));
    }
  }

  callback(null, user, context);
}
```
