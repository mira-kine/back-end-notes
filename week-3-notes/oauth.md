- A redirect URI, or reply URL, is the location where the authorization server sends the user once the app has been successfully authorized and granted an authorization code or access token

- In your auth.js controller:

1. redirect to GitHub's authorization endpoint
2. in your .get that signed in a user (.get('/login/callback) for example)
   a. get code from query param - const { code } = req.query;
   b. exchange code for token - use npm i cross-fetch (or node-fetch, but we will use cross-fetch because there is no fetch fxn in express rn) - fetch access_token from oauth. Syntax can be const resp = await fetch('url', {
   method: 'POST',
   <!-- header will always be key value pair so it does not need to be stringified -->
   headers: {
   Accept: 'application/json' (we want the app form receive in json),
   'Content-Type': 'application/json' (what we will provide will be in json)
   },
   <!-- turn a javascript object into a string using JSON.stringify, body options are diverse so it has to be stringified -->
   body: JSON.stringify({
   client_id: process.env.CLIENT_ID,
   client_secret: process.env.CLIENT_SECRET,
   code,
   }),
   });
   <!-- here we await the fetch token, and after we receieve it, we will parse -->
   const tokenResp = await resp json();
   c. get the user information from GH using the token
