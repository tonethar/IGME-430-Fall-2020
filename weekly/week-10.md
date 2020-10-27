# Week-10 (10/27/20 & 10/29/20)

## I. Overview 

- React MVC Project Overview
  - Project 2 Link
  - Discussion
  - Video Link
  - Link to DomoMaker

## II. DomoMaker A - Assignment Walkthrough

- The architecture of this app is very similar to the *Simple Models* HW
  - **app.js** to load the dependencies and start up the express server
  - **router.js** to call the various routes with code defined in the **controllers/** folder
  - a **models/** folder that contains mongoose models (one per file) such as **Account**
- Note: the **client.js** code is all [jQuery](https://jquery.com/) - here's a nice overview - [jQuery Fundamentals - jquery Basics](http://jqfundamentals.com/chapter/jquery-basics)
- Create an account with **signup.handlebars**
  - `<input id="pass" type="password" name="pass" placeholder="password"/>`
  - note that the `type` is `"password"`
  - `models/Account.js` is a mongoose model for the user's account
    - properties are `username`,`salt`,`password` (encrypted), `createdDate`
    - we encrypt the typed in password with node's built-in **crypto** library:
      - https://nodejs.org/api/crypto.html#crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback
      - https://nodejs.org/api/crypto.html#crypto_crypto_randombytes_size_callback
  - `controllers/Account.js` uses `signup()` to call `AccountModel.generateHash()` and generate an encrypted password
  - password encryption:
    - clear text
    - encryption
      - https://blueimp.github.io/JavaScript-MD5/
      - https://md5calc.com/hash/md5/12345678
    - rainbow tables:
      - https://www.geeksforgeeks.org/understanding-rainbow-table-attack/
      - https://en.wikipedia.org/wiki/Rainbow_table
    - salt
      - https://security.stackexchange.com/questions/17421/how-to-store-salt
      - https://security.stackexchange.com/questions/100898/why-store-a-salt-along-side-the-hashed-password
  - Mongo database
    - you will be able to see the mongo collections and documents created by **models/Account.js**
    - locally you will probably be using `mongod`


## III. DomoMaker B - Assignment Walkthrough

- sessions






<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-9.md**](week-9.md)  |  [**IGME-430 Home**](../README.md) | **week-11.md**
