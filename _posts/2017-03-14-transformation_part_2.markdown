---
layout: post
title:  "Transformation part 2"
date:   2017-03-14 13:53:49 -0400
---

Last week I was working on matrix 3d transformations of CSS using ruby. The results were interesting but a little boring. You can see them [here](https://enigmatic-basin-52093.herokuapp.com/shapes/ruby) and read about them [here](https://martincrane.github.io/2017/03/03/transformation/).

This week I wanted to make them more dynamic so I dove into jQuery. jQuery can listen to mouse movements and update CSS accordingly using the .mousemove() function. It passes an event object into your function that contains 2 pieces of data, event_object.pageY, which is the Y position of the mouse, and event_object.pageX, which is the X position of the mouse. You can then use these values to manipulate the CSS. 

```
$( "body" ).mousemove(function( event_object ) {
  var MouseY = event_object.pageY;
  var MouseX = event_object.pageX;
	$(".center").css('width', MouseY + '%');
	}
```

So the above example is saying everytime the mouse moves within the body tag of the webpage ($( "body" ).mousemove), we are going to execute a function that has this event_object that gets passed into it ((function( event_object ) {). Then, the next line says, we're going to make a variable for the X and Y values of the mouse so we can use them to change something (  var MouseY = event_object.pageY; var MouseX = event_object.pageX;). Finally, we execute what we want to change. In this case, it is the width of all divs in the center class, and it is changed to the value of the vertical quardinate of the mouse (MouseY). Pretty cool.

Apply that same logic to matrix 3d, and you have a whole other beast entirely. Matrix3d is so unwieldy that I find it's a process of trial and error to get something that feels good. There are 16 variables to change, and often small abounts of input can warp them heavily. I'm going to include the code for one of the cool floating effects I made with matrix 3d here:

```
var multiply = 0;

function twist() {
  var PadWidth = Math.sin(multiply) * <%= @shape.skew_1 %> * .0001 ;
  var PadHeight = Math.sin(multiply) * <%= @shape.skew_1 %> * .0002 ;
  var PadSkew = Math.sin(multiply) * <%= @shape.skew_1 %> * .0002;
  multiply = multiply + .001;
  $( ".skew" ).css('-webkit-transform','matrix3d(1,'+PadSkew+',0,'+PadSkew+','+PadHeight+',1,'+PadHeight+',0,0,0,1,0,5,0,0,1)');
}

setInterval(function(){
twist();
}, 1);
```

Check out what it looks like IRL [here](https://enigmatic-basin-52093.herokuapp.com/shapes/float). This is using the setInterval function to update the matrix 3d of the div every milisecond. The setInterval function (setInterval(function, miliseconds)) says do this function every x miliseconds. The twist() function just edits the matrix 3d CSS. It uses sin functions because sin never go above 1! We can use it to keep elements roatating within a fixed range. Pretty cool.

Lastly, I combined the two ideas to make a page that moves with the mouse! This is definitely my favorite. Check it out [here](https://enigmatic-basin-52093.herokuapp.com/shapes/mousefloat). Inspect the code to see what I did.

Also [this.](https://enigmatic-basin-52093.herokuapp.com/shapes/thirds)
