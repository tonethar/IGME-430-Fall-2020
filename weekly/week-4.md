# Week-4 (9/15/20 & 9/17/20)

## I. Finish up notes for *HTTP API Assignment*
- See IV-A. & IV-B. from [last week](week-3.md)
- Look at completed examples and test them with [Postman](https://www.postman.com/downloads/)

<hr>

## II. *HTTP API Assignment II*
- What's new: `HEAD` requests and body parsing of `POST` requests
- Working example here: - https://http-api-application-ii.herokuapp.com/ - let's test this in the browser
  - shared data is being created "in the cloud" - so keep the names SFW please
  - let's test this version both in the browser (with the Network tab open) & with Postman



### II-A. Questions
- *What is the major difference between what the server returns when it receives a `HEAD` request as opposed to the more common `GET` request?*
- *How do `POST` requests differ from `GET` requests? i.e. When should we use a `POST` request **instead of** a `GET` request?*

### II-B. Study Guide Reference Links
- HTTP Methods:
  - https://www.tutorialspoint.com/http/http_methods.htm 
  - http://www.w3schools.com/TAGS/ref_httpmethods.asp 
- HTTP Responses:
  - https://geemus.gitbooks.io/http-api-design/content/en/responses/ 
  
<hr>
  
## III. `HEAD` request demo

- demo starter code (link is also in myCourses): https://github.com/IGM-RichMedia-at-RIT/head-request-class-example
- demo YouTube video (link is also in myCourses): https://www.youtube.com/watch?v=DPkIjyjVHTs
- Overview:
  - look over code:
    - **package.json** - we only have eslint `"devDependencies"`
    - **server.js** is already importing **htmlResponses.js** and **jsonResponses.js**, but it needs to get its *routing* set up
    - **htmlResponses.js** is all set - it simply sends back 2 static files (**client.html** & **style.css**)
    - **jsonResponses.js** is where most of the work still needs to be done
    - **client.html** will send XHR requests to the server:
      - sends Ajax requests via `XHR`
      - the user will be able to choose the *request method* of either `GET` or `HEAD` (as opposed to the user changing the value of the `Accept` header like we did in the last HW)
 - Walkthrough:
   - **jsonResponses.js**:
     - `const users = {};` 
       - is going to store data that the user sends to the server - this data will persist for 15 minutes or so until the Heroku server reboots. Project 1 will also follow this model of short-lived data. For Project 2 we'll learn to use MongoDB to persist the data so that the server can access it even through reboots
     - complete `respondJSON`
     - what are the differences between `respondJSONMeta`, `getUsersMeta`, `notFoundMeta` AND `respondJSON`, `getUsers`, `notFound` ?
       - when is this useful?

<hr>

## IV. `POST` requests & body parsing example

- demo starter code (link is also in myCourses): https://github.com/IGM-RichMedia-at-RIT/body-parse-example
- demo YouTube video (link is also in myCourses): https://www.youtube.com/watch?v=QY5sBCg6Ksg
- **YOU NEED TO GO THROUGH THIS ON YOUR OWN**

<hr>  

## V. Project 1 Assigned

- Requirements (link is also in myCourses): https://people.rit.edu/arwigm/430/
- YouTube video (link is also in myCourses): https://www.youtube.com/watch?v=kozmX-FWqdc
- See myCourses dropboxes for deliverable due dates

<hr><hr>  

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-3.md**](week-3.md)     |  [**IGME-430 Home**](../README.md) | **week-5.md**
