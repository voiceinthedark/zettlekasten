# Notes app backend

> Working on a notes app backend

- The extraction of user object into a middleware to be attached to the request pipeline, doesn't seem to work.
  - Probably I should attempt chaining middlewares by extracting the id from the extracted token middleware and verifying the user in the user extraction middleware.
  - It seems that the page request is running before the token extractor even starts!
