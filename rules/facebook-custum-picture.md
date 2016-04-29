---
gallery: true
categories:
- enrich profile
summary: By using this rule you can enrich the profile with facebook profile picture.
---
## Use a custom sized profile picture for Facebook connections

This rule will set the `picture` to a custom size for users who login with Facebook.

```js
function (user, context, callback) {
  if (context.connection === 'facebook') {
    var fbIdentity = _.find(user.identities, { connection: 'facebook' });
    // See: https://developers.facebook.com/docs/graph-api/reference/user/picture/ for more
    // sizes and types of images that can be returned
    var pictureType = 'large';
    user.picture = 'https://graph.facebook.com/v2.5/' + fbIdentity.user_id + '/picture?type=' + pictureType;
  }
  callback(null, user, context);
}
```
