---
gallery: true
categories:
- access control
summary: By using this rule you can whitelist users based on their usernames.
---
## Whitelist for a Specific App

This rule will only allow access to users with specific email addresses on a specific app.

```js
function (user, context, callback) {
    //we just care about NameOfTheAppWithWhiteList
    //bypass this rule for every other app
    if(context.clientName !== 'NameOfTheAppWithWhiteList'){
      return callback(null, user, context);
    }

    var whitelist = [ 'user1@mail.com', 'user2@mail.com' ]; //authorized users
    var userHasAccess = whitelist.some(
      function (email) {
        return email === user.email;
      });

    if (!userHasAccess) {
      return callback(new UnauthorizedError('Access denied.'));
    }

    callback(null, user, context);
}
```
