
*****                                   
									  Hello Hackerlab
*****

**Enoncé:** Aucun

Cette épreuve nous donne un fichier **hello-hackerlab.crx** a télécharger. Après le téléchargement on l'analyse avec **binwalk** : 

    $ binwalk hello-hackerlab.crx 
**Résultat:**

    DECIMAL       HEXADECIMAL     DESCRIPTION
    --------------------------------------------------------------------------------
    593           0x251           Zip archive data, at least v2.0 to extract, compressed size: 2, name: styles/
    632           0x278           Zip archive data, at least v2.0 to extract, compressed size: 321, uncompressed size: 590, name: main.js
    990           0x3DE           Zip archive data, at least v2.0 to extract, compressed size: 157, uncompressed size: 251, name: manifest.json
    1190          0x4A6           Zip archive data, at least v2.0 to extract, compressed size: 144, uncompressed size: 205, name: index.html
    1374          0x55E           Zip archive data, at least v2.0 to extract, compressed size: 15776, uncompressed size: 15771, name: icon_128.png
    17192         0x4328          Zip archive data, at least v2.0 to extract, compressed size: 1100, uncompressed size: 1095, name: icon_16.png
    18333         0x479D          Zip archive data, at least v2.0 to extract, compressed size: 2, name: assets/
    18372         0x47C4          Zip archive data, at least v2.0 to extract, compressed size: 23606, uncompressed size: 23603, name: hello_world.png
    42023         0xA427          Zip archive data, at least v2.0 to extract, compressed size: 88, uncompressed size: 116, name: sample_support_metadata.json
    42169         0xA4B9          Zip archive data, at least v2.0 to extract, compressed size: 285, uncompressed size: 470, name: styles/main.css
    42499         0xA603          Zip archive data, at least v2.0 to extract, compressed size: 466723, uncompressed size: 466919, name: assets/screenshot_1280_800.png
    509943        0x7C7F7         End of Zip archive, footer length: 22

Après analyse on remarque que le fichier était en faite une archive contenant plusieurs fichiers. Il ne reste plus qu'à extraire cette archive:

    $ dd if=hello-hackerlab.crx bs=1 skip=593 > hello-hackerlab.zip

**Résultat:**

    509372+0 enregistrements lus
    509372+0 enregistrements écrits
    509372 octets (509 kB, 497 KiB) copiés, 0,984453 s, 517 kB/s

Fin d'extraction.
Dans ce fichier zip extrait nous avons l’architecture entier d'un site 
En visionnant c'est fichier on tombe sur le fichier **main.js** avec un contenu très intéressant :

```javascript
chrome.app.runtime.onLaunched.addListener(function() {
  // Center window on screen.
  var screenWidth = screen.availWidth;
  var screenHeight = screen.availHeight;
  var width = 500;
  var height = 300;
  //console.log("43,54,46,5f,59,6f,75,57,69,6e,54,68,65,43,68,72,6f,6d,65,41,70,70,52,65,76,65,72,73,65,42,65,67,69,6e,6e,65,72,42,61,64,67,65");

  chrome.app.window.create('index.html', {
    id: "helloWorldID",
    outerBounds: {
      width: width,
      height: height,
      left: Math.round((screenWidth-width)/2),
      top: Math.round((screenHeight-height)/2)
    }
  });
});
```
Nous remarquons le commentaire d'un code qui log une donné en hexadécimal :
```javascript
//console.log("43,54,46,5f,59,6f,75,57,69,6e,54,68,65,43,68,72,6f,6d,65,41,70,70,52,65,76,65,72,73,65,42,65,67,69,6e,6e,65,72,42,61,64,67,65");
```
L'information `43,54,46,5f,59,6f,75,57,69,6e,54,68,65,43,68,72,6f,6d,65,41,70,70,52,65,76,65,72,73,65,42,65,67,69,6e,6e,65,72,42,61,64,67,65` est sûrement le flag nous allons le décoder avec [asciitohex](https://www.asciitohex.com/). Le flag de validation est : 

**CTF_YouWinTheChromeAppReverseBeginnerBadge**


