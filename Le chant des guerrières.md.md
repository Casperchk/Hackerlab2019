*****
		           Le chant des guerrières - Stéganographie
*****
**Enoncé:** AGOODJIE ou le chant des guerrières. Les cyber-amazones entonnaient souvent ce chant sacré pour retrouver le flag caché.


Cette épreuve nous donne un fichier **chant.tar.7z** à télécharger. Après l'avoir décompresser on obtient un fichier **.mp4**  (une vidéo).

En lisant cette belle musique des guerrières amazones on aperçoit le flag mais la lecture est assez rapide pour qu'on note quoi que ce soit.
Après avoir créé une séquence d'image de la vidéo avec **ffmpeg** on arrive à lire correctement le flag.

    $ ffmpeg -i chant.mp4 -r 24 -f image2 -qscale 1 photo-%0d.jpg

  
![](https://lh3.googleusercontent.com/Vu6jGEh1eL3KQMVsmkGgqoDQ4yPGnd-RtjUnWgNH-vBy8vCcFB6znfu-dnh4sLLcXz-QL_ZSEuQ)
  
Flag de validation: **CTF_AGOODJIERENOUVELE**
