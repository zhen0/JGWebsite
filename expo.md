### Error: 'assets/icon.png' could not be found…. A Journey Into the World and Bugs of React Native, Redux and Expo 

At Grace Hopper we get a week at home between Junior and Senior Phase to review all we learned in the last few weeks and prep for the upcoming build-projects. As my wonderful husband (who works in tech but isn’t an engineer) keeps telling me that mobile is the Next Big Thing, I wanted to use the time to build my own app and get some practice using React Native.

I started full of confidence as I read around React Native and saw that it looked similar to React and JS.  I was also pretty pleased to see an app called Expo that facilitates the development process and lets you write in what feels a lot like a JS environment (I wrote my code on VSCode) without having to see up an Android or Apple developer account. I followed the pretty clear instructions on the Expo app set up docs and after a bit of back and forth setting up Watchman (requiring also the set up of Homebrew…) I had a basic “Hello World” app up and running.  I was then able to change the text and add pictures.  I thought the hard part was over and started planning out my app…..

I planned an app that would work with the sharing app I had already built (part of) in Sequelize, Express and React.  This meant using forms and a connection to my api.  After reading around the best way to create forms in React Native and considering formik, I realized that a simple solution might be a good starting point and used React Native’s Text-Input component, which was pretty straight forward and worked pretty well. 

So far so good.  But when I tried to add Redux and connect to the store, I hit a problem when I tried to use ‘connect’.  (Eerily similar to the issue I had a few days ago when setting up Redux in my web-app…).  The error message (in a scary big red screen - thanks Expo!) was: 

Uncaught Invariant Violation: Element type is invalid: expected a string (for built-in components) or a class/function (for composite components) but got: object.

Some reading around (especially here) made me think I’d maybe imported or exported a component incorrectly, perhaps forgetting {} around the import of an export or maybe adding {} around an import of an export default.  However, I double-checked and my imports and exports all looked good.  Further reading suggested I maybe should try updating my React Native version.  I gave it a break, thinking fresh eyes might help… then came back to another error!

Error: 'assets/icon.png' could not be found, because 'assets' is not a subdirectory of any of the roots

This was on the master branch from git. I’d committed a version that I knew was working and now it’s not.  What the heck???!!!

At this point I’ve decided to let the issue percolate at the back of my mind while I work on my Grace Hopper projects. But I'll be returning to tackle this again! 

As a follow up note, I encountered similar issues in my hackathon project baseball bandersnatch. After some investigation, I think it's a versions issue and I decided to tackle react native without redux. It's been a good reminder of the basics of react and using the home component as a kind of store in react gave me similar functionality as redux. 
