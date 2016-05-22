---
layout: post
title:  Why python comprehensions are the best thing since sliced bread
tags:
- python
- functional
---

Ever since I've picked up [Perl](http://metacpan.org/author/GIDEON) and Python in my free time, I strongly believe in what [Bjarne Stroustrup says here](http://www.youtube.com/watch?v=NvWTnIoQZj4) : "Nobody should call themselves a professional if they only know one language. Five is a good number."

When I came across [Linq](http://en.wikipedia.org/wiki/Language_Integrated_Query), I thought haughtily how C# was so superior to other languages, unfortunately I didn't know Python then.

So after learning Python comprehensions from [this coursera course I took](https://www.coursera.org/course/matrix), I got so excited and amazed.  Python comprehensions now are the best thing since sliced bread in my book.

Here is a quick overview of what you can do with python comprehensions.

Python has a built in _dictionary_, _list_, _set_ and _tuple_. Essentially a comprehension is a succinct way to evaluate or generate one of these structures.

Download the [latest python](http://python.org/download/releases/3.3.2/). Whatever platform you're in, open a Command Prompt window, and type python, and follow the snippets below. Note: Macs come pre-installed with python, just open the terminal and type python.


<script src="https://gist.github.com/gideondsouza/6460345.js"></script>

For a line like this : `[x for x in range(10)]` . range(N) returns an enumerable or "loopable" structure. The portion between the `[` and the `for` is where you can use x and do pretty much anything with it or return some expression.

Here is a dumb counter example : `[5 for x in range(5)]`. This will generate a list : `[5, 5 , 5 , 5 ,5]`. If you did this : `[x*5 for x in range(5)]`. You'll get multiples of five.

Hopefully you've got a hang of it. Now you can add some decisions while building your list.

<script src="https://gist.github.com/gideondsouza/6460422.js"></script>

Now I shall introduce the set date type. A set in python is an unordered list of **unique** items.  Note: to create an empty set you do : `s = set()`.  If you do this `x={}` x becomes a dictionary. Here is the [python docs for a set.](http://docs.python.org/3/tutorial/datastructures.html#sets)

<script src="https://gist.github.com/gideondsouza/6460529.js"></script>

Next, another important type is the tuple, here are the python docs on tuples :

<script src="https://gist.github.com/gideondsouza/6460607.js"></script>

Now lets get funky and use two loops in our comprehension to generate permutations and combinations of the numbers 1 to 5

<script src="https://gist.github.com/gideondsouza/6460685.js"></script>

Have I got you convinced!?
