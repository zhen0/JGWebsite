### Creating An App to Share Our Stuff!

I live with my family in NYC and thought we are lucky enough to have a decent sized apartment, we still have cupboards that are full of stuff!  One of the main space-stealers are strollers.  For a long time we had three strollers - one for travel, one for everyday use and a jogging/off-roader stroller for runs and hikes. Eventually we sold the jogging stroller to a neighbor but then two days later decided to go for a hike upstate and had to ask if we could borrow it back.  This gave me the idea for an app that lets us share strollers and other big pieces of kit that we want occasional access to but don’t necessarily need to own our very own version of. 

At Grace Hopper we created a full-stack app as our Senior Enrichment/Junior Phase final project.  I took the skills I’d used there to create a basic app that used Sequelize to place users and kit in a PostgreSQL database.  I then wrote an api, again using Sequelize and also Express, to allow queries, new posts, deletions and alterations.  I used React for the front-end and managed the store with Redux.  It’s still a work in progress and I plan to add in a CSS library (perhaps Semantic UI), an authentication product such as Passport.js and to move my database to Heroku.  I’m also working on a mobile React Native app. 

Some of the lessons I have learned along the way:

- Debugging in React Native (and I guess any new language or framework) is hard!  (See more here!)

- Webpack, React and Redux don’t always play well together.  I spent an afternoon debugging the following error “TypeError: react__WEBPACK_IMPORTED_MODULE_4___default.a.memo is not a function” which popped up when I tried to use the redux connect function.  The error seemed to want my React module to be pure but thought it wasn’t.  Eventually I gave up and went to bed.  Which leads me to my next lesson…
- Sometimes it’s really helpful to take a break and old tricks can (kind of) work!  After giving up on the above error, my husband suggested “have you tried switching it off and back on again”. Although he was joking, when I came back to it with fresh eyes in the morning his suggestion made me consider trying a re-install.  I changed to React version in my package.json to 16.3.6, deleted the package-lock.json and re-ran npm install.  Hey Presto!  No more error messages and my app worked. 
- Postman is great for checking an api and giving you confidence that it works so you can focus on the front end!
- You can configure nodemon to ignore certain files by adding a nodemon ignore section into the package.json.  This was really helpful when nodemon kept crashing after finding what it thought was an error in the Expo/React Native related node-modules. 

- Always remember the ‘/’ before the address when you do an api request!
- User.findById is no longer a valid query when using sequelize.  Remember to use findByPk instead
