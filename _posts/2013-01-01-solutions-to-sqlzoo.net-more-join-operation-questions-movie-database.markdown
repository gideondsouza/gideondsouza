---
layout: post
title: Solutions to sqlzoo.net More Join Operation Questions (Movie Database)
tags:
- sql
---

While meandering around the web for sql exercises and tutorials I came across [www.sqlzoo.net][1].

It is the perfect place to get hands on knowledge for SQL, especially JOINS!

Below are solutions to all the questions on the [More JOIN Operations][2] tutorial. Questions 1-6 are plain straightforward. Questions 7-11 are basic join questions and 12-16 and pretty hard. I ended up spending quite some time trying to solve the last bunch.

Here are all the solutions in case you got stumped. (I just included all questions for completeness)


### Problem 1 : List the films where the yr is 1962 [Show id, title]
This one is pretty straightforward.

<script src="https://gist.github.com/3551780.js"> </script>

### Problem 2 : Give year of 'Citizen Kane'.
This one too :

<script src="https://gist.github.com/3551783.js"> </script>

### Problem 3 : List all of the Star Trek movies, include the id title and yr. (All of these movies include the words Star Trek in the title.)

<script src="https://gist.github.com/3551454.js"> </script>

### Problem 4 : What are the titles of the films with id 11768, 11955, 21191

<script src="https://gist.github.com/3551463.js"> </script>

### Problem 5 : What id number does the actor 'Glenn Close' have?

<script src="https://gist.github.com/3551476.js"> </script>

### Problem 6 : What is the id of the film 'Casablanca'

<script src="https://gist.github.com/3551479.js"> </script>

------
## Real join questions begin :

### Problem 7 : Obtain the cast list for 'Casablanca'. Use the id value that you obtained in the previous question.

<script src="https://gist.github.com/3551492.js"> </script>

### Problem 8 : Obtain the cast list for the film 'Alien'

<script src="https://gist.github.com/3551529.js"> </script>

### Problem 9 : List the films in which 'Harrison Ford' has appeared

<script src="https://gist.github.com/3551537.js"> </script>

### Problem 10 : List the films where 'Harrison Ford' has appeared - but not in the star role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

<script src="https://gist.github.com/3551544.js"> </script>

### Problem 11: List the films together with the leading star for all 1962 films.

<script src="https://gist.github.com/3551556.js"> </script>
--------

## Hard Questions.
### These questions are a little bit hard. Give some time to crack them before looking at the solutions.

### Problem 12 : Which were the busiest years for 'John Travolta'. Show the number of movies he made for each year.

<script src="https://gist.github.com/3551570.js"> </script>

### Problem 13 : List the film title and the leading actor for all of 'Julie Andrews' films.

<script src="https://gist.github.com/3551578.js"> </script>

### Problem 14 : Obtain a list of actors in who have had at least 30 starring roles. (Yep, the result set this generates is a empty set)

<script src="https://gist.github.com/3551585.js"> </script>

### Problem 15 : List the 1978 films by order of cast list size.

<script src="https://gist.github.com/3551594.js"> </script>

### Problem 16 : List all the people who have worked with 'Art Garfunkel'.

<script src="https://gist.github.com/3551605.js"> </script>

And there you have it! Hope it was helpful.


  [1]: http://www.sqlzoo.net
  [2]: http://sqlzoo.net/wiki/More_JOIN_operations
