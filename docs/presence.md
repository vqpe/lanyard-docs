# Getting User Presence Data

Simply send a GET request to the users endpoint with your `user ID`. This is for the REST API, if you want to get real-time updates instead, check the [WebSocket documentation](#websockets).

> https://api.lanyard.rest/v1/users/{userid}

### JavaScript Code

```js
fetch("https://api.lanyard.rest/v1/users/162969778699501569")
  .then((res) => res.json())
  .then(console.log);
```

### Interactive Playground

The response below is fetched live, edit the user ID and hit Run to try your own.

<div data-playground="lanyard-user" data-user-id="492707412504215552"></div>

<small>Adapted from [lanyard.eggsy.xyz](https://lanyard.eggsy.xyz/api/getting-user-presence).</small>
