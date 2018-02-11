---
layout: post
title:  The dawn of the micro web frameworks, introducing dancer
date:   2013-09-10
tags:
- web-dev
- dancer
---

Turns out micro-frameworks are really _**in**_ these days, there is:

* [Sinatra](http://www.sinatrarb.com/) for Ruby (This is grand daddy that inspired everyone else)
* [Dancer](http://www.perldancer.org/) for Perl
* [Flask](http://flask.pocoo.org/) for Python
* [Nancy](http://nancyfx.org/) for .NET
* [Scotty](http://www.ittc.ku.edu/csdl/fpg/software/scotty.html) for Haskell

I've been using Dancer pretty often, I recently built http://www.perlmonksflair.com  with it.

So this is what a simple dancer app looks like:

Save the following in my_app.pl

<script src="https://gist.github.com/gideondsouza/6508444.js"></script>

Then in your command line:

    $ perl my_app.pl &
    ...
    $ curl http://localhost:3000/
    Hello world!

If you know enough web development you probably get it. This line `get '/' => sub {}` registers the url : / with a subroutine, or more correctly a coderef (a reference to a subroutine)

That means the homepage (like www.example.com/) will show "Hello world" in the browser.  (In perl the last statement in sub will be the return value)

Now lets get to something more complicated. Need a webservice, just use this plugin [Dancer::Plugin::REST](https://metacpan.org/module/Dancer::Plugin::REST). This sample is copied straight from the POD for that plugin :P

<script src="https://gist.github.com/gideondsouza/6508454.js"></script>

Note if you individually needed to add a route that returned json you could always use to [to_json](https://metacpan.org/module/Dancer#to_json-structure-options) method from within a sub.

Need to do github authentication in your application? Simple use this plugin [Dancer::Plugin::Auth::Github](https://metacpan.org/module/Dancer::Plugin::Auth::Github), yes I wrote this one! :

<script src="https://gist.github.com/gideondsouza/6508472.js"></script>

Yes there is a plugin to do authentication for twitter, [and more plugins to do other cool stuff](https://metacpan.org/search?q=Dancer%3A%3APlugin) too.

So what are you waiting for? Go and dance your way into an awesome web application.
