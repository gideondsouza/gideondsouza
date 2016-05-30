---
layout: post
title:  How to get the current location, address and send it to a server on android
tags:
- asp.net-mvc
- ajax
- uploadify
---

After answering a question on stackoverflow I realized uploading files with ajax was something everyone was looking for.

So to commemorate the [asp.net-mvc badge][1] I won recently I'm writing a full example of how to do this with asp.net-mvc.

I'll use the [uploadify jquery plugin][2]. There are [many others][3] you can use too.

So all in all it's pretty simple. We'll create something that looks like this:

![Asp.net-mvc Ajax Upload screenshot][4]

It allows you to select multiple files, uploads them asynchronously. Then appends a link to the file, assuming it's an image.

I uploaded a picture of my [Arduino Starter Kit][5] :)

## How to :

1. Create a new asp.net mvc4 web application.
2. Delete the `Index.cshtml` page under `\View\Home\`.
3. Open `HomeController.cs` and Right Click the `Index()` method.
4. Click Add View, and uncheck _Use a Layout or Master Page_.

Create an upload method like the following code snippet.
Your home controller should look like this:

<script src="https://gist.github.com/4284314.js"></script>

**Note** : Uploadify names the file it sends as 'Filedata'.

For the view it should look like this:

<script src="https://gist.github.com/4284335.js"></script>

Note : I had to change the css in uploadify.css, line 74 to point to the uploadify-cancel.png correctly.

    74:   background: url('../Content/uploadify-cancel.png') 0 0 no-repeat;

And that's it!!! I have a full sample you can [download here][6].


  [1]: http://stackoverflow.com/badges/310/asp-net-mvc?userid=368070
  [2]: http://www.uploadify.com
  [3]: http://www.webdeveloperjuice.com/2010/02/13/7-trusted-ajax-file-upload-plugins-using-jquery/
  [4]: /Media/Default/BlogPost/blog/ajax_upload_mvc_uplodify.PNG
  [5]: https://www.sparkfun.com/products/9284
  [6]: http://gideondsouza.com/Media/Default/Misc/UploadifyExample.zip
