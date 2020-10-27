# Week-10 (10/27/20 & 10/29/20)

## I. Overview 

- React MVC Project Overview
  - [Project 2 - Product/Service Site - React](https://people.rit.edu/arwigm/430/)
  - Videos:
    - [Rich Media 2 - Week 12.1 - React MVC Project Overview](https://www.youtube.com/watch?v=Kl1II4VpgOE)
    - [Rich Media 2 - Week 11.1 - React FSCs](https://www.youtube.com/watch?v=kAMb0sEp9js) - *Functional Stateless Components*
    - [Rich Media 2 - Week 11.2 - React Class Components](https://www.youtube.com/watch?v=EzgxSVN-AzI)
  - DomoMakers (see myCourses for PDFs and due dates):
    - [DomoMaker A Done](https://domomaker-a-2201.herokuapp.com)

## II. DomoMaker A - Assignment Walkthrough

- The architecture of this app is very similar to the *Simple Models* HW
  - **app.js** to load the app dependencies and start up the [express](https://www.npmjs.com/package/express) server
  - **router.js** to call the various routes with code defined in the **controllers/** folder
  - a **views/** folder containing handlebars templates of the site's three pages (**app**, **signup**, **login**)
  - a **models/** folder that contains mongoose models (one per file) such as **Account**
- Note: the **client.js** code is all [jQuery](https://jquery.com/):
  - why? `jQuery.animate()` I guess ...
  - here's a nice overview - [jQuery Fundamentals - jquery Basics](http://jqfundamentals.com/chapter/jquery-basics)
- Create a user account with **signup.handlebars**
  - `<input id="pass" type="password" name="pass" placeholder="password"/>`
  - note that the `type` is [`"password"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/password)
  - **models/Account.js** is a mongoose model for the user's account
    - properties are `username`,`salt`,`password` (encrypted), `createdDate`
    - we encrypt the typed in password with node's built-in **crypto** library:
      - https://nodejs.org/api/crypto.html#crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback
      - https://nodejs.org/api/crypto.html#crypto_crypto_randombytes_size_callback
  - `controllers/Account.js` uses `signup()` to call `AccountModel.generateHash()` and generate an encrypted password
  - password encryption:
    - clear text:
      - https://simple.wikipedia.org/wiki/Cleartext
      - https://www.theverge.com/2019/4/18/18485599/facebook-instagram-passwords-plain-text-millions-users
    - encryption
      - https://www.howtogeek.com/howto/33949/htg-explains-what-is-encryption-and-how-does-it-work/
      - https://blueimp.github.io/JavaScript-MD5/
      - https://md5calc.com/hash/md5/12345678
    - rainbow tables:
      - https://www.geeksforgeeks.org/understanding-rainbow-table-attack/
      - https://en.wikipedia.org/wiki/Rainbow_table
    - salt
      - https://security.stackexchange.com/questions/17421/how-to-store-salt
      - https://security.stackexchange.com/questions/100898/why-store-a-salt-along-side-the-hashed-password
  - Mongo database
    - locally you will probably be using `mongod` (probably), and on Heroku you will be using your MongoDB cloud account
    - you will be able to see the following in a mongo client (`mongo` in Terminal/Powershell or the **MongoDB Compass** app):
      - the database name is set via `dbURL` and is `DomoMaker`
      - the *collectio*n is named `accounts` and is autogenerated by `mongoose` in **models/Account.js**
      - each user is a *document* in the `accounts` collection
      - handy mongo commands:
        - `show dbs`
        - `use DomoMaker`
        - `show collections`
        - `db.accounts.find().pretty()` // show all documents in the accounts collection
        - `db.accounts.remove({})` // delete all documents in the accounts collection
  - Login to an existing account with **login.handlebars**


## III. DomoMaker B - Assignment Walkthrough

- sessions






<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-9.md**](week-9.md)  |  [**IGME-430 Home**](../README.md) | **week-11.md**