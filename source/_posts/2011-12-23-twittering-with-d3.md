---
layout: post
title: Twittering with D3
date: 2011-12-23 20:08
comments: true
category: viz
viz: viz

---

What you see above is something I had been thinking of doing since the obsession of a redesign hit my head: rendering visual snippets of my latest tracked actions as pretty and useless graphics. Hopefully this is the first of many. 

My very first data mapping project was my [Final Year Project](http://j.mp/divyaieee) where I had to render XML data from the server on to a J2ME application. I have since not wanted to recreate that horrific experience again and have stayed well out of the way of such complicated mappings. But, last year, I wrote a bit on using [Polymaps for mapping tweets](http://www.netmagazine.com/tutorials/build-tweet-map-svg) and discovered that [Mike Bostock](http://bost.ocks.org/mike/) has since created a new library for data visualization called [D3](http://mbostock.github.com/d3/). I finally got a chance to play with it.

### Idea

The bar chart shows a timeline of the last 10 tweets starting with the earliest tweet. Each bar represents a tweet and grows darker across the timeline based on how many retweets occur. The darkest bar represents a tweet that was retweeted the most. Clicking on each bar gives you the tweet itself and the actual number of retweets that has occurred.

I originally started with the idea of only plotting tweets created over the last 24 hours and the ebb and flow of each of their retweets. But, then, it became harder to visualize how I would treat retweets that occurred beyond a day. It seemed simpler to just switch over to plotting the graph for the latest few tweets.

### Design

I had in my mind a graded bar chart that would animate across time and change in color values based on when and how many retweets occurred. I wanted to include axes in the design, but they looked very noisy when I got around to doing them, so they were _axed_ :)

### Implementation

This project was primarily a vehicle to learn [D3](http://mbostock.github.com/d3/) and [node.js](http://nodejs.org/) and I must say I did learn quite a bit of both while using them. Not having much of a data visualization background, understanding `scale`, `transition`, and `data` took a while, but it became more intuitive as I grasped how these worked. 

The binding of `data` to each SVG/DOM object using `selectAll('<node>').data()` is really awesome. It makes it easy to add/remove nodes depending on the data that you are dealing with, though, it does require you to think carefully about your data object (I spent many sleepless hours on this). D3's handy [interpolators](https://github.com/mbostock/d3/wiki/Transitions#wiki-d3_interpolate) are useful for interpolating between arbitrary set of values. The variety of [mappings of domains to ranges](https://github.com/mbostock/d3/wiki/Scales) that is available is also impressive.  
    
I used [nTwitter](https://github.com/AvianFlu/ntwitter) to make requests to the Twitter REST API and write the results to a JSON file. Node’s async callbacks threw me in a loop but [Deepak](http://deepak.jois.name) used [Async](https://github.com/caolan/async) to make it all seamless (while also helping me out with a major rework of the code). 

[moment.js](http://momentjs.com/) was quite handy both server-side and client-side to parse and compare dates for tweets and retweets. 

### Play!

The code is in the [Viz](https://github.com/nimbupani/viz) folder to which I should be adding more such pointless data art. Please do suggest improvements or feel free to use this in your own obsessive experiments :)
 
