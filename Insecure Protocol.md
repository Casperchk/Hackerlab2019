* * * * *
                  Insecure Protocol - Forensic
 * * * * *

**Enoncé:** Aucun

Dans ce challenge il s'agira d'analyser une capture réseau **capture.pcap** afin de trouver le flag.

On ouvre le fichier avec **Wireshake**. On analyse le trames du protocole **HTTP** ( le protocole non sécurisé):

On remarque une requête **POST**:

>POST /thatoneyes/action_page.php HTTP/1.1
Host: guidos.000webhostapp.com
Connection: keep-alive
Content-Length: 50
Cache-Control: max-age=0
Origin: http://guidos.000webhostapp.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Referer: http://guidos.000webhostapp.com/thatoneyes/xafezjfgeg.html
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

	uname=admin&psw=CTF_forensicinvestigat&remember=onHTTP/1.1 200 OK


On a le paramètre **psw** qui est égale au flag: **CTF_forensicinvestigat** Bingo on peut valider l'épreuve.


