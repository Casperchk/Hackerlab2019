
              
*****                                                              
					  Damn url shoterner - Forensic
*****
                                           
**Enoncé:** L'unité Forensic a collecté beaucoup d'urls raccourcies et ne sait pas laquelle est la bonne. Elle sait néamoins que Djakpataglo utilisait l'une de ces urls raccourcies pour des attaques de phishing contre les membres du gouvernement.

A cette épreuve est jointe un fichier **url_list.tar.xz** à télécharger. Ce fichier continent un fichier **url_list** contenant des urls. Après un bon coup d'oeil on remarque qu'il y a des urls dupliquées. Utilisons la commande **sort** pour supprimer les liens dupliqués 

    $ sort -u url_list > url_uniq_list

Visiter les liens  un à un nous prendra du temps vu le nombre de lien qu'il reste. Mais nous pouvons utiliser l'extension **intruder** de **burpsuite** pour exécuter les requête une à une et vérifier leur statuts.
Après avoir configuré **intruder** avec la liste des des urls comme payloads et lancé l'attaque, nous avons les statuts de toutes les requêtes. Filtrons les statuts afin d'avoir uniquement les statuts 301 ou 200. 
On obtient des requêtes avec des statuts 301 (redirection) et 200 (OK). Sur plus de 500 urls on tombe sur une url nous donnant un code 301 : `https://bit.ly/2oQSSN6`  en l'ouvrant dans un onglet du naviguateur on a:  `http://dev2608.hackerlab.bj:8001/for_2/`. En modifiant l'url par `http://hackerlab.bj:8001/for_2/` on a notre flag :
**CTF_HackerLabBestForensicSearcherIsYOU**
                                            
