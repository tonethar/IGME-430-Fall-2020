# Week-6 (9/29/20 & 10/01/20)

## I. Overview
- This week we are talking about *tools* that will make your developer life easier!

## II. Transpiling with Babel

- Here's some newer JS features we'd like to try:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator
- But these features don't work in all recent browsers - what to do?
  - https://babeljs.io/
  
## III. Nodemon & Babel Demo

- Start code: https://github.com/IGM-RichMedia-at-RIT/Nodemon-Babel-Class-Example (also linked in Week 5 of myCourses)
- There is a YouTube Video walkthrough f this demo linked in "Week 5 Videos" in myCourses 

1. `npm install --save-dev nodemon @babel/core @babel/preset-env @babel/cli`

- If you are on Mac OS and run into issues like **gyp: No Xcode or CLT version detected!**:
  - https://stackoverflow.com/questions/60573595/npm-install-fails-on-node-gyp-rebuild-with-gyp-no-xcode-or-clt-version-detec
  - https://developer.apple.com/download/more/

2. Check **package.json** `"devDependencies"` to see what was installed

3. Add a script to your **package.json** - `"nodemon" : "nodemon --watch ./src ./src/server.js"`

4. Run it with `npm run nodemon`

5. Modify one or the files in your `src` folder - you will see the server reboot

6. ... now we'll move on the babel ...

7. Open up **.babelrc** - and take a look - for now it is compiling to ES5 - we're not going to change this for now - but this file IS required for bable to work

8. Add a script to your **package.json** - `"build" : "babel ./client --out-file ./hosted/bundle.js"`

    - this is going to transpile your ***client-side*** JavaScript and put the results of the compilation into **/hosted/bundle.js**

9. Go ahead and make a **hosted** folder

10. Move **client.html** into the **hosted** folder

11. Move the JS from **client.html** into a file named **client.js**, and put that file in the **client** folder

12. Delete the "babel" script tags from **client.html**

13. Link to our (soon to be) transpiled JS code - `<script src="/bundle.js"></script>`

14. Change **htmlResponses.js** to point at new location of **client.html** (in the **hosted** folder)

15. Write code to load **bundle.js** 

16. Write a `getBundle` function - the `content-type` is `'application/javascript'`

17. In **server.js** modify `urlStruct` to serve up **/bundle.js**

18. Now we can `npm run build`
    - check the **hosted** folder to see **bundle.js**
    - open up **bundle.js** to see the transpiled JavaScript
    - go ahead and edit **client.js** to and `npm run build` again, and then check **bundle.js** to see the changes
    - don't edit **bundle.js** (your changes will get continually wiped out)
    - `npm run build` and then `npm run nodemon` to see it functioning (check the browser to see that **bundle.js** is getting loaded)
  

- https://www.npmjs.com/package/nodemon
  
  
<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-4.md**](week-4.md)     |  [**IGME-430 Home**](../README.md) | [**week-7.md**](week-7.md)
