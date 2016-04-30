---
gallery: true
categories:
- enrich profile
summary: By using this rule you can enrich the profile with information from rapLeaf.
---
## Enrich profile with Rapleaf

This rule gets user information from __rapleaf__ using the e-mail (if available). If the information is immediately available (signaled by a `statusCode=200`), it adds a new property `rapLeafInfo` to the user profile and returns. Any other conditions are ignored. See [RapLeaf docs](http://www.rapleaf.com/developers/personalization-api/) for full details.

```
function (user, context, callback) {

  //Filter by app
  //if(context.clientName !== 'AN APP') return callback(null, user, context);

  var rapLeafAPIKey = 'YOUR RAPLEAF API KEY';

  if(user.email){
    return callback(null, user, context);
  }

  request({
    url: 'https://personalize.rapleaf.com/v4/dr',
    qs: {
      email: user.email,
      api_key: rapLeafAPIKey
    }
  }, function(err, response, body){
    if(err) return callback(err);

    if(response.statusCode===200){
     user.rapLeafData = JSON.parse(body);
    }

    return callback(null, user, context);
  });

}
```
