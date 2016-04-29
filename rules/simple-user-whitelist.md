---
gallery: true
categories:
- access control
summary: By using this rule you can whitelist users based on their email addresses.
---
## Whitelist

This rule will only allow access to users with specific email addresses.

```js
function (user, context, callback) {
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
