# Week-2 (9/01/20 & 9/03/20)

## I. Tuesday 9/01/20

- [Joke API HW](https://github.com/tonethar/IGME-430-Shared/blob/master/notes/HW-node-simple-web-api.md)
  - Create a node API project *from scratch*, with no "start code", and deploy it to GitHub & Heroku
  - Learn how to use nodemon


## II. Thursday 9/03/20
1. Continue with Joke API example:
    - Discuss [HTTP Protocol](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
      - Request phase (when the client initiates a connection):
        - [HTTP Request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) (ex. `GET`, `POST`, `PUT`)
        - Request url
        - [HTTP Request headers](https://developer.mozilla.org/en-US/docs/Glossary/Request_header) (ex. `user-agent`, `host`, `accept`)
        - (Look at the `XHR` code in **joke-client.html** to see some of this)
      - Response phase:
        - [HTTP Status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) (ex. 200)
        - [HTTP Response headers](https://developer.mozilla.org/en-US/docs/Glossary/Response_header) (ex. `content-type`, `Access-Control-Allow-Origin`)
        - Content
    - In this HW we created BOTH the *client* AND the *server*:
      - Request Phase: the `XHR` code in **joke-client.html**
      - Response Phase: what we did in Nodejs and **index.js**, using the [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse) class
    - New stuff:
      - Debugging on Heroku 
      - `git clone` our repository again (will then need to `npm install`)
      - Add testing with ESLint:
        - https://eslint.org
        - https://eslint.org/docs/rules/
        - https://www.npmjs.com/package/eslint-config-airbnb-base
        - Demo code:
          - `npm install --save-dev eslint eslint-config-airbnb eslint-plugin-import` (or just `npm install --save-dev eslint`)
          - for **package.json** - `"pretest": "eslint ./src --fix", "test": "echo \"Tests complete\""`
          - `eslint --init`
      - Integrate with CircleCI
      - Create an external module
        - use CommonJS - i.e. `require()` and `module.exports`:
          - this is a "node only" thing, and what the PDF HW/Exercises will use
          - https://nodejs.org/en/knowledge/getting-started/what-is-require/
          - https://flaviocopes.com/commonjs/
          - also demo the use of ES6 "shorthand" object notation/initialization
        - use ES6 modules i.e. `import` and `export` (like we did in 330)
  
  
2. Simple HTTP HW - see Week-1 content section of myCourses
    - [Port](https://en.wikipedia.org/wiki/Port_(computer_networking))
    - [List_of_TCP_and_UDP_port_numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
    - [Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml)
    - other questions?

<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-1.md**](week-1.md)     |  [**IGME-430 Home**](../README.md) | **week-3.md**
