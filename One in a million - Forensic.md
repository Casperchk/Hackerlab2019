* * * * *
                        One in a million - Forensic                
* * * * *

**Enoncé:** Télécharge le fichier et trouve la flag.

Le but est donc de trouver le flag de validation

Apres avoir téléchargé le fichier, et extrait avec `tar xf file` on voit que l'archive contenait une image **chal.img**

Examinons le contenu avec **binwalk**:

`$ binwalk chal.img`


DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
> 2121728       0x206000        Zip archive data, at least v1.0 to extract, name: one_in_a_million/
2121803       0x20604B        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/212
2121895       0x2060A7        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/211
2121987       0x206103        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/210
2122079       0x20615F        Zip archive data, at least v1.0 to extract, compressed size: 13, uncompressed size: 13, name: one_in_a_million/21
                ....................................................
                ....................................................
                
>2213226       0x21C56A        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/908
2213318       0x21C5C6        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/907
2213410       0x21C622        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/906
2213502       0x21C67E        Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one_in_a_million/905
2303574       0x232656        End of Zip archive, footer length: 22

On remarque que l'image contient une archive à l'adresse **2121728** qui contient d'autre archives. Nous allons l'extraire avec l'outil **dd**:

`$ dd if=chal.img bs=1 skip=2121728 of=zoo.zip`
> 3018131 octets (3,0 MB, 2,9 MiB) copiés, 7 s, 431 kB/s 3121152+0 enregistrements lus 3121152+0 enregistrements écrits 3121152 octets (3,1 MB, 3,0 MiB) copiés, 7,23628 s, 431 kB/s

On ouvre l'archive **zoo.zip**, il contient assez de fichiers. Essayons de rechercher le mot clé *CTF* à l'interieur: 
`$ strings zoo.zip | grep CTF` 
> CTF_FOuineURDeCLes

Bingo!! Voila donc le flag  **CTF_FOuineURDeCLes**.

