---
gallery: true
categories:
- access control
summary: By using this rule you'll be able to whitelist users based on a file in Dropbox.
---
## Whitelist on the cloud

This rule denies/grant access to users based on a list of emails stored in Dropbox.

```js
function (user, context, callback) {
  request.get({
    url: 'https://dl.dropboxusercontent.com/u/21665105/users.txt'
  }, function (err, response, body) {
    var whitelist = body.split('\r\n');

    var userHasAccess = whitelist.some(function (email) {
      return email === user.email;
    });

    if (!userHasAccess) {
      return callback(new UnauthorizedError('Access denied.'));
    }

    callback(null, user, context);
  });
}
```
