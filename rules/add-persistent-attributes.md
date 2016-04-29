---
gallery: true
categories:
- enrich profile
summary: By using this rule you can enrich the profile of a user and persist that information in auth0 user store.
---
## Add persistent attributes to the user

This rule count set the default color (an example preference) to a user (using user_metadata`).

```js
function (user, context, callback) {
  user.user_metadata = user.user_metadata || {};
  user.user_metadata.color = user.user_metadata.color || 'blue';

  auth0.users.updateUserMetadata(user.user_id, user.user_metadata)
    .then(function(){
        callback(null, user, context);
    })
    .catch(function(err){
        callback(err);
    });
}
```
