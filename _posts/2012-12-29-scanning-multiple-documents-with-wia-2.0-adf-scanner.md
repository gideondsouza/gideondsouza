---
layout: post
title:  Scanning multiple documents with WIA 2.0 (ADF Scanner)
tags:
- csharp
- .net
- com-interop
---

So a long time ago I had to do a project that involved getting images from a scanner with an auto document feeder. It was a challenge doing this with WIA ([Windows Imaging Aquisation](https://en.wikipedia.org/wiki/Windows_Image_Acquisition)) but I found some code somewhere online and made it into a nice library.

Today I finally shared this library with the world here: [http://adfwia.codeplex.com/][1]  
[**Update**-15Dec2011]: I put it up on github too: [https://github.com/gideondsouza/AutoDocumentFeed_for_WIA][2]


It includes the source under the MIT License, it also has a little test app you can play with.

**Note**: Some scanners have trouble with the DIP setting. If you get: `Unhandled Exception : Value does not fall within range.`

Try a higher or lower DPI.

![ADF-Scanner-App][3]


  [1]: http://adfwia.codeplex.com/
  [2]: https://github.com/gideondsouza/AutoDocumentFeed_for_WIA
  [3]: http://i.imgur.com/wHoqull.jpg
