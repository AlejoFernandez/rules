---
gallery: true
categories:
- access control
summary: By using this rule you'll be able to map scope values to properties.
---

# Custom authorization scopes

This rule maps arbitrary `scope` values to actual properties in the user profile.

```js
function (user, context, callback) {
  // The currently requested scopes can be accessed as follows:
  // context.request.query.scope.match(/\S+/g)
  var scopeMapping = {
    contactInfo: ["name", "email", "company"],
    publicInfo: ["public_repos", "public_gists"]
  };
  context.jwtConfiguration.scopes = scopeMapping;
  callback(null, user, context);
}
```
