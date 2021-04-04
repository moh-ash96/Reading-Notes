# EJS
It is a templating language that allows us to generate HTML markup with plain JavScript.
## Get started
* We start with configuring the Node js environment using the comman
```
npm init
```
* then install dependencies using 
```
npm install --save express bode-parser cors ejs
```

* then we define express, cors, body-parser, path, and app.
* set views using 
```
app.set ('views', path.join(_dirname, 'views'));
app.set('view engine', 'ejs');
```
* then we add 
```
app.get('/', (req, res)=>{
    render ('index', {
        we add the variables here (they can be string, array, object or anything)
    })
})
```
* Now we make an index.ejs file and we can access the variable from the server.js so we can render it.
## What we can do in ejs:
We can access the variables inside 'js' file using the tag :
```
<%if we don't want to evaluate the content><%>
and 
<%= if we want to evaluate the content><%>
```
in the ejs we can loop over an object using **for loop** to render its content and also we can use **if statement** to specify what exactly we want.
