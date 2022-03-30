- A redirect URI, or reply URL, is the location where the authorization server sends the user once the app has been successfully authorized and granted an authorization code or access token

- In your auth.js controller:

1. redirect to GitHub's authorization endpoint
2. in your .get that signed in a user (.get('/login/callback) for example)
   a. get code from query param

   - const { code } = req.query;
     b. exchange code for token
   - use npm i cross-fetch (or node-fetch, but we will use cross-fetch because there is no fetch fxn in express rn)
   - fetch access_token from oauth. Syntax can be const resp = await fetch('url', {
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
   - use the access token to access the API that allows you to make requests to the API on behalf of the user
   - const profileResp = await fetch('https://api.github.com/user', {
     headers: {
     Authorization: `token ${access_token}`
     },
     });

     const { avatar_url, login } = await profileResp.json();
     d. create (or fetch a user in our database using the GH username)
     let user = await User.findByUsername(login);
     <!-- check if there is a user, if not then create a new one -->

     if(!user) {
     user = await User.insert({ username: login, photoUrl: avatar_url })
     }
     <!-- create the jwt =  -->
     <!-- httpOnly means you only want it on your server -->

     res.cookie(process.env.COOKIE_NAME, sign(user), {httpOnly: true, maxAge: ONE_DAY_IN_MS} );
     })
     const profileJson = await profileResp.json();
     res.send(profileJson);

3. move your responses out into github utils file -> instead of service because it doesn't have anything to do with the model. There's no state being saved or antyhing important other than a long function to fetch the api
4. move those newly refactored controller into the UserService services because the controller is only supposed to deal with routes, no other logic

- middleware is what you will do with every request and certain endpoint -> it will always run during a request as part of the life cycle

- services = multiple pieces of functionality that you can use when you want
