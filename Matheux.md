******************************************************
				Matheux - Reverse Engineering
******************************************************
**Enoncé:** Précédez le mot de passe trouvé par CTF_ pour avoir le flag complet.

Le but est de retrouver le mot de passe du logiciel

Pour résoudre ce challenge, nous allons utiliser **Ghidra**. **Ghidra** est un outil de reverse engineering conçu par la **NSA** qui nous propose de nombreuses fonctionnalités comme le désassemblage et la décomposition de fichiers exécutables, la création et la représentation graphique de scripts, l’analyse de codes binaires…

Avec **Ghidra**, nous avons pu obtenir le code source du programme et trois fonctions qui traitent de la récupération de l'entrée utilisateur(la fonction main()), d'une opération de reverse(la fonction reverse()) et celui de test(fonction tester()) sur l'entrée utilisateur.

**-----------fonction reverse()-----------------------**

    ulong reverse(int iParm1)
    
    {
      int local_1c;
      uint local_10;
      
      local_10 = 0;
      local_1c = iParm1;
      while (local_1c != 0) {
        local_10 = local_1c % 10 + local_10 * 10;
        local_1c = local_1c / 10;
      }
      return (ulong)local_10;
    }

Cette fonction prend en paramètre un entier et renverse la position des chiffres du nombre pris en paramètre

    exemple: 1502------>2051
		     987------->789

La sortie de fonction **reverse()** est envoyée à la fonction **tester()**

**-----------------fonction tester()-----------------------**

    ulong tester(uint uParm1)
    
    {
      uint local_1c;
      int local_10;
      
      local_10 = 1;
      local_1c = uParm1;
      while (local_10 < 6) {
        local_1c = local_1c * local_10;
        local_10 = local_10 + 1;
      }
      return (ulong)local_1c;
    }

La fonction **tester()** prend en entrée un entier et le multiplie successivement par 1,2,3,4 et 5

    Exemple: 5----->600


Dans la fonction **main()**, l'entré utilisateur est comparée à `0x30a3e0=3187680` après avoir subi les deux opérations à travers les fonctions **reverse** et **tester**. Pour trouver notre fameux mot de passe, il faut chercher quelle entrée permet d'obtenir **3187680**.

Nous avons écrit un petit programme en **C++** pour faire les opérations inverses à celles de la fonction **tester** et de la fonction **reverse**. Notre programme prend en entrée la sortie de la fonction **tester** qu'il faut (c'est à dire **3187680**) et renvoi le mot de passe correcte que nous cherchons.

**----------------Notre programme----------------**
```cpp
#include <iostream>

using namespace std;

int main()
{
  int local_1c;
  int local_10;

  local_10 = 5;
  local_1c = 3187680;

	//Cette boucle divise sucessivement la variable par 5,4,3,2 et 1
  while (local_10 > 1) {
    local_1c = local_1c / local_10;
    local_10 = local_10 - 1;
  }


  //Cette boucle comme celle de fonction reverse, renverse la position des chiffres

  local_10 = 0;

  while (local_1c != 0) {
    local_10 = local_1c % 10 + local_10 * 10;
    local_1c = local_1c / 10;
  }
   cout<<local_10<<endl;


    return 0;
} 
```

On obtient à l'exécution de notre programme le mot de passe: **46562**
On ajoute ceci à **CTF_** pour avoir le flag complet: **CTF_46562**





