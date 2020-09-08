# Week-3 (9/08/20 & 9/10/20)

## I. *Simple HTTP HW*

- Let's review it

<hr>

## II. *Steaming Media Assignment* Notes

- It's due tomorrow night
- If you are stuck on anything, hang around after class

<hr>

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
  
 


| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
| [**week-2.md**](week-2.md)     |  [**IGME-430 Home**](../README.md) | **week-4.md**
