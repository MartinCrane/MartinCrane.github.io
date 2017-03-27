---
layout: post
title:  "JS Bubbling Basics"
date:   2017-03-27 09:15:33 -0400
---


Bubbling is a simple JavaScript event concept that can give you a lot of power to simplify your event listeners if you use it right. Whenever you have an DOM element nested within another, events that happen within the smaller, child element necessarily happen within the surrounding parent element as well. Think of a container div within the body tags. Anything that happen in the container will also happen in the body. 

You can use it to save energy by assigning one event listener to many different elements. This is most easily shown through a button container. Say we have 3 different buttons within one common container div...

```
      <div class="container" id="menu">
            <div class="one" data-action="hop">
                <div class="stop-the-bubble">
                  <h1>--stop the bubble--</h1>
                </div>
                <h1>HOP</h1>
            </div>
            <div class="two" data-action="skip">
                <div class="stop-the-bubble">
                  <h1>--stop the bubble--</h1>
                </div>
                <h1>SKIP</h1>
            </div>
            <div class="three" data-action="jump">
                <div class="stop-the-bubble">
                  <h1>--stop the bubble--</h1>
                </div>
                <h1>JUMP</h1>
            </div>
        </div>
```
				

We can put one event listener on the container with the id "menu" and listen for clicks. That's what the following code is doing: 

```
document.getElementById("menu").addEventListener("click", bubbler)
```


But how can we tell a hop click from a skip click you might ask? Event listeners' trigger functions pass event objects into their action functions. These objects can be thought of as a snapshot of what's happening in the browser. They are fun to play around with in the debugger, as they have access to so much information about the state of the browser. One of those bits of info is the event target, which is the original HTML location of the event, in this case a click. So we can figure out where the click is coming from via the "event.target" in bubbler function that the above listener is triggering:

```
function bubbler(event) {
          let element = event.target.closest("div").dataset.action
          let message = `event.target = ${event.target} // action = ${element}`
          alert(message)
        }
```

Notice that in the top HTML we put in "data-action" tags writing the button HTML. You can sneak in a data-id tag to discern one button from another. So in our listener, we are grabbing the dataset.action from our tag, which will give us either a hop skip or jump.

One thing to watch out for. You might get an errant target if you happen to click on a child element that's nested within your button. For example, my text here is an h1 tag that has no data ID. Solve that with a .closest() on your target. It tells this target location to find the nearest parent element. If we set that to div, an h1 target will go up the chain until it finds our div w the proper tags. 

Lastly, if you want to prevent bubbling, you can do that easily with a .stopPropogation() method. See the following code for an example: 

```
let stopClass = document.getElementsByClassName("stop-the-bubble");
        for (var i = 0; i < stopClass.length; i++) {
        stopClass[i].addEventListener("click", function(e) {e.stopPropagation()});
        }
```

Bam. See the working code[ HERE!!!!](https://enigmatic-basin-52093.herokuapp.com/shapes/bubble)
