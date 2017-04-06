---
layout: post
title:  "Spans and Listeners"
date:   2017-04-06 13:16:00 +0000
---


This week I did a small scale blog about a feature in my recent javascript project. The feature allows a user to break up an unstructured bunch of sentences into defined paragraphs by option clicking the sentence on which to start a new paragraph. It’s really easy to do an relies primarily on the <span> tag.

The <span> tag is a generic container for other elements that has no inherent visual representation. It’s kind of like a <div>, except it’s inline. That means we can insert it in the middle of a sentence and it won’t change the visual flow. In the paragraph example, I build a helper function that wrapped each sentence in a <span> with a datatype ’s’.


```
static spanFormat(text, index) {
    let startTag = `<span data-type="s" data-id="${index}" >`
    let closeTag = '</span>'
    let wordArr = text.split(" ")
    wordArr.push(closeTag)
    wordArr.unshift(startTag)
    return wordArr.join(" ")
  }
```

When generating the text for our paragraph view, I encased them in spans with a data-id of S. After that, all I had to do was affix an event listener to the text div. When a click happens, the listener inserts a closing and beginning paragraph tag at the start of the event.target sentence, creating a paragraph break. I formatted the <spans> with data-id s to turn light blue upon mouse hover, a nice visual to demarcate sentence breaks. 

Here’s the event listener. It sets an event listener for whenever the “alt” key is pressed.

```
$(window).keydown((e) => {
      if (e.key == "Alt") {
        $('p').on("click", (event) => {
          let $paragraphBreak = event.target
          if ($paragraphBreak.dataset.type == 's') {
            $( '</p><p>' ).insertBefore( $paragraphBreak )
          } else {
          }
        })
      } else {
      }
    })
```

This is a simple example, but I think this technique could be used in more powerful ways with regex. You could build a helper method that encases given phrases in invisible spans for later functionality and formatting. You can think of them as JavaScript hyperlinks. I’ll upload the live code soon.
