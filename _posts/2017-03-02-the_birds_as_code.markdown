---
layout: post
title:  "The Birds as Code"
date:   2017-03-02 21:24:46 +0000
---


I started a 3 month coding program at the Flatiron School at the beginning of the month. They’ve encouraged me to keep a blog about the things I’ve been learning and thinking about. I’ve worked in music and film scoring for quite a while now, and I’ve taken on a certain mindset about creativity and artistry that doesn’t quite translate to the coding world. I wanted to explore it here a bit.

Last month, I watched The Birds for the first time. It is about an isolated coastal town that gets taken over by swarms of killer birds. You can read all kinds of meaning into it, but I found myself seeing it as a battle between the individual and the group, the networked and the local. The birds attack en mass, one bird indecipherable from the other, and the humans under attack, each an individual, can only run and hide from the complexity of the hive.
This battle between the individual and the group feels representative of a tension I’ve felt between music and coding (definitely a tension that I like). In music, individuality is the end goal. Artistry on the highest level means writing and playing in an unmistakable voice, even when interpreting other people’s work. But it’s almost the opposite when writing code. Senior Google developer Nina Kang describes the hallmarks of great code as having a ‘self-documenting’ clarity and precision. That means the code speaks for itself. It doesn’t need comments to explain how it works. Self-documenting writing is so clear and efficient because it removes all unnecessary information. And what is unnecessary? Things like ambiguity, repetition, distinct phrasing, irony… all the idiosyncrasies that you could say constitute an individual’s style. She describes the best code as being almost anonymously written.

I don’t mean to suggest the two are in conflict or that the tension between them is a horror story. It’s actually a freeing feeling to be able to practice both. The networked world will only grow more connected, and I’m excited to learn a more selfless idea of creativity, of open source commitment to projects that can exceed the scope of any individual working alone. That’s a powerful motivating force when struggling against the difficulty of learning code.
I thought I’d end, logically, with an exit. In Ruby “exit”, will quit Ruby from where ever you are in a program. It’s nice to have if you happen to be stuck within several methods. Just call a method with exit.

```
def this_will_exit_ruby_from_anywhere
  exit
end
Also of note is “at_exit”, a nice little feature that will run a method anytime you exit a program
at_exit do
  puts "and so are you!"
end
puts "I am a program"
```

If you run the above code, you’ll get “I am a program and so are you!” It can be useful if you need to delete temporary files or reset a database a the end of a program.

