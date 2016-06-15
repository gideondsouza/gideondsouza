---
layout: post
title:  ajax upload files with asp.net-mvc and uploadify
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
Your [HomeController.cs](https://gist.github.com/gideondsouza/4284314#file-homecontroller-cs) should look like this:

    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }
        public ActionResult Upload()
        {
            var file  = Request.Files["Filedata"];
            string savePath = Server.MapPath(@"~\Content\" + file.FileName);
            file.SaveAs(savePath);

            return Content(Url.Content(@"~\Content\" + file.FileName));
        }
    }

**Note** : Uploadify names the file it sends as 'Filedata'.

For the view [Index.cshtml](https://gist.github.com/gideondsouza/4284335) should look like the following. Put your js/css etc files from the uploadify.zip into `/Scripts` in your asp.net-mvc project :

    @{
        Layout = null;
    }
    <!DOCTYPE html>
    <html>
    <head>
        <meta name="viewport" content="width=device-width" />
        <title>::Uploadify Example::</title>
        <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
        <script type="text/javascript" src="@Url.Content("~/Scripts/jquery.uploadify-3.1.min.js")"></script>
        <link rel="stylesheet" type="text/css" href="@Url.Content("~/Content/uploadify.css")" />
        <script type="text/javascript">
            $(function () {
                $('#file_upload').uploadify({
                    'swf': "@Url.Content("~/Content/uploadify.swf")",
                    //this is where the file posts when it uploads.
                    'uploader': "@Url.Action("Upload", "Home")",
                    'onUploadSuccess' : function(file, data, response) {
                      //data is whatever you return from the server
                      //we're sending the URL from the server so we append this as an image to the #uploaded div
                               $("#uploaded").append("<img src='" + data + "' alt='Uploaded Image' />");
                    }
                });
            });
        </script>
    </head>
    <body>
        <div>
            Click Select files to upload files.
            <input type="file" name="file_upload" id="file_upload" />
        </div>
        <div id="uploaded">
        </div>
    </body>
    </html>


Note : I had to change the css in uploadify.css, line 74 to point to the uploadify-cancel.png correctly.

    74:   background: url('../Content/uploadify-cancel.png') 0 0 no-repeat;

Check out the [same article for doing this with Ruby :)](http://www.gideondsouza.com/blog/uploading-multiple-images-with-ruby-and-sinatra-and-uploadify/)
<!-- And that's it!!! I have a full sample you can [download here][6]. -->


  [1]: http://stackoverflow.com/badges/310/asp-net-mvc?userid=368070
  [2]: http://www.uploadify.com
  [3]: http://www.webdeveloperjuice.com/2010/02/13/7-trusted-ajax-file-upload-plugins-using-jquery/
  [4]: http://i.imgur.com/Hm2R6sw.png
  [5]: https://www.sparkfun.com/products/9284
  [6]: http://gideondsouza.com/Media/Default/Misc/UploadifyExample.zip
