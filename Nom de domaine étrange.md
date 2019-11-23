* * * * *

                     Nom de domaine Etrange - Forensic

* * * * *

**Enoncé:**  *Lors de l'investigation au domicile du gayeman DJAKPATAGLO, nos agents sont tombés sur le nom de domaine suivant: `xn--ctf_wookpo-5he.com`. Aidez les à retrouver le nom de domaine original que le gayeman a enregistré.*

Le but est donc de retrouver l'original du nom de domaine enrégistré. Le préfixe de ce nom de domaine commence par `xn--` . So let google it ( allons voir ce que google peut nous donner comme information ).

En faisant une petite recherche google nous tomber un article de Wikipedia qui dit de quoi il s'agit. Selon Wikipedia:

`Un nom de domaine internationalisé est un nom de domaine Internet qui peut contenir des caractères non définis par le standard ASCII. Parmi ces caractères, on trouve notamment les lettres accentuées courantes dans de nombreuses langues européennes, ainsi que d'autres caractères n'appartenant pas à l'alphabet latin.Plusieurs registres de noms de domaine autorisent aujourd'hui les noms de domaine internationalisés, par exemple .de (Allemagne), .eu (Europe)`
............................................................................................................................................... 
==Le standard définissant les noms de machines (RFC 11232) ne considère qu'un nombre très limité de caractères (sous-ensemble ASCII). D'où le principe du protocole IDNA (Internationalized Domain Names in Applications, RFC 58903) : les noms de domaine internationalisés sont convertis dans un nom de domaine ASCII (format Punycode). Par exemple, `www.académie-française.fr` sera converti en `www.xn--acadmie-franaise-npb1a.fr` .==

Nous savons maintenant que nous devons convertir le domaine `xn--ctf_wookpo-5he.com` en son original. Pour cela nous avons utilisé **Punycode converter**.

**Punycode** est une syntaxe de codage définie dans la **RFC 3492** et conçue pour être utilisée en adéquation avec les noms de domaine internationalisés dans les applications les supportant. En utilisant [Punycoder](https://www.punycoder.com) nous avons pu retrouver le vrai nom de domaine qui est : `ctf_woɖokpo.com`. Bingo voilà notre flag: **ctf_woɖokpo.com**.

