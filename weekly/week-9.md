# Week-9 (10/20/20 & 10/22/20)

## I. Overview 
- This week we learn how to add MongoDB support to an app (via Mongoose)
- The start code is here:
  - https://github.com/IGM-RichMedia-at-RIT/Simple-MVC-Example
  - be sure to FORK it, and then CLONE it to your dekstop - `git clone <url>`
- The complete video of this demo is here - https://www.youtube.com/watch?v=2DgCCVpRRbM
- The "running on heroku" version is here - https://simple-mvc-example-done-2201.herokuapp.com/
- The completed demo code (which is the start file for the Homework - "Simple Models Exercise" is here - https://github.com/IGM-RichMedia-at-RIT/simple-mvc-example-done

## II. Walkthrough

### II-A. Look over code

**package.json**
- `mongoose` is new

**app.js**
- has some mongoose stuff

- Docs for mongoose: https://mongoosejs.com/
- With mongoose, we need to create a **schema** for our data:
  - https://mongoosejs.com/docs/guide.html
  - each schema maps to a MongoDB collection and defines the "shape" of the documents within that collection
- Models:
  - https://mongoosejs.com/docs/models.html

### II-B. Work on *models/Cat.js*
- create cat *schema*
- create cat *model*
- export them
- what's a *schema* again?

```js
const mongoose = require('mongoose');

let CatModel;

// name the "fields" of Cat
// give them a type
// see here for schemea types: https://mongoosejs.com/docs/guide.html
const CatSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    trim: true,
    unique: true,
  },
  bedsOwned: {
    type: Number,
    min: 0,
    required: true,
  },
  createdDate: {
    type: Date,
    default: Date.now,
  },
});

// schemas can have functions
// static functions

// the cat's name is a unique value - therefor it is the *primary key* of the `Cat`
CatSchema.statics.findByName = (name, callback) => {
  const search = {
    name,
  };
  // findOne() is built into mongoose
  // https://mongoosejs.com/docs/api.html
  return CatModel.findOne(search, callback);
};

CatModel = mongoose.model('Cat', CatSchema);

module.exports = { CatModel, CatSchema };
```


### II-C. Work on *controllers/index.js*

- "cat" info has already been imported
- look over what the functions do


#### II-C-i. Create our first `Cat` model

- handy shortcut to `Cat`

```js
const Cat = models.Cat.CatModel;`
```

- Make default `Cat` model instance

```js
let lastAdded = new Cat(defaultData); // creating a Cat - this creates a Mongoose object
console.dir(lastAdded);
```

- `createdDate` will be populated when we actually put it in the DB
- note `_id` - which is a [*guid*](https://en.wikipedia.org/wiki/Universally_unique_identifier)  - a unique identifier for the document

### II-D. Head to *controllers/index.js*

#### II-D-i. Complete */* & */getName* endpoints

```js
const hostIndex = (req, res) => {
	// render the handlebars template
  res.render('index',{
    currentName: lastAdded.name,
    title: 'Home',
    pageName: 'Home Page',
  });
};
```

```js
const getName = (req, res) => {
  // get name of most recently created cat
  // watch what ESLint (when we run npm run test) does to this code
  return res.json({name: lastAdded.name});
};
```

- go test these in the server

#### II-D-ii. Implement `readAllCats()`

```js
const readAllCats = (req, res, callback) => {
  // get all cats
  // https://mongoosejs.com/docs/api.html#model_Model.find
  // without a filter object parameter I get every Cat document back
  // if there are no cats I get back an empty array
  // .lean() gives me just the Mongo document(s) and filters out all other mongoose stuff
  Cat.find(callback).lean(); 
};
```

#### II-D-ii. `readCat()`

- this returns a single cat of a particular name

```js
const readCat = (req, res) => {
 // get 1 cat
 const name1 = req.query.name;
 
 // "error first" style
 // mongoose will return either an error, or a Document (i.e. a result)
 const callback = (err,doc) => {
  if(err){
    return res.status(500).json({err}); // in a production env we would not send back the entire error message
  }
  return res.json(doc);
 };
 Cat.findByName(name1,callback); // see CatSchema.statics.findByName in Cat.j
};
```

### II-E. Implement `hostPage1()`

- this uses **page1.handlebars** - it is going to display all of the cat objects
- it uses `readAllCats()`

```js
const hostPage1 = (req, res) => {
  // "error first" style again
   // mongoose will return either an error, or an *array* of Documents, which we call `docs` this time
  const callback = (err,docs) => {
    if(err){
      return res.status(500).json({err}); // in a production env we would not send back the entire error message
    }

    return res.render('page1',{cats: docs})
  };

  readAllCats(req,res,callback);
};
```

### II-F. Test **/page1**
- Head to the command line and insert a Cat into the Cat collection
- Head to **/page1** to see the cat, and to **/** to see last added

```js
db.cats.insert({name: "Kitty",bedsOwned: 10, createdDate: Date()})
```


### II-G. Implement `setName()`

```js
const setName = (req, res) => {
  if (!req.body.firstname || !req.body.lastname || !req.body.beds) {
    return res.status(400).json({ error: 'firstname,lastname and beds are all required' });
  }
  // create new cat
  const name = `${req.body.firstname} ${req.body.lastname}`;
  const cataData = {
    name,
    bedsOwned: req.body.beds
  };

  const newCat = new Cat(cataData);
  const savePromise = newCat.save();

  savePromise.then(() => {
    lastAdded = newCat;
    res.json({
      name: lastAdded.name,
      beds: lastAdded.bedsOwned,
    });
  });

  savePromise.catch((err) => {
    res.status(500).json({err});
  });
  
  return res; // to keep ESLint happy
};
```



- test by heading to **/page2** to create a cat, and then:
  - check DB - `db.cats.find().pretty()`
  - **/** - last added cat's name
  - **/page1** - 


## Implement `searchName()`

```js
const searchName = (req, res) => {
  if (!req.query.name) {
    return res.status(400).json({ error: 'Name is required to perform a search' });
  }

  return Cat.findByName(req.query.name,(err,doc) => {
    if(err){
      return res.status(500).json({err});
    }

    // When there are no matches findOne() returns null!
    if(!doc){
      return res.json({'error':'No cats found!'})
    }

    return res.json({
      name: doc.name,
      beds: doc.bedsOwned,
    });
  });
};
```

- test it from **/page2** by searching for a cat




## Implement `updateLast()`

```js
const updateLast = (req, res) => {
  // update lastAdded Cat
  lastAdded.bedsOwned++;

  // save the changes to mongo
  // mongo uses the `_id` of the Cat to save the updates
  const savePromise = lastAdded.save();
  savePromise.then(() => {
    // return the updated Cat if successful
    res.json({
      name: lastAdded.name,
      beds: lastAdded.bedsOwned,
    });
  });

  // // return an error message if not successful
  savePromise.catch((err) => {
    res.status(500).json({ err });
  });
};
```



<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-8.md**](week-8.md)  |  [**IGME-430 Home**](../README.md) | **week-10.md**(week-10.md)
