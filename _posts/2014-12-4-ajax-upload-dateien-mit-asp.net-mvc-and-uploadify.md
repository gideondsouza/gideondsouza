---
layout: post
title:  ajax upload-Datein mit asp.net-mvc und uploadify
tags:
- asp.net-mvc
- ajax
- uploadify
---

Nachdem ich eine Frage auf Stackoverflock dazu beantwortet habe, ist mir klar geworden, dass das Hochladen mit ajax etwas ist, wonach alle bisher gesucht hatten.

Ich habe gerade erst den [asp.net-mvc badge][1] Badge gewonnen und das will natürlich gefeiert werden - deswegen werde ich hier ein umfassendes Beispiel geben, wie man eben das mit asp.net-mvc macht.

Ich werde das [uploadify jquery plugin][2] benutzen. Es gibt aber auch [viele andere][3] die man dafür nutzen kann.

Alles in allem ist es ziemlich einfach. Wir werden etwas erstellen, dass dann in etwa so aussehen wird:

![Asp.net-mvc Ajax Upload screenshot][4]

Damit kannst du mehrere Dateien auswählen, die dann asynchron hochgeladen werden. Dann wird ein Link an die Datei angefügt, in der Annahme, dass es sich dabei um ein Bild handeln würde.

Ich habe ein Bild von meinem [Arduino Starter Kit][5] hochgeladen :)

## How to / Anleitung

1. Erstelle eine neue asp.net mvc4 web-Anwendung.
2. Lösche die `Index.cshtml` Seite unter `\View\Home\`.
3. Öffne den `HomeController.cs` und rechtsklicke auf die `Index()`-Methode.
4. Klicke auf Add View, und entferne das Häkchen bei _Use a Layout oder Master Page_.

erstelle eine upload-Methode wie im folgenden code snippet.
Dein [HomeController.cs](https://gist.github.com/gideondsouza/4284314#file-homecontroller-cs) solte so aussehen:

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

**Anmerkung** : Uploadify benennt die Dateien, die es sendet als "Filedata".

Die Ansicht [Index.cshtml](https://gist.github.com/gideondsouza/4284335) sollte in etwa so aussehen. Verschiebe deine js-Dateien aus der uploadify.zip nach `/Scripts` und pngs und css nach `/Content` in deinem asp.net-mvc-Projekt :

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
                    //hier postet die datei, wenn sie hochgeladen wird
                    'uploader': "@Url.Action("Upload", "Home")",
                    'onUploadSuccess' : function(file, data, response) {
                      //daten sind wasimmer man vom server zurueckbekommt
                      //wir senden die URL vom server und haengen es als bild an die #uploaded div
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


Anmerkung: Ich musste die css in  uploadify.css ändern, so dass line 74 richtig auf die uploadify-cancel.png zeigt.

    74:   background: url('../Content/uploadify-cancel.png') 0 0 no-repeat;

Schau dir doch auch [diesen Artikel an, um das Ganze mit Ruby zu machen :)](http://www.gideondsouza.com/blog/uploading-multiple-images-with-ruby-and-sinatra-and-uploadify/)
<!-- Und das wars!!! Ich habe ein komplettes Beispiel, dass du [hier downloaden][6]kannst. -->


  [1]: http://stackoverflow.com/badges/310/asp-net-mvc?userid=368070
  [2]: http://www.uploadify.com
  [3]: http://www.webdeveloperjuice.com/2010/02/13/7-trusted-ajax-file-upload-plugins-using-jquery/
  [4]: http://i.imgur.com/Hm2R6sw.png
  [5]: https://www.sparkfun.com/products/9284
  [6]: http://gideondsouza.com/Media/Default/Misc/UploadifyExample.zip
