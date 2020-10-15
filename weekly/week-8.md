# Week-8 (10/13/20 & 10/15/20)

## I. Overview 

- In the second part of the course we will learn about the MVC design pattern utilizing Express and React, persisting data with MongoDB, and distributing data with Redis

## II. Software Design Patterns

- What are Design Patterns?
  - Reusable solution to a commonly occuring problem
  - Makes communication between developers easier
  - https://en.wikipedia.org/wiki/Software_design_pattern
  - https://addyosmani.com/resources/essentialjsdesignpatterns/book/
- Presentations/Resources:
  - see the "Week 6.2 HTTP Server Design" video
  - see the accompanying PDF 
- Assignments:
  - See the HTTP Server Design Study Guide Dropbox (it has you research a JavaScript software design pattern and discuss it)

<hr>

## III. Databases
  - Database Management Systems (or DBMS) are applications designed for managing and organizing collections of data
  - Traditional systems typically store *records* (i.e. *rows*) of data in *tables*
    - think "Excel spreadsheet" with rows representing individual records, and columns representing various fields or attributes of each record
    - languages like SQL ("Structured Query Language") - ex. `SELECT {firstName,lastName} FROM Customers WHERE id='11234'` - are used to pull records from the database
  - In this course we will be using MongoDB (and Redis in conjunction with Mongo to create a *distributed* database
    - MongoDB stores its data as *Documents* (sim to "SQL Records") that are contained in *Collections* (sim to "SQL Tables")
      - https://docs.mongodb.com/getting-started/cpp/documents/
      - MongoDB documents are composed of key:value pairs in a format know as BSON ("Binary JSON") - sim to JSON but with more available data types - https://en.wikipedia.org/wiki/BSON
      
   **Mongo Document example**
 
```json
let mydoc = {
    _id: ObjectId("5099803df3f4948bd2f98391"),
    name: { first: "Alan", last: "Turing" },
    birth: new Date('Jun 23, 1912'),
    death: new Date('Jun 07, 1954'),
    contribs: [ "Turing machine", "Turing test", "Turingery" ], views : NumberLong(1250000)
}
```
 
- Presentations/Resources
  - see "Database Study Guide" dropbox, and "Database Study Guide" PDF in Week-7 content section of myCourses
 
<hr>

## IV. MVC with Express

- Express:
  - a web framework for Node
  - https://www.npmjs.com/package/express
  - Static file hosting
  - plugins (like `serve-favicon`, `cookie-parser`, `body-parser`, `compression`)
    - https://www.npmjs.com/package/serve-favicon
    - https://www.npmjs.com/package/cookie-parser
    - https://www.npmjs.com/package/body-parser
    - https://www.npmjs.com/package/compression
    
<hr>

## V. Express Controller Demo
Demo Code:
  - https://github.com/IGM-RichMedia-at-RIT/simple-mvc-views-controllers
  - https://github.com/IGM-RichMedia-at-RIT/simple-mvc-views-controllers-done

Walkthough:
- look at **package.json**
  - start file is **app.js**
  - new app dependencies
- **client** folder
  - has static files
- **src** folder
  - controllers folder
  - **app.js**
  - **router.js**
- **views** folder
  - just static HTML today
- mainly just working with controller code today
- **controllers/index.js**
- look at **app.js**
- Start coding **app.js**:
  - body-parser is going to handle both GET and POST requests for us
  
```js
app.use(bodyParser.urlencoded({extended:true})); // x-www-form-encoded & value=true&number=10

app.set('view engine','handlerbars');
app.set('views',`${__dirname}/../views`);

app.use(favicon(`${__dirname}/../client/img/favicon.png`));

app.use(cookieParser());

router(app);

app.listen(port,(err)=>{
  if(err){
    throw err;
  }
  console.log(`Listening on port ${port}`);
});
```

- test it:
  - `npm i`
  - `npm run nodemon`
  - **localhost:3000/**
  - can't find any pages to serve!
  - it *can* find **http://localhost:3000/assets/img/internet.png** and **http://localhost:3000/assets/img/favicon.png**
- The pages we want to serve are being sent by **controllers/index.js**
  - We need to add a `module.exports` to it
- Start coding **router.js**:
  - this replaces our `switch` statement (or *dispatch table*)
  - `app.get('/',controllers.index);`
  - test it
  - add **page2** & **page3** endpoints
- Add `notFound` handler code to **controllers/index.js** and a `404` route to **router.js**

```js
res.status(404).sendFile(path.resolve(`${__dirname}/../../views/notFound.html`));

app.get('/*',controllers.notFound); // order matters!
```
 
- handling GET requests
  - **/page1** links to a **getName/** endpoint - let's get that working
  - add `getName` to **controllers/index.js**
  - here's the code - `res.json({name}); // creates JSON, sends status code, sends content type, sends the JSON!`
- test the **getName/** endpoint in browser - wow that wasn't much code!
- now let's hook up a `POST` request to enable a **/setName** endpoint
- in **controllers/index.js** - create `setName` with this line of code - `console.dir(req.body);`
- hook up the **/setName** `POST` endpoint in **router.js** 
- test it from the form on **/page2** (recall that we can't do `POST` requests from the browser's address bar)
  - for review, let's also test the endpoint log from the Postman app
- now add the rest of the code:

```js
// handle the error condition first
if(!req.body.firstname || !req.body.lastname){
	return res.status(400).json({error: "firstname and lastname are both required", id:"badRquest"});
}

// if the required params are present, update `name` and send it back
name = `${req.body.firstname} ${req.body.lastname}`;
// return res.status(204).json({name});
return res.json({name});
```

- test it from the form on **/page2** and the Postman app  

<hr>

**Demo Wrap up**
- in this demo, we primarily focused on the *controller* part of MVC:
  - controllers are responsible for controlling the flow of the application execution
  - https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller
  
**What did express do for us?**
- set up a functioning web server with 5 lines of code
- served up static files (images) with one line of code - `app.use('/assets', ...)`
- served up a favicon with one line of code - `app.use(favicon(...))`
- loaded and served up static HTML files with `res.sendFile(...)`
- handled a `POST` request - `setName` - with 5 lines of code

<hr>
 
## VI. MVC - View (Templates with handlebars) Demo

### VI-A. Overview

- MVC - Model View Controller
- Controller handles requests, model stores the data, views handle how to display the data
- Above we covered the controller, today we'll cover the view
- We'll see how to use the templating language handlebars (very similar to the Vue.js templating system) - https://handlebarsjs.com/

<hr>

### VI-B. Demo Code

- https://github.com/IGM-RichMedia-at-RIT/simple-mvc-templates
- https://github.com/IGM-RichMedia-at-RIT/simple-mvc-templates-done

<hr>

### VI-C. Look over start code

- check out **package.json** - the only thing that is new from last time is **express-handlebars**
- **app.js** is mostly the same except:
  - we are importing the `express-handlebars` library - https://www.npmjs.com/package/express-handlebars
  - we are now using `json()` with the `bodyParser` - https://www.npmjs.com/package/body-parser#bodyparserjsonoptions
  - this is in addition to the form parsing we did last time - https://www.npmjs.com/package/body-parser#bodyparserurlencodedoptions
- **router.js** is the same
- **controllers/index.js** - we've ripped out all of the implementations - because the code will be different now that we will be using handlebars to render the view pages (rather than being static HTML files like they were last time)
- the HTML pages in the **views** folder now all have the **.handlebars** extension instead of **.html**

<hr>

### VI-D. Demo
- in **app.js** go ahead and import the `express-handlebars` library - `const expressHandlebars = require('express-handlebars');`
- tell express to load in the handlebars parser:

```js
// load the handlebars engine
app.engine('handlebars',expressHandlebars({
  defaultLayout: '' // NOT using a main.handlebars layout file, which is kind of a "super template"
})); 

app.set('view engine', 'handlebars'); // use the handlebars engine
app.set('views', `${__dirname}/../views`); // tell express where the .handlebars files are
```

- take a look at **index.handlebars**
  - everything inside of the `{{ }}` will be evaluated - variable names will be substituted with text for example - and this happens on the server-side (which is different from Vue)
  - the controller passes the values - for example the `title` - to the view
- head to **controllers/index.js**
- here's the code that renders the index page

```js
const hostIndex = (req, res) => {
  res.render('index',{ // `res.render()` is NEW for us - express knows to look for the index.handlebars file
    title: "Home" 		// the data we want to pass into the template is in an object - in this case `title: "Home"`
  });
};
```

<hr>

**DISCUSSION**
- test it in the browser, **/** should load, with "Home" in the title bar
- "view source" on the browser and you see <title>Home</title> and NOT <title>{{title}}</title>
- This is because the rendering (i.e. replacing `{{title}}` with `Home`)is happening on the *server-side* and thus the browser is never seeing the template, it is instead only seeing the results of the processing
- This means that with handlerbars, the browser does not see the "source code" (i.e. the Handlerbars directives), but instead only sees the results of the processing (i.e. the HTML)
- This is different from Vue.js:
  - With Vue.js, the browser does the processing (i.e. processing the template) on the *client-side* (i.e. the browser), meaning
  - if we "View Source" in the browser on a Vue.js page, we WILL see the template
  - if we "Inspect Element" in the browser on a Vue.js page, we will see only the results of the processing (i.e the HTML)

<hr>

**CONTINUE DEMO**

- Add some more variables to **index.handlebars**

```html
<h1>Welcome to {{pageName}}!</h1>
<p>How are you today {{userName}}?</p>
```

- Test the page is a browser - you can see the new text, but you can't see the variable names, nor can you see any values
- Now head to **controllers/index.js** and fill in some values for `pageName` and `userName`


**TRY THIS:**
- add a `<title>` to  **page1.handlebars** with a `title`, and modify **controllers/index.js** as needed, then test **page1** in browser
 - what happens if I send "extra" variables along?
- now get **page2** working - note that there are no directives (i.e. handlebars) on **page2.handlebars** that need to be rendered

<hr>

**MORE DEMO**
- Get the 404 page working - add the following to **notFound.handlebars** and **controllers/index.js**

```html
<h1>404! The '{{page}}' page could not be found!</h1>

res.status(404).render('notFound',{
  page: req.url,
});
```

- note: to get the image hosting working (we moved the images from where they were last time), head to **app.js** and change `client` to `hosted`

<hr>

**IMPLEMENT `getName`**

- `res.json({name});` // handle GET request

<hr>

**IMPLEMENT `setName`**

```js
// handle POST request
// same as our previous demo
if(!req.body.firstname || !req.body.lastname){
	return res.status(400).json({
		error: 'firstname and lastname are both required',
		id:    'badRequest',
	});
}

name = `${req.body.firstname} ${req.body.lastname}`;
return res.json({name});
```

- test the form on **/page2**, **/getName**, and the home page - you should see that `name` is being set


<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-6.md**](week-6.md)  |  [**IGME-430 Home**](../README.md) | **week-9.md**
