---
layout: post
title:  Simple portfolio site in React
date:   2017-06-02 20:46:59 +0000
---


it’s been a minute, but I thought I’d write a bit about some projects I’ve been grinding on over the past month. The first is a music portfolio site that I made for myself that basically reproduces a Squarespace site. It’s up at www.martincrane.net 

The site is built in React with a Rails server for the blog and portfolio portion. Because a Rails server is overkill for such a static site, I just run it locally and save the json data it serves as a data file within the React site. I wanted to use React because I love the ability it has to quickly filter items by category. That’s really useful on a portfolio site where you want the viewer to see everything at once for browsing, yet easily be able to narrow down a category if something more specific is needed. I saved tags with each title record, and the filters use simple array filtering to scan the tags for a keyword. Easy enough.

The blog section of the site was interesting as well. I love the markup functionality of this github hosted blog, and I thought it would be cool to make a live blog that updates what you type realtime (again, trying to use the functionality of React in a more simple application). You can see what I made here https://martincrane.net/newblog . I keep my server local to keep hosting prices down, so this will submit what you write to a non-existant local server. However, you can see the realtime drafting of the post. It’s more or less a controlled form in React that is run through a markup parsing tool. I then created some custom regex tags to insert media. !!!rp!!!medialink!!!rp!!! will format whatever video or audio media link you insert realtime. 

Another cool hack I used was react-media-player . It’s an npm package written by http://travisrayarnold.com/ and it’s really flexible. I chose to host my audio with this over soundcloud because it is so much quicker to load, and you can easily make customized players. That being said, react-media-player always loads media upon page loading. I didn’t want 40mb worth of m4a’s being served every time someone went to my site, so I built a hack that loads a 4kb m4a bit of silence in every player upon page load. When a user clicks play, the player then advances to the next track (the actually media file). This solution decreased my site bandwidth tremendously. 

Lastly, this site uses uses React to give the menu and loading page a floating effect depending on the mouse location or device orientation. I used a ref in the css to grab the component and find its location and then measured the mouse location (saved in a redux state) to rotate the component towards the mouse. React is a little murky on component locations within componentDidMount(). I could get accurate left right coordinates, but not top bottom. Nevertheless, it was good enough to get a UX that felt like floating. I use the component coordinates to split the screen into an X-Y grid, with the component in the middle. I then use the mouse location to plot the mouse on that grid, turn it into a ratio (percentageY, percentageX), and then rotate the x and y of the component using realtime inline CSS that’s rendered using the component’s state. 

```
let style={"transform":`rotateX(${percentageY * -20}deg) rotateY(${percentageX * 20}deg) scale(1)`}
```

Using a CSS animation class in the component smoothes the redraw and gives the nice intertia feeling. Check out the float at www.martincrane.net

