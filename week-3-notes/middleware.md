# Lecture on middleware

## Express Middleware

- if you want to persist cookies between requests, you use an agent so that you can test cookies in your test
- you need next() to let middleware know that it needs to go to the next one
- When next() is invoked with an argument from a controller, the request is forwarded on to the error handling middleware
- contents of a jwt is not encrypted.
- encoded = a known mapping where certain characters match certain encodings, it can be easily decoded
- encrypted = you need a specific key to decrypt
