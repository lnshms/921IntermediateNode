# Chapter 3 Demo: Error handling

## Objectives:
* View default error handling from express a generator

## Steps

1. First, expand the directory called `simple` and open a terminal at this location. Do an `npm install` and `npm start` but do not open browser, lets look at code first.

1. Open `app.js` in the editor. Notice the first line requiring `http-error`. 
    Is this a custom or 3rd party module? How can you find out? Search for the documentation. Scroll down to continue...
    
    ```
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    https://www.npmjs.com/package/http-errors
    ```


    The `create-error` function is what we are using to refer to the package `http-errors`. Open the link for it on npm. 

1. How many downloads per week? Pretty popular package!

    ### 404
1. In `app.js`, look at the next to last middleware with the comment: `catch 404 and forward to error handler`
    
    This catch 404 will only be reached if no other middleware returns with a send or render beforehand. This middleware is used to generate an error, set the status to 404 then it goes the next middleware the error handler. 

    The function `next()` is called with this error. What is the next middleware that runs?

    It is the error handler which is middleware which takes 4 arguments. 
    
    ```javascript
    app.use(function(err, req, res, next) {
    ```    

    What happens in this middleware? Notice how it passed data to the view.

1. In the browser, go to the URL http://localhost:3000

    The page should load with a link to a page that does not exist (no matching route.) 

    ### throwing errors

1. Look in `routes/index.js` and find the route `/throwserror`

    Notice how it calls a function that doesnt exist. This will throw an error so that next() is never called. But Express takes care of this and will also forward on the error handling middleware. Open in the browser, is it picked up by the error handler?

1. Find the `/mtgox` route. This simulates a service not being avaiable by creating a 503 error with a custom message and passing this into next().  Open in the browser, is it picked up by the error handler?

1. Find the `/fileread` route. Notice how it uses an error first call back and calls next passing the err. Load this route in the browser, is it picked up by the error handler?

1. Find the `/filewrite` route. Notice how it uses two callbacks. You can string together as many as you like, these are additional middleware that gets called in order. Notice the difference in the way fs.writeFile is called. next will be called, either with or without the error. If it is with an error, then it gets picked up by the errorhandler. Otherwise a response of OK is returned. Load this route in the browser, is it picked up by the error handler?

