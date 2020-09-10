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
  - head to **responses.js**:
    - it has a helper function called `respond()` that will make it so we don't have to keep repeating the `response.writeHead()`, `response.write()` and `response.end()` lines of code OVER and OVER and OVER and OVER and OVER and ...
    - stub in `getCats` - `const getCats = (request, response, acceptedTypes)...`
  - `npm start` - server should launch, even though it failed the tests (but it will do nothing at this point)
  
    
    

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-2.md**](week-2.md)     |  [**IGME-430 Home**](../README.md) | **week-4.md**
