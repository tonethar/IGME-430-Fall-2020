# Week-0 (8/20/20)

## I. Overview
- Welcome to the course!
- Make sure you read the syllabus linked from the main landing page here --> [README.md](../README.md) 
- This is not an easy class:
  - so start assignments early
  - ask for help when you need it
  - use the Discord - it was very helpful for many students last semester
- What is this course about?
  - Up until now, you've been programming mostly on the *client-side* (HTML/CSS/JavaScript), and then FTPing your pages up to banjo, which is a basic HTTP web server
  - #1 - In this course we will learn how to write code and create our own *web servers* - thus we will be doing *full-stack* development (both front-end AND back-end)
    - How to work with the HTTP protocol
    - How to retrieve/pass/store data on our customized web server
    - How to authenticate users
    - How to author distributed systems [(Redis)](https://redis.io/)
    - In this course, we'll be doing the front and back-end programming in the SAME language (JavaScript). This can be a little confusing for people because they have to keep straight in their head the following - "Is this JS code running on the *front-end* (the browser) or the *back-end* (a Node.js server)"
      - JS in the web browser has the usual limitations (no *write* access to computer hard-drive, no database, no native threads etc), less access to newer JS features, having to support old browsers, etc ...
      - JS running on a Node.js server however has full access to underlying hardware - so much more powerful!
  - #2 - Work with a modern MVVM framework (React, which is similar to Vue.js)
  - #3 - Modern Software Development Concepts (GitHub instead of FTP for posting code, code validation via linting, build/continuous integration tools such as Webpack & CircleCI)

## II. Example Projects
- next week!

## III. Communication

- What name do you call me?
  - "Professor", "Professor Jefferson", or "Tony" all work
- Discord
  - Invites:
    - Change your nickname to your real name & section (ex. "Grace Hopper 01")
    - Post an Intro
  - Professional/SFW: Be aware of your status text (ex. "f-ing losing at Fortnight!" won't cut it)
- Zoom Professionalism
    - Article link (paywalled): https://www.wsj.com/articles/seven-rules-of-zoom-meeting-etiquette-from-the-pros-11594551601
    - The PDF of this article is in myCourses
    - Zoom - hold space bar to talk. But before you ask a question, first ask yourself "will others benefit from the answer to this question?"
      - if not, then post to the class Discord `#live-chat` channel
      - otherwise, please ask questions! 
 - Attendance/Participation/Engagement (10% of grade)
   - Zoom meetings
     - be on time (there's a waiting room for our Zoom meetings, so it's pretty obvious when someone is late)
     - keep web cam on, and microphone muted
     - you could get called on at anytime, so be ready to respond 
   - Discord Invite & Introduction & Logistics Survey
     - if I have to ask multiple times, it will hurt your participation grade
   - There will be several (graded) Discord discussion threads during the semester
  

## IV. Week-0 Introductions ("Do I have to?" - YES!)
- Introductions - we'll do this alphabetically - so be ready:
 - 1) name/major/year
 - 2) where you are physically located right now
 - 3) your favorite food
 - 4) something interesting you did this summer
 - "Next!"
 
 
 ## V. Week-0 Assignment

- *Review of basic npm & node* is due next Wednesday night (8/26/2020) - see myCourses dropbox for instructions - here are the video links:
  - [Node Demo - Intro to node & npm - 1 (09:45)](https://video.rit.edu/Watch/430-intro-node-npm-1)
  - Here is our exciting code:
  
  ```js
  console.log("Hello!");
  
  function hello2(){
    console.log("Hello Hello!!");
  }
  
  const hello3 = () =>{
    console.log("Hello Hello Hello!!!");
  };
  
  hello2();
  hello3();
  ```
  
  - You need to know these Unix file management commands - these are covered in the video:
    - `cd xxx` - *change directory in xxx folder*
    - `cd ..` - *change directory "up" a level*
    - `pwd` - *print working directory* - you always have a "current working directory" when executing commands
    - `ls` - *list contents of current directory*
   - And for command line Node.js:
     - `npm init -y`
     - `npm test`
     - `npm start`
     - `npm -v`
     - `node -v`
- [Node Demo - Intro to node & npm - 2 (06:04)](https://video.rit.edu/Watch/430-intro-node-npm-2):
  - add a npm package to the project - https://www.npmjs.com/package/shortid
  - here's the code to use the package:
  
```js
const shortid = require('shortid');
console.log(shortid.generate());
```
  
- on the command line:
  - `cd` to the folder
  - `npm start`
- ***BOOM*** - **`Error: Cannot find module 'shortid'`**
- it didn't work because you need to *install* the `shortid` package first (i.e. download the files, which will be place in a `node_modules` folder) 
  - `npm install shortid` (or `npm i shortid`)
  - `npm start`
  - it should work now
  - now take a look in the **package.json** file - you will see that a `dependencies` key has been added
  
- before you submit this assignment to myCourses, you will need to delete the `node_modules` folder (to keep the file size down)
- so how do you re-download the files when you want to work on the project later?
  - ***EASY!*** - `npm install` (or `npm i`)
  
  
- ***IMPORTANT:*** This first assignment is really easy and won't take too long, later assignments are much more involved, so don't procrastinate and start your assignments early!
 

 ## VI. Resources?
 
 - See *Node Intro* slides in myCourses
 - Any Questions?
 
 <hr><hr>
 
| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|   :-\  |  [**IGME-430 Home**](../README.md) | [**week-1.md**](week-1.md)
