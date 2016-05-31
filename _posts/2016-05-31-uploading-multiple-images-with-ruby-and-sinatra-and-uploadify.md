---
layout: post
title:  Uploading multiple images with Ruby, Sinatra and Uploadify.
tags:
- ruby
- web-dev
- sinatra
- uploadify
---

This is the finished product:
<img src='http://i.imgur.com/jUwZVYx.png' alt="screenshot example" />

I'm continuing off from this article where I describe how to just [upload files in a Sinatra application](http://www.gideondsouza.com/blog/uploading-images-with-ruby-and-sinatra/).

We'll move forward to now uploding multiple files. If you've been searching for this you may have come across [uploadify.com](www.uploadify.com)

It's a flash/jquery based plugin. I've used it in ancient times. Yes you may still flash to gracefully degrade if the browser isn't all that new. However, they have a paid html5 version of their library. **My code uses the free library.**

**Setup** :

* Install shotgun so you don't have to reload your Sinatra app everytime you change/debug

        $ gem install shotgun
* Download the free uploadify plugin : [http://www.uploadify.com/download/](http://www.uploadify.com/download/)
* Extract the uploadify zip into a _/public_ folder. Inside it put an _/img_ folder, uplodify expects the cancel button image to come out of here.

Your directory should look like this:

    [gideon@gideon-fedora image_manager]$ tree
    .
    ├── img_mgr.rb
    ├── public
    │   ├── img
    │   │   └── uploadify-cancel.png
    │   ├── jquery.uploadify.js
    │   ├── jquery.uploadify.min.js
    │   ├── license.txt
    │   ├── uploadify.css
    │   └── uploadify.swf
    └── views
        └── form_multiple.erb

    3 directories, 8 files

All our meat is in two files _img_mgr.rb_ and _form_multiple.erb_

Here is our sinatra app:

<script src="https://gist.github.com/gideondsouza/59f1d9ccb2551d0c06e8c47351a063f8.js"></script>

The home page route _'/'_ serves the _form_multiple.erb_ file. This will use uploadify to set itself up. It will make requests to the _'/upload'_ route. In here we get the filename from _params[:Filename]_ and the file object from _file = params[:Filedata][:tempfile]_. If you want to know how I figured this out, I simple wrote in _puts params_. This gets printed into the console and you can check out the object yourself then. I write the file into the _/public_ folder. It can be served them from the root of the wherever this is hosted.

The view looks like this:

<script src="https://gist.github.com/gideondsouza/1367104cfc8a83c4b5c924fe467d6032.js"></script>

If you notice in our server(sinatra) app we return the filename as a response, this is what the uploadify plugin will give us in the _onUploadSuccess_ handler. All we do it append an image tag into our predefined div.

To execute all you need to do is :

      $ shotgun img_mgr.rb

If you need the whole thing in a nice downloadable package, [here it is](/assets/image_manager.zip).

Feel free to post any questions or comments.
