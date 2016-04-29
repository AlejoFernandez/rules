---
gallery: true
categories:
- enrich profile
summary: By using this rule you can enrich the profile with the location of the user.
---
## Enrich profile with the locations where the user logs in

This rule gets the user locations based on the IP and is added to the app_metadata in the `geoip` attribute.

```
function (user, context, callback) {

  user.user_metadata = user.user_metadata || {};

  user.user_metadata.geoip = context.request.geoip;

  auth0.users.updateUserMetadata(user.user_id, user.user_metadata)
    .then(function(){
      callback(null, user, context);
    })
    .catch(function(err){
      callback(err);
    });
}
```
