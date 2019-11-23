* * * * *
					Evil Dropper - Reverse Engineering
* * * * *

A cette épreuve est jointe une archive contenant un fichier **facture.doc** . Quand nous ouvrons le fichier avec **Microsoft Word** nous avons un avertissement qui dit que le document contient des macros. On clique sur activer pour activer l'exécution des macros. 
Allons maintenant dans le menu **Affichage** de Word puis cliquons sur `Macro` **>** `Afficher les macros`. Nous pouvons voir la macro **Auto_Open**. Cliquons sur **Exécuter pas à pas** pour exécuter la macro et l'analyser pas à pas. Nous remarquons une variable de type chaîne de caractère définie au début: 
```basic
Dim etWoxmfiCOK As String 
etWoxmfiCOK = wreDPsIVQmesmz(Array(((15 Xor 45) + 38), ((8 Xor 28) + 6), (175 Xor 16), ((81 Xor 14) + 106), (102 + (18 Xor 84)), (54 Xor 255), ((1 Xor 114) + 102), (1 + 2), (7 Xor 54), (121 Xor 2), (25 Xor 55), (104 + (0 Xor 40)), (126 + (26 Xor 88)), ((16 Xor 1) + (212 Xor 13)), (95 + (42 Xor 187)), (8 Xor 184), 63, (2 + 28), ((142 Xor 30) + 107), 110, (49 Xor 134), (7 Xor 229), (0 Xor 49), (25 Xor 150), 17, (3 + 1), 125, (90 Xor 169), (12 + 141), 96, (58 Xor 169), (49 + 58), ((0 Xor 41) + (47 Xor 78)), 173, ((4 Xor 2) + 16), ((1 Xor 13) + (45 Xor 23)), \_ ((23 Xor 59) + 82), (98 Xor 251), ((24 Xor 48) + (10 Xor 30)), (67 Xor 7), (15 + 216), 204, ((44 Xor 75) + 47), 108, ((12 Xor 36) + 12), 2, (95 + (7 Xor 15))), 0) & wreDPsIVQmesmz(Array((6 Xor 71), 216), ((5 Xor 12) + (25 Xor 63)))
```
Affichons son contenu dans une fenêtre Popup (**MsgBox**). Pour cela il suffit d'ajouter :
```basic
MsgBox(etWoxmfiCOK) 
```
tout juste après la déclaration de la variable puis d'exécuter le macro à nouveau.
Nous avons une fenêtre Popup affichant un lien: `http://guidos.hostingerapp.com/flag_evil_word.zip`
C'est un lien vers une archive téléchargeons la. 

L'archive contient un fichier **flag.txt** ouvrons la donc pour obtenir le flag.
Flag: **CTF_NotEveytimeYouNeedToReverseAMalware**

