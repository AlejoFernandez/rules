---
gallery: true
categories:
- webhook
summary: By using this rule you can send an email to an administrator on the first login using Mandrill.
---
# Send email with Mandrill

This rule will send an email to an administrator on a user's first login. We use a persistent `signedUp` property to track whether this is the case or not. This rule assumes you've stored a secure value named `MANDRILL_API_KEY`, which contains your secret API key for Mandrill. It is sent in each request.

In the same way, other services such as [Amazon SES](http://docs.aws.amazon.com/ses/latest/APIReference/Welcome.html) and [SendGrid](sendgrid.md) can be used.

Make sure to change the sender and destination emails.

```js
function (user, context, callback) {
  user.app_metadata = user.app_metadata || {};
  // Only send an email when user signs up
  if (!user.app_metadata.signedUp) {
    // See https://mandrillapp.com/api/docs/messages.JSON.html#method=send
    var body = {
      key: configuration.MANDRILL_API_KEY,
      message: {
        subject: 'User ' + user.name + ' signed up to ' + context.clientName,
        text: 'Sent from an Auth0 rule',
        from_email: 'SENDER_EMAIL@example.com',
        from_name: 'Auth0 Rule',
        to: [
          {
            email: 'DESTINATION_EMAIL@example.com',
            type: 'to'
          }
        ],
      }
    };
    var mandrill_send_endpoint = 'https://mandrillapp.com/api/1.0/messages/send.json';

    request.post({url: mandrill_send_endpoint, form: body}, function (err, resp, body) {
      if (err) { return callback(err); }
      user.app_metadata.signedUp = true;
      auth0.users.updateAppMetadata(user.user_id, user.app_metadata)
        .then(function(){
          callback(null, user, context);
        })
        .catch(function(err){
          callback(err);
        });
    });
  } else {
    // User had already logged in before, do nothing
    callback(null, user, context);
  }
}
```
