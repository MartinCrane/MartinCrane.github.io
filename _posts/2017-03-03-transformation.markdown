---
layout: post
title:  "Transformation"
date:   2017-03-03 09:05:27 -0500
---


This last week I’ve come across some cool websites, and I want to know how they work! So I thought I’d take something apart. I’m very much a beginner, so bear with my inexperience here. 

What struck me about Diane Martel’s [site](http://diane-martel.com/) was the depth of the scrolling, and how that depth made a simple portfolio site feel really incredible. I love these 3D elements in UI, and I think it’s literally a new space that allows for innovation. 

My first step was to look at the source code (view-source:http://diane-martel.com/). As I’m still learning Javascript, I wasn’t familiar with a lot of the site’s inner workings. It looks like it utilizes some functions to determine the window size, and then utilizes html canvas.

What I DID understand, though, was the inspect element view in chrome. It displays in realtime the updates to the html. What I noticed most was the constantly changing matrix3d CSS tag on each element of the menu bar. Matrix3D tag controls all of the 3D transformations in html. It uses a matrix of 16 numbers to control a CSS object's skew, rotation, etc. I'm still getting used to what each values use, so check out more at  [site](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function) and [site](https://dev.opera.com/articles/understanding-the-css-transforms-matrix/) .

I'm guessing that Javascript controls these values, so I thought I would make a somewhat static version of the transformations in Ruby. I drafted up a simple web page and created a controller for it in Ruby. I wanted to be able to pass a number into the rotation of the object and have the page re-render with the new skew, so I made a create route that constantly re-renders with the last user input.

```
  def create
    @shape = Shape.new
    @shape.type = params[:shape][:type]
    @unit = @shape.type * 0.00001
    render :index
  end
```

The form stores the user input as @shape.type and a scale as @unit. Then, I put them back into the CSS that contorts the element. 

```
.skew_left {
  transform: matrix3d(1,0,0,<%=@shape.type * 0.0001%>,0.00,<%=@shape.type * 0.3%>,0.002, <%=@shape.type * @unit%>,0,-0.02,1,0,5,0,0,1);
-webkit-transform: matrix3d(1,0,0,<%=@shape.type * 0.0001%>,0.00,<%=@shape.type * 0.3%>,0.002,<%=@shape.type * @unit%>,0,-0.02,1,0,5,0,0,1);
}
```

Skew-left is a CSS class I made that handles the 3D distortions of the CSS. You can see how @shape.type updates the matrix3d tags with user values. What's interesting to me about this is using a single input (in this case, a number) to drive several 3D distortions at once. The user input is pretty static here, but it could easily be replaced with a mouse position (or any stream of data). You can modify the ratio of how fast the distortions change relative to each other using algebra, which I haven't done in 15 years so I'm not going to try here. But the possiblities are amazing. Here's a screenshot:

![Imgur](http://i.imgur.com/L5Pnm08.jpg)

The site is here: [RUBY DISTORTIONS](https://enigmatic-basin-52093.herokuapp.com/shapes/ruby)




