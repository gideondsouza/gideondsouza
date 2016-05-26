---
layout: post
title:  How to authenticate with oauth in perl (Dancer, GitHub, LWP::UserAgent)
tags:
- perl
- web-dev
---

I've been playing with perl a lot lately and after recently playing with Catalyst, I moved on to Dancer.

Dancer has a [nice tutorial][1] with a [simple dummy blog application. The app is on GitHub here][2]. It describes quite a few aspects about Dancer, including sessions, routes, storage and displaying pages.

It's a neat little example in that it's hardly a few files.

Naturally I wanted to get my hands dirty and wanted to try and implement OAuth authentication with github. I don't mean by pulling a nice CPAN module (there isn't one) but writing the whole OAuth flow myself. Fortunately I found this to be a simple task.

I managed to change the authentication in the sample dancer app to login with github. [I added this in a forked project.][3]

So I'm going to describe the following:

* Use [LWP::UserAgent][4] to make requests to github
* Use [JSON::Parse][5] to gather the response from GitHub
* Set a session object to the username and avatar img url and use this on the masterpage (main.tt).

So you can see the forked project files. I just changed [dancr.pl][6] and [main.tt][7]. I also removed `login.tt` since there is no need for that. You have to [add your application with github][8] and then you'll get a `client id` and `client secret`.

### Step 1 :
 To login you have to redirect to `https://github.com/login/oauth/authorize` with the following params : `YOUR CLIENT ID`, `redirect url`, `scope` (these are permissions you want) and finally `state` which is used to prevent [cross-site request forgery attacks][9]

  <script src="https://gist.github.com/4407530.js"></script>

 I added two variables on the top and the login route changes to **just** redirect the user to githubs login page. If the user allows your app, then github will send a special `code` to your app by calling your **callback url**.


### Step 2 :
 Goto your `Github > Account Settings -> Applications -> Your App -> Callback Url`. **Note** you can set this to localhost byt specifying it like this `127.0.0.1:<SOMEPORT>`. I setup this url to `/auth/github/callback`. So in my `dancr.pl` I added this route, hopefully the comments should be a good explanation:

 <script src="https://gist.github.com/4407631.js"></script>

 This route sub uses a helper method that looks like the following, it parses the query string into a hash.

 <script src="https://gist.github.com/4407649.js"></script>

### Step 3 :
 The above step adds a few session variables if all goes well, so I then use these in the main.tt page like this:

 <script src="https://gist.github.com/4407696.js"></script>

And that's about it. If all goes well your homepage should look like this:

![Dancr screenie][10]

Any comments, feedback and insults about this article are very welcome! :)

  [1]: http://search.cpan.org/dist/Dancer/lib/Dancer/Tutorial.pod
  [2]: https://github.com/PerlDancer/dancer-tutorial
  [3]: https://github.com/gideondsouza/dancer-tutorial
  [4]: http://search.cpan.org/~gaas/libwww-perl-6.04/lib/LWP/UserAgent.pm
  [5]: https://metacpan.org/module/JSON::Parse
  [6]: https://github.com/gideondsouza/dancer-tutorial/blob/master/dancr.pl
  [7]: https://github.com/gideondsouza/dancer-tutorial/blob/master/views/layouts/main.tt
  [8]: https://github.com/settings/applications
  [9]: http://www.codinghorror.com/blog/2008/09/cross-site-request-forgeries-and-you.html
  [10]: http://i.imgur.com/Or4ksr7.png
