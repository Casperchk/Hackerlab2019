* * * * *
                          Agent of OCRC- Forensic
 * * * * *

**Enoncé:** Au cours d'une investigation, les agents de l'OCRC (Office Central de Répression de la Cybercriminalité) ont récupéré un ordinateur. Après des fouilles, il semble que le suspect soupçonné de pédophilie et de détention d'images à caractère pédopornographique ait effacé les images compromettantes. Néanmoins, les agents de l'OCRC ont pu récupéré un fichier crucial. Aide-les dans leur enquête, cyber-amazone.

Le but de cette épreuve est d'aider les agents de l'OCRC dans leur enquête en investiguant le fichier. Inspectons le fichier avec **binwalk**:

`$ binwalk file`

>DECIMAL   HEXADECIMAL  DESCRIPTION
>-------------------------------

>2072 0x818 JPEG image data, JFIF standard 1.01

Nous pouvons remarquer la présence d'un format de fichier **JPEG** à l'intérieur. Nous allons donc l'extraire pour voir:
`$ dd bs=1 skip=2072 if=file > foo.jpeg`

Maintenant nous ouvrons l'image **foo.jpeg** extrait et bingo nous avons le flag: **CTF_MouisTuEsUnVraiguerrier**


