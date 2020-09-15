# Week-3 (9/08/20 & 9/10/20)

## I. *Simple HTTP HW*

- Let's review it

<hr>

## II. *Steaming Media Assignment* Notes

- It's due tomorrow night
- If you are stuck on anything, hang around after class

### II-A. More on HTTP Protocol

- Let's discuss how a browser downloads and assembles a web page - head to this demo in Chrome or Firefox, and open the Web Inspector:
 - http://igm.rit.edu/~acjvks/courses/shared/430/simple-server-request-demo/middle-aged-man.html
 
### II-B. In-class Demo
- Let's add an image to the landing page of our HW - Node Simple Web API:
  - Instructions: https://github.com/tonethar/IGME-430-Shared/blob/master/notes/HW-node-simple-web-api.md
  - Current state of landing page (no image): https://dorkus-jokes.herokuapp.com/
  - Here's the image we want to use - it is hosted at igm.rit.edu: http://igm.rit.edu/~acjvks/courses/shared/430/simple-server-request-demo/images/mam.jpg
  - GOAL: Get this image to appear on the bottom of the landing page - so EASY!
  - PROBLEM: This is called "inlining" - and we are using someone else's server to display an image - sooner or later they will notice and/or the file will get moved or deleted.
- Now let's have our NodeJS server host the image
  - GOAL: Host the image locally on our NodeJS server and serve it up so that it appears on the bottom of the landing page, DO NOT use the igm.rit.edu link above
  - HINT: See *Simple HTTP HW* for the required code - in that HW we served the **spongegar.png** image under the **dankmemes** endpoint

### II-C. Stream Media HW
- The assignment is in Week 2 content section of myCourses
- The "done" example is here:
  - https://acjvks-streaming-media-fall-20.herokuapp.com
  - https://acjvks-streaming-media-fall-20.herokuapp.com/page2
  - https://acjvks-streaming-media-fall-20.herokuapp.com/page3
- Here's a screenshot of the headers:

![screenshot](_images/party-mp4-response-headers.png)
  

 - Many of the concepts were already covered in the *Simple HTTP HW*:
   - CommonJS modules with `require()` and `module.exports`
   - `onRequest` "request handler" for `http.createServer()`
   - URL endpoints
   - sending status codes (ex `200 Ok`) with `response.writeHead()`
   - sending content-type headers (ex. `content-type: image/png` or `content-type: text/html`) with `response.writeHead()`
   - sending content (text or PNG media types) with `response.write()`
 - New concepts covered in this HW:
   - new status code for streaming: `206 Partial Content`
   - new `content-type` values - `video/mp4` and `audio/mpeg`
   - new headers for streaming: `Content-Range` and `Accept-Ranges`
   - new methods for streaming: `fs.createReadStream()`
   - writing a helper function
   - the concept that it a client must make *multiple requests* to a web server for a typical web page:
     - web pages consist of multiple files: HTML, CSS, JS, images, and so on
     - the first file that a client (ex. Web Browser) downloads is usually the default HTML file that is located at the URL the user typed into the browser (or link that they clicked on)
     - the additional files (CSS,JS, images) are requested after the client begins to parse the HTML page
     - each of these files must be individually requested by the client app 
     - the client then "assembles" the web page and displays it to the user
     - this means that we have to create an *endpoint* for each file (HTML,CSS, media, etc) in our `onRequest` handler
   - let's check the HW to see if you got it right!
 
<hr>

## III. Notes for *HTTP API Study Guide*
- See myCourses dropbox
- This won't take you too long - so get'er done
- See *Week-3/Lectures* in myCourses for helpful PDFs
- See the first YouTube video ("Rich Media 2 - Week 3.1 Servers") linked under *Video Lectures/Week 3 Videos* in myCourses

<hr>

## IV. Notes for HTTP API Assignment
- This is a *substantial* assignment - so get started ASAP
- See *Week-3/Class Examples* in myCourses for links to helpful code
- See the 2nd and 3rd YouTube videos ("Rich Media 2 - Week 3.2 Accept Headers" & "Rich Media 2 - Week 3.3 Status Codes") linked under *Video Lectures/Week 3 Videos* in myCourses

### IV-A. Accept Header Example
- see video and demo code links in myCourses
- here's the demo code link - you can either download the ZIP or `git clone` it: https://github.com/IGM-RichMedia-at-RIT/accept-header-example
- this demo code will make a good starter for the HW, so I recommend you clone it
- here's the demo video link - https://www.youtube.com/watch?v=ElramkPkvaA
- Walkthrough:
  - `cd` into folder
  - look over **package.json** file
  - `npm i` will download to **node_modules** all of those packages listed under the `"dependencies"` and `"dev-dependencies"` keys
  - the **node_modules** folder is huge! That's why we don't commit it to our respository (or myCourses)
  - `npm test` or `npm run test` - it will fail for now
  - look over **client.html**
    - this file contains JavaScript that will run on the *client side* (e.g. in the user's browser)
    - I recommend you delete the babel stuff as it is not necessary to run ES6 in 2020's browsers
    - we'll be adding Ajax calls (e.g. `XHR`) to this later on
    - **IMPORTANT** - **client.html** will be downloaded from our server, but will then be running in the user's browser
    - for **client.html** to get the "cat data" it craves, it will have to send an Ajax request
    - our server (**server.js**) will return the cata data in either JSON or customized XML (JSON will be the default)
      - JSON = "JavaScript Object Notation"
      - XML = "Extensible Markup Language" (i.e. a language for defining our own markup language)
    - add `onclick` event handlers or `click` event listeners to the buttons - have them call `sendAjax` - pass in `/cats` and either `application/json` or `text/xml`
    - for testing purposes, add this to the top of `sendAjax` - `console.log(url,acceptedType);`
    - to test the button clicking, you can open **client.html** directly in a browser (we don't need to serve it via node and **server.js**)
    - now implement the rest of `sendAjax`
      - create new XHR object
      - `open` connection
      - set the `Accept` request header
      - set up `onload` callback function that points at `handleResponse`
      - `send` the request
    - add `console.log(xhr.response);` to the top of `handleResponse`
  - head to **responses.js**:
    - it has a helper function called `respond()` that will make it so we don't have to keep repeating the `response.writeHead()`, `response.write()` and `response.end()` lines of code OVER and OVER and OVER and OVER and OVER and ...
    - stub in `getCats` - `const getCats = (request, response, acceptedTypes)...`
  - `npm start` - server should launch, even though it failed the tests (but it will do nothing at this point)
  - head to **server.js**
    - we are importing a new library - `url`
    - let's see it in action - add the following to the top of `onRequest()` and then head to `localhost:3000` and check the console. We should see that we can pull out a lot of information - including info in the *query string*
      - `const parsedUrl = url.parse(request.url);`
      - `console.log(parsedUrl);`
    - now let's get an array of the "accept" headers that the requester (client) is sending over - add this to `onRequest`:
      - `const acceptedTypes = request.headers.accept.split(",");`
      - `console.log(acceptedTypes);`
    - go ahead and test it at `localhost:3000` and check the node console
    - now test it from the browser via the **client.html** XHR calls - you will need to change the url to `http://localhost:3000/getCats` (don't forget to change it back later) - check the node console to see how the `content-type` changes depending on the button we click
  - still in **server.js**:
    - how do we handle the different `.pathname` values and our endpoints?
      - up until now we have been using `if..else` or `switch` statements
      - let's instead use a *dispatch table* (`urlStruct`) - a dispatch table has *references* (or pointers in other languages) to functions
      - let's set up values for `/`, `cats` and `index`
    - now in `onRequest`, how do I call these functions?
      - let's implement it:
        - now test it in the browser, we should get back our index page
        - now test the browser `XHR` by clicking the buttons - because node is now serving up the page, be sure to double-check that the XHR `url` is `/cats` - we should see logs to the node console
  - in **responses.js**:
    - implement `getCats`
    - now test `/cats` from browser to see the JSON
    - now click buttons in `/cats` from **client.html** to see the JSON
  - in **client.html**:  
    - complete the implementation of `handleResponse` so that it displays the JSON cat data in the window
    - test it
  - still in **client.html**:  
    - implement the XML parsing code
    - we can't test it because the server is still only sending back JSON
  - in **responses.js**:
    - in `getCats`, get the server to send back XML if the client "requests" it by looking at the `Accept` header that the client sent
  - test in **client.html**:
    - when the client asks for XML (via the `Accept` header) it gets the XML file
    - when the client asks for JSON (via the `Accept` header) it gets the JSON file
    
### IV-B. Status Codes Example
- you will also need this for the *HTTP API Assignment*
- ***you will need to run through this on your own***
- see video and demo code links in myCourses
- here's the demo code link - you probably want to download the ZIP (assuming you are already using the *Accept Header Demo* as HW start code: https://github.com/IGM-RichMedia-at-RIT/status-code-example - 
- here's the demo video link - https://www.youtube.com/watch?v=vHSb7GjmMxA
- among other things, this covers how to grab parameters from a query string, like `/?loggedin=true`
- it uses the `query` library, and `query.parse()` to do so
- reference:
  - https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
  - https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
  - https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/418
  - https://www.ietf.org/rfc/rfc2324.txt
  - https://www.google.com/teapot
  - https://en.wikipedia.org/wiki/Hyper_Text_Coffee_Pot_Control_Protocol

#### IV-B-i. Code Snippet for grabbing *url parameters* with the `query` library

```js
const parsedUrl = url.parse(request.url);
const params = query.parse(parsedUrl.query);
const valid = query.parse(parsedUrl.query).valid;
console.dir(parsedUrl);
console.dir(params);
console.dir(valid);
```
    
## V. Next Week

- Next week we'll talk about different kinds of requests, like `HEAD`, so that you can get *HTTP API Assignment II* working

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-2.md**](week-2.md)     |  [**IGME-430 Home**](../README.md) | [**week-4.md**](week-4.md)
