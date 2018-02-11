---
layout: post
title:  Mehrere Dokumente mit WIA 2.0 scannen (ADF Scanner)
tags:
- csharp
- .net
- com-interop
---

Vor einiger Zeit stand ich vor dem Problem, dass ich für ein Projekt Bilder von einem Scanner mit einem automatischen Dokumenteneinzug benötigte. Die Herausforderung lag darin, das mit WIA ([Windows Imaging Aquisation](https://en.wikipedia.org/wiki/Windows_Image_Acquisition)) umzusetzen, aber ich fand tatsächlich einen Code irgendwo online und machte daraus eine schöne library.

Heute kann ich diese library hier endlich mit der Welt teilen: [http://adfwia.codeplex.com/][1]  
[**Update**-15Dec2011]: Ich hab ihn auch auf github hochgeladen: [https://github.com/gideondsouza/AutoDocumentFeed_for_WIA][2]


Sie beinhaltet die Quelle (source) unter  der MIT-Lizenz, und eine kleine Testapp mit der man herumspielen kann.

**Note**: Manche Scanner haben Probleme mit der DIP-Einstellung. Bei der Anzeige: `Unhandled Exception : Value does not fall within range.` 

Probier eine höhere oder niedrigere DPI aus.

![ADF-Scanner-App][3]


  [1]: http://adfwia.codeplex.com/
  [2]: https://github.com/gideondsouza/AutoDocumentFeed_for_WIA
  [3]: http://i.imgur.com/wHoqull.jpg
