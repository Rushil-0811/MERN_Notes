
express notes

nodemon is important, easier to make changes as it restarts the server.

const express = require('express')
const app = express()

app.listen(3000)- app is listening on port 3000

To setup different routes, we define routes using something like app.get('./', (req, res, next)=>{
console.log('here')
res.send('HI')
})

for http methods, first parameter is the path, second parameter is a function which takes 3 parameters, request, response and the next function. 
next is not often used, req, and res are important.
send is used for testing only.
sendStatus is better, can pass http status codes in this, refer status codes but u know this stuff man.
res.status(500).send('hi')
can chain statuses like this.
can pass json using 
res.status(500).json({message:"error"})
res.download(server.js)- can mkake the user download a file.
we either send down json or render a file.
res.render("index", {})- first parameter is the file u wanna render, second parameter is an object
to render stuff we need to use a view enginer, ejs and pug are good for this.

app.set('view engine', "ejs")

to access ejs we do it like this - Hello <%= locals.text %>, this will help access the object data ementioned in res.render.

Routers are kinda like mini applications that run in the main application, u define routers.

app.get('/users', (req,res)=>{
res.send("users")
})

app.get('/users/new', (req,res)=>{
res.send("uers form")
})

we put these routes in its own file so that it is all encapsulated.
and then import that to the main rendering file.
create routes folder, create user file in the routes folder.
const router = express.Router()

replace tyhe app call with router,
router.get('/users', (req,res)=>{
res.send("users")
})

router.get('/users/new', (req,res)=>{
res.send("uers form")
})

everything related to the users call can be done by calling the users route, so we wont hacve to define every route as /users,
we can simply define it thru /, whihc inthis case will efer to /users. EXAMPLE BELOW, anything that starts with /users, 

in the main app.jsx
const userRouter= require('./routes/users')
app.use('/users', userRouter)

you can nest the routes like shown above.

router.post('/', (req,res)=>{

})

to create a dynamic parameter, start with a colon
router.get('/:id', (req,res)=>{
req.params.id
res.send("get user with ID ${req.params.id}")
})

everything in express goes from top to bottom, it reads line by line in order, so static routes to be defined above the dynamic routes.

you can chain all your http requests via this .route function, u cn chain usiong .get, .post, .put
router
.route(":/id")
.get((req,res)=>{

})
.post((req,res)=>{
})
.put((req,res)=>{
})

this chaining just makes the code cleaner.

when next is called it tells that when the code that is defined in the function runs, run this thing next
param is a type of middleware which runs when the request is sent and before getting the response
.param is a function which is pretty useful.
router.param("id", (req,res,next,id)=>{
console.log('id')
next(), without next this would be stuck in an infinite loop
})

every piece of middlware takes up req,res and next, next is aminly used when creating middleware
middleware should be defined aqtr top as express runs from top to bottom.

u can call middleware before the req,res function, to dcalkl middlware only to individual routes/endpoints.

router.get('/new', logger, (req,res)=>{})

there are pre defined middleware in express as well, static html, etc.

