# Week - 1 (8/25/20 & 8/27/20)

## I. Overview

- Last time we got familiar with running `node` and `npm` on the command line, and installing packages (i.e. "libraries")
- Today we are going to look at some of the other tools we'll be using in this course:
  - Heroku is a *platform as service* - https://www.heroku.com/platform
  - We will be deploying our apps to Heroku using Git and GitHub

## II. Platform as a Service

- See ***Cloud Servers & Version Control*** slides in myCourses
- Heroku - *platform as service*:
  - can run code for us in PHP, Python, JavaScript, Java and so on
  - has many "add-ons" (databases such as Mongo, authentication systems etc...)
  - *scalable* - it does *load balancing* with "Dynos"
- ***VIDEO*** - These slides are recapped, in the first 9 minutes of this video: https://www.youtube.com/watch?v=GL_BfMltuD4

## III. GitHub & Version Control

- See ***Cloud Servers & Version Control*** slides in myCourses
- Workflow:
  - we use a local git repository, and push our changes to GitHub when we want
  - GitHub can be set up to then push our code to Heroku
  - Heroku will then update and relaunch our app
  - we can set up this "connection" up in the Heroku control panel
- Demo:
  - make a test repository
  - grab clone URL
  - launch PowerShell/GitBash/Terminal
  - create folder on local drive and `cd` into it
  - `git clone <url>`
  - `cd` into repository folder
  - create text file in folder
  - `git status` (untracked files present)
  - `git add` (file name, * - doesn't push .files, or .) - they are now in staging areas
  - `git commit -m "message"` (moves from staging area to local repo)
  - `git status`
  - `git push` (now that it's in the local repo, you can push)
  - NOTE: one-liner `git add commit` - https://stackoverflow.com/questions/4298960/git-add-and-commit-in-one-command/39831427
  - now modify file on GitHub and commit it
  - type `git pull` to download changes
  - ***OPTIONAL***: type `git remote update` or `git fetch` followed by `git diff master..origin/master` to just see the differences between the local and remote repository
- ***VIDEO*** - These slides are recapped, starting 9 minutes into this video: https://www.youtube.com/watch?v=GL_BfMltuD4

# IV. Resources

- https://overapi.com/git
- https://www.git-tower.com/blog/git-cheat-sheet

# V. - Thursday 8/27/20
- TODAY'S GOAL: Make sure that everyone is comfortable with node/npm (i.e. and has it working on their own computer), has Git working on their local computer, and has set up a Heroku account
- any questions on *HW-Review of basic npm & node* OR *Simple GitHub HW* ?
- the next HW due is *Git & Heroku Setup*:
  - if you have already completed it, after I check you off, you can bail for today!
  - if you have not yet completed it, you must stay logged in on Zoom and work on it. Let me know when you are done and I will check you off
- Next Wednesday night the *Simple HTTP* HW is due:
  - this HW has you creating and running a simple web server, and then pushing it to Heroku
  - we will review the necessary concepts on Tuesday's (2A) class
  - if you would like to get a head start on this HW (recommended) then go ahead and watch the pre-recorded lecture on this topic here: [YouTube - Week 2.1 - First Node Demo](https://www.youtube.com/watch?v=xksZCkshgQM) (54:18)

