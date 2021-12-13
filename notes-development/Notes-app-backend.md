# Blogs app backend

> Working on a Blogs app backend

- The extraction of user object into a middleware to be attached to the request pipeline, doesn't seem to work.
  - Probably I should attempt chaining middlewares by extracting the id from the extracted token middleware and verifying the user in the user extraction middleware.
  - It seems that the page request is running before the token extractor even starts!

> I have fixed it!
> The problem was that I was calling one middleware `tokenExtractor` globally, while I was calling the `userExtractor` locally. the solution was to chain them locally instead.

```javascript
// app.use(tokenExtractor);
app.use(requestLogger);
app.use(errorHandler);
// app.use(userExtractor);

app.use('/api/login', tokenExtractor, loginRouter);
app.use('/api/users', usersRouter);
app.use('/api/blogs', tokenExtractor, userExtractor, blogRouter); // Here I am chaining the middleware locally instead of calling them from the global level
```

> The extractors are pretty straight forward

```javascript
const tokenExtractor = async (request, response, next) => {    
        const authorization = await request.get('authorization');
       if (authorization && authorization.toLowerCase().startsWith('bearer ')) {
         request.token = authorization.substring(7);         
       } else{
         request.token = null;
        }
        next();
};

const userExtractor = async (request, response, next) => {    
  if(request.token){
    const decodedToken = jwt.verify(request.token, process.env.SECRET);
    // console.log('decoded: ', decodedToken);
    request.user = await User.findById(decodedToken.id);
    console.log(request.user);
    next();
  } else{
    response.status(403).json({ error: 'no token received' });
  }
};
```

> Few notes to mention

- Applying authentication middleware to local wide router, will break down fetching of data.
  - Better to assign middleware to method-wide requests e.g POST



#javascript, #expressjs, #nodejs, #mongodb, #mongoose, #debug