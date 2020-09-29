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

7. Open up **.babelrc **


- https://www.npmjs.com/package/nodemon
  
  
<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-4.md**](week-4.md)     |  [**IGME-430 Home**](../README.md) | [**week-7.md**](week-7.md)
