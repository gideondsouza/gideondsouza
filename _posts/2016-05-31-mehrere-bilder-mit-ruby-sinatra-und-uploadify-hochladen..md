---
layout: post
title:  Mehrere Bilder mit Ruby, Sinatra und Uploadify hochladen.
tags:
- ruby
- web-dev
- sinatra
- uploadify
---

Das hier ist das Endprodukt:
<img src='http://i.imgur.com/jUwZVYx.png' alt="screenshot example" />

Ich knüpfe hier an den Arikel an, an welchem ich beschrieben habe wie man [Dateien mit einer Sinatra-Anwendung hochlädt](http://www.gideondsouza.com/blog/uploading-images-with-ruby-and-sinatra/).

Wir gehen weiter und wollen jetzt mehrere Dateien hochladen. Falls du schon danach gesucht hast, bist du vielleich über [uploadify.com](www.uploadify.com) gestolpert.

Dabei handelt es sich um ein flash/jquery basiertes Plugin. Ich habe es vor Urzeiten benutzt. Kann sein, dass du immernoch dafür brennst respektvoll auch mal mit weniger zu leben, wenn der Browser nicht so furchtbar neu ist. Egal, sie benutzen eine kostenpflichtige html5-Version ihrer library. **Mein Code benutzt eine kostenlose Library.**

**Setup** :

* Installiere shotgun damit du die Sinatra-App nicht jedesmal neuladen musst, wenn etwas verändert/debuggt wurde
        $ gem install shotgun
* Downloade das kostenlose uploadify-Plugin : [http://www.uploadify.com/download/](http://www.uploadify.com/download/)
* Unzippe die uploadify-Zip in einen _/public_ Ordner. Lege darin einen _/img_ Ordner an, uplodify erwartet, dass die "Abbrechen"-Schaltfläche von hier kommt.

Deine directory sollte in etwa so aussehen:

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

Das Eingemachte befindet sich in den zwei Ordnern _img_mgr.rb_ und _form_multiple.erb_

Hier ist unsere Sinatra-App:

<!-- <script src="https://gist.github.com/gideondsouza/59f1d9ccb2551d0c06e8c47351a063f8.js"></script> -->
[img_mgr.rb](https://gist.github.com/gideondsouza/59f1d9ccb2551d0c06e8c47351a063f8) :

    require 'sinatra'

    get '/' do
      erb :form_multiple
    end

    post '/upload' do
    #this method will get as ajax call for every file uploaded
      @filename = params[:Filename]
      file = params[:Filedata][:tempfile]

      File.open("./public/#{@filename}", 'wb') do |f|
        f.write(file.read)
      end

      #return filename as the response, the file we just wrote.
      return @filename
    end

Die Homepage route _'/'_ bedient die _form_multiple.erb_-Datei. uploadify benutzt diese um sich selbst einzurichten. uploadify sendet Anfragen an die _'/upload'_ route. Hier drinnen kommen wir an die Dateinamen von _params[:Filename]_ und dem Datenobjekt (file object) von _file = params[:Filedata][:tempfile]_. (Wen es interessiert, wie ich das rausgefunden habe - Ich habe einfach "_puts params_" in die route geschrieben, das Parameterobjekt (params object) wird dann in die Console ausgegeben und so kannst du dir das Objekt auch selbst anschauen). Ich schreibe die Datei in den  _/public_ -Ordner. Benutzt werden kann es von der root von wo auch immer das ganze liegt, also gehostet wird.

Die Ansicht sieht dann so aus:

[form_multiple.erb](https://gist.github.com/gideondsouza/1367104cfc8a83c4b5c924fe467d6032#file-form_multiple-erb) :
<!-- <script src="https://gist.github.com/gideondsouza/1367104cfc8a83c4b5c924fe467d6032.js"></script> -->

    <html>
        <head>
            <title>Image Upload</title>
            <link rel="stylesheet" type="text/css" href="uploadify.css" />
            <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
            <script type="text/javascript" src="jquery.uploadify.min.js"></script>
        </head>
        <body>

            <h1>Upload Images</h1>

            <input type="file" name="file_upload" id="file_upload" />
            <script>
            $(function() {
              $('#file_upload').uploadify({
                  'swf'      : 'uploadify.swf',
                  'uploader' : '/upload',
                  'onUploadSuccess' : function(file, data, response) {
                      $("#images").append("<img src='/" + data + "' height='100px'/>");
                  }
                });
            });
        </script>
        <div id="images">
        <strong>Uploaded images here:</strong><br />
        </div>
        </body>
    </html>

In unserer Server-(Sinatra-)App geben wir die Dateinamen als eine response (Antwort) zurück, und genau dieses gibt uns die uploadify-Plugin über das _onUploadSuccess_-Steuerungsprogramm (handler). Das fügt einen Bild-tag zu unserer voreingestellten div hinzu.

Das ist dann alles, was du brauchst um das ganze auszuführen :

      $ shotgun img_mgr.rb

Wenn das ganze in einem schönen downloadfähigen Packet benötigt wird, [kann man es hier finden](/assets/image_manager.zip).

Und wie immer: Feel free Fragen oder Kommentare zu schreiben.
