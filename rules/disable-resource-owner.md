---
gallery: true
categories:
- access control
summary: By using this rule you'll be able to disable the Resource Owner endpoint.
---

## Disable the Resource Owner endpoint

This rule is used to disable the Resource Owner endpoint (to prevent users from bypassing MFA policies).

```js
function (user, context, callback) {
  if (context.protocol === 'oauth2-resource-owner') {
    return callback(
      new UnauthorizedError('The resource owner endpoint cannot be used.'));
  }
  callback(null, user, context);
}
```
