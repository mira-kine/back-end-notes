# Lecture on O-Auth

## Auth Flow

- Signing In: 0. User submits sign in form

  1. API checks the data base to see if that user exists
  2. If the user exists, the API compares the hashed password from the database with the hashed password sent in the user's request
  3. If user exists and hashed passwords match, API sends success response and attaches a cookie to be stored in the user's browser
  4. User makes a request to the API, sending the cookie along with it
  5. API gets the request with the cookie, grabs the cookie's value (which is a JSON Web Token) and verifies its contents. If the cookie valid, the API stores the user object on the 'req' object, then continues fulfilling the request

- JSON Web Token is the first amount of encoded data. Second part is the payload, which is the data stored in the JSON Web Token
- bcrypt = a way to hash passwords

## Using jwt.io to see what header, payload, and verify signature is visible

- jwt.sign(payload, secretOrPrivateKey)
- that key will be compared to signature in order to verify signature
- const payload jwt.verify(token, 'top_secret_jwt-secret'); -> this is comparing to verify the signature
- app.use(express.json()) is what gives us access to req.body (it is the built in middleware)
- middleware = in the middle of the request response life cycle
- "next" is what sends it on the next piece of middleware
- make something private using #

## TDD for sign up

1. Write test of user object you will get back (without password in the expected)
2. controller that sends in user object
3. Model that inserts it into User table
4. Service -> where you will deal with hashing the pw and will create user (because remember controller ONLY deals with api request, not with the logic of it)

## TDD for sign in

- check for existing user
- if user exists, compare hashed password
- if passwords match, return user

- get passwordHash() to return this.#passwordHash is done to return the hashed password as necessary to compare (after you check for whether the user exists)

## cookie parser

- app.use(cookieParser()) -> req.cookies/res.cookie
- to use this in our auth controller, you can set it up directly in your response by doing res.cookie('session', token) -> you can name it what you want. This way you are setting the value of the cookie to the token
- bring in the jwt by using const token = jwt.sign(user, process.env.JWT_SECRET, { expiresIn: '1 day'}) -> put the JWT secrets and salt rounds into your .env file
- authToken() {
  return jwt.sign({...user}, process.env.JWT_SECRET, { expiresIn: '1 day' }) -> because you are referencing your currently signed in user
  }

## Ensure that you are logged in

- in the .get method of user, you want to get the value of the cookie (jwt)
- cookies are for sending and storing arbitrary data, whereas bearer tokens are specifically for sending authorization data, often encoded as a JWT
  1. get value from cookie: const { session } = req.cookies
  2. verify the jwt: const payload = jwt.verify(session, process.env.JWT_SECRET)
  3. send the payload back up/send the contents of jwt up as a response (res.send(payload))
- agent essentially creates a cookie jar for these requests to store the cookies from your previous requests. Set this up by doing const agent = request.agent(app)
- jwt is going to return an expired at time (exp) and issued at time (iat). You can se these to expect.any(Number)

--> send this out to another middleware file ie: authenticate.js because this is where the use rmakes a request to the API sending a cookie along with it (in the subsequent requests step after you have signed in the first time)

- const ONE_DAY_IN_MS = (1000 _ 60 _ 60 \* 24) -> is what you use for maxAge in your cookie method
- /me end points -> as soon as your react app loads, it can hit this endpoint which lets the react app know if you are signed in already or not

## TDD protecting routes using authenticate middleware

- Create an agent for storing cookies on the requests in this test
- Create a user to sign in with
- Try hitting the protected endpoint to ensure it's indeed protected
- Then, sign in and make the same request
- with a message that says 'Top secret you should only see if you are logged in' for ex.
