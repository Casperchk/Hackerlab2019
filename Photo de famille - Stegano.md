* * * * *
                   Photo de famille - Steganography
  * * * * *

**Enoncé:** Un souvenir inoubliable!

Une image est mise à notre disposition. Nous devons extraire les données cachées à l'intérieur.

Essayons d'avoir des infos sur l'image:

`$ steghide info amazones.jpg `
>"amazones.jpg":
  format: jpeg
  capacité: 3,6 KB
Essayer d'obtenir des informations à propos des données incorporées ? (o/n) o
Entrez la passphrase: (nous validons juste)
  fichier � inclure "flag.txt":
    taille: 23,0 Byte
    cryptage: rijndael-128, cbc
    compression: oui

Nous remarquons qu'il y a un fichier **flag.txt** caché à l'intérieur, nous allons l'extraire:

`$ steghide --extract -sf amazones.jpg`
> Entrez la passphrase: (nous validons un mot de passe vide)
Ecriture des données extraites dans "flag.txt".

On ouvre le fichier **flag.txt** et nous avons le flag:
**CTF_YOUROCKTAKEYOURFLAG**

