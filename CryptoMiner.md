****************************************************************
							CryptoMiner?
****************************************************************

**Enoncé:** Trouver le domaine que ce malware essaie de contacter et renseignez-le comme flag. Attention: Ceci est un vrai malware. Traitez-le seulement dans un sandbox. Mot de passe ouverture du zip: miner


Il est question d'analyser ce malware et de voir les connexions réseaux qu'il établie. La première idée qui nous viens à l'esprit est de lancer l'exécutable avec l'outil **wine** et de faire la capture et une analyse de trafic réseau avec **wireshark**.
On exécute:

    $ wine crypto_miner.exe
Puis on lance **Wireshark** .
 

On patiente un peu puis, dans wireshark, nous obtenons notre domaine:

    6	11.963081120	192.168.8.105	192.168.8.1	DNS	74	Standard query 0x185c A v9.proxxxy.xyz







