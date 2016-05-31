---
layout: post
title:  Uploading images with Ruby, Sinatra and Uploadify
tags:
- ruby
- web-dev
- sinatra
---

So if you may have noticed, I have a thing for [micro frameworks](http://www.gideondsouza.com/blog/the-dawn-of-the-micro-web-frameworks-introducing-dancer/).

I've recently taken the step to learning Ruby. I've usually found that reading long books, and guides tend to be boring and not very pratical. You can do 80% of what is done in a language by learning the important 20%. (Something on the lines of the [Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle))

I start always with the aim to **do** something in any programming language I'm learning. This way I learn the important 20%.

Most of development today is focused on web development, invariably, at some point you want to build a web-app. Micro frameworks are a great way to start.

So I played a little with Ruby and [Sinatra](sinatrarb.com) and decided to build something of a file manager, maybe integrate it into dropbox, we'll see.

**This is the first round** of that plan, a simple little web-app that uploads images into a folder and then shows you the image once you've uploaded it.

Make sure you have ruby and install sinatra like this:

    gem install sinatra

Your files should look like this (the code is below):

    [gideon@gideon-fedora image_manager]$ tree
    .
    ├── img_mgr.rb
    ├── public
    └── views
        ├── form.erb
        └── show_image.erb

A quick rundown:

* Sinatra serves static files from a folder named _public_. We'll write our image into this folder.
* We'll use erb, yes there are [so wow so much views engines](http://www.sinatrarb.com/intro.html#Available%20Template%20Languages). The cool kids seem to like Haml.
* We have two routes (1) _'/'_ and (2) _'/show_image'_ corresponding to our views with will serve the upload (1) _form.erb_ and then show the image with _show_image.erb_

Here comes the code :

<script src="https://gist.github.com/gideondsouza/fc7e990030b17884d79efb28b74ced2e.js"></script>

<script src="https://gist.github.com/gideondsouza/f3a55300cc1002054fdf17ddd2468e38.js"></script>

<script src="https://gist.github.com/gideondsouza/aa2396b5cd59429f4a082b05f4c8bc3f.js"></script>


Hopefully most of this will look self-explainatory and help you get your hands dirty. I'm going to try and make this a series where I eventually develop this into a little bit of an actual app.
