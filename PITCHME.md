---?image=assets/sword.jpg
# Slaying The Beast
## How we escaped from PHP
[@garrybodsworth](https://twitter.com/garrybodsworth)

[@yagroltd](https://twitter.com/yagroltd)
Note:
- What we do at Yagro
- Two stories
- What to do when you inherit engineering at a startup
- Trying really hard to avoid the rewrite
- Bad code can be written in all languages
---
## Inheritance
- A server which is both website and webservice
- PHP + in-house framework
Note:
- Server, Ubuntu on Amazon
- PHP, MySQL, Apache
- In-house framework more of a bunch of helpers
- Requires Apache htaccess files
- Huge functions
- Pretty much impossible to enumerate APIs
- Can't remove dead code because it might be used and it is not possible to work it out
- Part server rendered, part client side
- Jquery spaghetti
- SVN deployment
- Poor security F grade [Observatory results yag.ro](https://observatory.mozilla.org/analyze.html?host=yag.ro)
---
## Plan?
- Observe
- Fix bugs
- Add features
- Learn how people use it
Note:
- Start at the bottom and work up
- Took over sprints after a number of weeks
- Critical to learn how the system works for customers
---
## Small steps
- Use git & GitLab
- "Push" deploy using CI
- Enable HTTPS
- Load balancers and firewalls
Note:
- Ability to run development locally - find loads of bugs just in the console output!
- Things are looking better, but now it is time to work out what the future is.
---
## DON'T REWRITE
Note:
- Many examples of the big rewrite failing
- I loathe to throw out working code
---
## DO REWRITE
Note:
- All the evidence pointed at it being necessary
---
## Stage #1
- Split out the marketing website
- This is PHP(!)
- Site and service domains different
Note:
- Website is written in PHP using PyroCMS based on Laravel
- Completely separate from webservice
- Now we have something we can work on
---
## Evaluate
- Frontend
- Backend
Note:
- Frontend tech to evaluate - React, Angular, Vue
- Backend tech will be Python - Flask, Django
- Try each technology to see if different approaches will work
- Initially evolution by replacing small bits
- It is worth spending time evaluating as the pain of changing later is large
---
## Database
- sqlacodegen
- Django inspectdb
- Bespoke scripting
- loaddata & dumpdata for MySQL -> Postgres
Note:
- Initially had raw SQL
- Tried sqlacodegen to generate SQLAlchemy
- Django inspectdb to generate the models
- There were quite a few multiple join and grouped queries - so choosing a few of them to replicate in these two ORMs would decide which to use. M2M
- After multiple days of battling SQLAlchemy, Django worked in a few hours.
- Create 2 DB connections, one MySQL, on Postgres, then use dumpdata and loaddata to transfer between the two.
- Once you are done you can start writing migrations!
---
## Backend
- Can't enumerate
- Use Django user model
- Better HTML emails
- 1000s of lines into dozens
Note:
- I did a version which ran teh original frontend on top of Python. Kind of worked but kept getting API "surprises"
- During development there was the huge vulnerability found in the PHP mail package
---
## Frontend
- Use VueJS
- Make SPA
Note:
- VueJS not prescriptive
- Was going to evolve the frontend we had
- Ended up having to rewrite all APIs
- More time wasted on WebPack
---
## Deployment
- Built very early on
- CI & CD
Note:
- GitLab CI runners and integration are great
---
## Limit Scope
- Keep database models
- CSS
Note:
- Only did basic data integrity fixes for the first version
- Saved loads of time not redesigning database
- Had to stay looking the same
- Keep the SASS
---
## Timescales
- Started Nov 2016
- Expected end of Jan 2017
- Delivered February 14th
Note:
- Overshot by 2 weeks
- Could have shipped earlier but waited for better quality
---
## Success?
- Nobody noticed
- Implementing bug for bug
Note:
- Nobody really noticed the entire foundations were replaced
- Usernames becoming case sensitive shows everyone has the wrong values in their password manager. Defence of the RFC was not going to fly.
- In future we can move database forward using migrations
- Improve the dynamic-ness of the UI
- Start tidying up the API surface area
