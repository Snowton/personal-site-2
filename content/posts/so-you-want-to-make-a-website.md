---
title: "So You Want to Make a Website"
date: 2023-09-15T10:35:16-04:00
draft: true
---
First: you can do it. You've done it before, and you came through to the other side with a product in hand.

Don't force yourself to put in more effort than you're able, because that creates negative associations, but be ready to drop-everything-and-code for gains.

I'll be logging my progress on entend for future-me to better remember how to build projects, as I don't do this that often.

## 9/25

Researched importing google fonts with react, and found next/font. also, getDate() was working on GMT time, which we can't have, so i spent a while figuring that out. now (hopefully) i can style in peace

So it's not hard to make things look nice. it's much harder to get things to be responsive, to figure out what you REALLY want them to look like, and to WRITE about the things you need to write about before doing all of these brainless things.
## 9/24

time to test if the intentions work for new days!! and it kind of did, but kind of didn't. i think it didn't work partially because i was still developing it, so we'll see how it works tomorrow.

I got the reflections + done updating to work.
## 9/22 and 9/23

I did a bit of work yesterday but forgot to log it. One of the main important things is that in order for sizing on position: absolute to work in CSS, the parent has to be position: relative, otherwise you'll size/position relative to the entire page or something.

I finally got the form and the updating the database to work. :) I also mostly finalized how I would get the entries in the database to update, and added helpful functionality for keeping track of the dones/reflections even if you change the wording of an intention.

I got the calendar to work!! and did a bit of listing with previous intentions, and stuff.
## 9/19

Met with Julie a bit and worked on formatting the form so the syntax highlighting would show up.
## 9/17 

Today I read about how to handle form elements in React. Also, setValue functions can take in a function that goes from prev value to new value. I started implementing a form in intentions.js.
## 9/16

I added functionality for adding/getting intentions to the api. I read about good ways to store data in nosql databases for a users:posts relationship. Turns out to be flexible I might like to be storing the posts separately with a reference to the userID, and storing an array of intentionIDs for every user.
## 9/15

Before today, I read a lot about creating serverless applications with React+Next.js, and using vercel to deploy them. I then created a next/react project in /programfiles, and created some frontend routes I might like to see, and example user data in my_user.js. I also created some easels with ideas and layouts. This was a very open-ended "what do I want to build" phase.

Today, I decided to start coding the actual functionality of the page. I read about creating a github-style calendar (not heatmap in this case, but similar). I read about using mongo with serverless applications in next. I figured out how to use mongo locally again (see MongoDB file in the life vault). 

For some reason, `router.query` started giving me "favicon.ico" instead of the identity parameter in the URL, like "mathematician". I spent a long time trying to figure out what the hell was going on until I fixed some other thing and realized the page would render even if the console was logging silly errors like that. I couldn't find anything like this on the internet either, so I think my computer is just trying to screw me over.
