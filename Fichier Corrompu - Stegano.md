* * * * *
                    Fichier Corrompu - Stéganographie
* * * * *

**Enoncé:** Les agents de DJAKPATAGLO ont trouvé une nouvelle astuce: corrompre des fichiers pour exfiltrer des données. L'astuce a été encore une fois découverte par le bjCSIRT qui sollicite votre expertise pour lire le contenu de ce fichier.

Le but ici est d'arriver à lire le contenu du fichier corrompu.

Nous téléchargeons donc le fichier. Il s'agit d'un fichier *.png* corrompu. Grâce à l'outil **pngcheck** on vérifie que l'image est bien corrompu: 
`$ pngcheck -v chal.png` 
> File: chal.png (3647 bytes)
		this is neither a PNG or JNG image nor a MNG stream
ERRORS DETECTED in chal.png

Le fichier est bien corrompu. Nous allons essayer de le réparer avec l'outil **PCRT (PNG Check & Repair Tool)**. C'est un script python qui permet de verifier si une image **png** est correct et qui fixe l'erreur dans le cas contraire:


`$ python PCRT.py -v -i chal.png`

	 ____   ____ ____ _____ 
	|  _ \ / ___|  _ \_   _|
	| |_) | |   | |_) || |  
	|  __/| |___|  _ < | |  
	|_|    \____|_| \_\|_|  

			PNG Check & Repair Tool 

			Project address: https://github.com/sherlly/PCRT
			Author: sherlly
			Version: 1.1
	
	[Detected] Wrong PNG header!
	File header: 90514E470D0A1A0A
	Correct header: 89504E470D0A1A0A
	[Notice] Auto fixing? (y or n) [default:y] y
	[Finished] Now header:89504E470D0A1A0A
	[Finished] Correct IHDR CRC (offset: 0x1D): 3EF3D125
	[Finished] IHDR chunk check complete (offset: 0x8)
	[Finished] Correct IDAT chunk data length (offset: 0x84 length: DA3)
	[Finished] Correct IDAT CRC (offset: 0xE2F): 7F3128C0
	[Finished] IDAT chunk check complete (offset: 0x84)
	[Finished] Correct IEND chunk
	[Finished] IEND chunk check complete
	[Finished] PNG check complete
	[Notice] Show the repaired image? (y or n) [default:n] n

Nous ouvrons le fichier image réparé et on peut voir le flag au bas de l'image:
Flag: **CTF_Amazone_Slayer**

