
*****     
						Shit! -  Steganographie
*****
**Enoncé:** Aucun

Cette épreuve nous donne un fichier **file** à télécharger . C'est une archive. Après téléchargement on extrait l'archive.
En fouillant chaque dossier nous sommes tombé sur le fichier **/xl/sharedStrings.xml** notre patience semble être récompensé le flag est sous nos yeux:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<sst xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" count="1" uniqueCount="1"><si><t xml:space="preserve">CTF_thaiq0H_ze8Hoow </t></si></sst>
```

Flag: **CTF_thaiq0H_ze8Hoow**
