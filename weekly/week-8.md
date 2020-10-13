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

## V. Express Demo
- Demo Code:
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
- The pages we want to serve are being  **controllers/index.js**
  - need `module.exports`
- Start coding **router.js**:
  - this replaces our `switch` statement (or *dispatch table*)
  - `app.get('/',controllers.index);`
  - test it
  - add **page2** & **page3** endpoints
- Add `notFound` handler

```js
res.status(404).sendFile(path.resolve(`${__dirname}/../../views/notFound.html`));

app.get('/*',controllers.notFound); // order matters!
```
 

 

<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-6.md**](week-6.md)  |  [**IGME-430 Home**](../README.md) | [**week-8.md**](week-8.md)
