#C #Coding 

		RUCKTOOA Thomas / 2600

Ecrire une fonction qui doit afficher toutes les lettres de l’alphabet sans retour à la ligne tout en renvoyant le nombre de caractères affiché. L’affichage se fera via la fonction write.



Voici un exemple de la résolution de cet énoncé : 
__________________________________________________________________
#include <unistd.h> 

int my_alphabet(void) {

    int i;
    
    char c;
    
    for (i = 0, c = 'a'; c <= 'z'; ++i, ++c) {
    
        write(1, &c, 1);
    }
    return i;
}

___________________________________

# Une explication ?

Voici une explication pour chaque lignes de code : 

```c
#include <unistd.h>
```

Cette ligne inclut le fichier d’en-tête `unistd.h` qui contient les déclarations pour les appels système Unix, y compris `write`.

```c
int my_alphabet(void) {
```

Ceci déclare une fonction appelée `my_alphabet` qui ne prend aucun argument (`void`) et renvoie un entier (`int`).

```c
    int i;
    char c;
```

Ces lignes déclarent deux variables : `i` est un entier qui sera utilisé pour compter le nombre de caractères affichés, et `c` est un caractère qui sera utilisé pour stocker chaque lettre de l’alphabet.

```c
    for (i = 0, c = 'a'; c <= 'z'; ++i, ++c) {
```

Ceci est une boucle `for` qui initialise `i` à 0 et `c` à ‘a’. La boucle continue tant que `c` est inférieur ou égal à ‘z’. Après chaque itération de la boucle, `i` est incrémenté de 1 et `c` est également incrémenté de 1 (ce qui le fait passer à la lettre suivante de l’alphabet).

```c
        write(1, &c, 1);
```

Ceci appelle la fonction `write`, qui écrit le contenu de `c` sur la sortie standard (représentée par le descripteur de fichier 1). Le deuxième argument est l’adresse de `c` (car `write` attend un pointeur), et le troisième argument est le nombre d’octets à écrire (dans ce cas, 1, car un caractère est de taille 1).

```c
    }
```

Ceci marque la fin du corps de la boucle `for`.

```c
    return i;
```

Ceci renvoie la valeur de `i`, qui représente le nombre total de caractères affichés.

```c
}
```

Et enfin, cette ligne marque la fin de la fonction `my_alphabet`.

# Un deuxième exemple 

Écrire un fichier my_strlen.c contenant une fonction:


Cette fonction compte le nombre de caractère que comporte un tableaux de char[].

Par exemple:

- Si str="salut a tous", la valeur de retour doit être 12
- Si [str=%22g@m3rz](mailto:str=%22g@m3rz)", la valeur de retour doit être 6
- Si str="", la valeur de retour doit être 0

Cette version **doit être itérative**.

# La solution 
_____________________________________________


#include "my_strlen.h"

int my_strlen(char const str[]) {

    int count = 0;
    
    while (str[count] != '\0') {
    
        count++;

    }
    return count;
}
____________________________________________________________________

Quand je décompose le code : 

```c
#include "my_strlen.h"
```

Cette ligne indique au préprocesseur de C d’inclure le fichier d’en-tête “my_strlen.h”. Ce fichier contient la déclaration de la fonction `my_strlen`.

```c
int my_strlen(char const str[]) {
```

C’est la définition de la fonction `my_strlen`. Elle prend un tableau de caractères constant (une chaîne) en argument et renvoie un entier.

```c
    int count = 0;
```

On initialise une variable `count` à 0. Cette variable sera utilisée pour compter le nombre de caractères dans la chaîne.

```c
    while (str[count] != '\0') {
```

C’est une boucle `while` qui continue à s’exécuter tant que le caractère actuel dans la chaîne n’est pas le caractère de fin de chaîne (`'\0'`).

```c
        count++;
```

On incrémente `count` à chaque itération de la boucle, ce qui signifie qu’on compte un caractère supplémentaire dans la chaîne.

```c
    }
```

C’est la fin de la boucle `while`.

```c
    return count;
```

On renvoie `count`, qui est maintenant le nombre total de caractères dans la chaîne.

```c
}
```

C’est la fin de la fonction `my_strlen`.

J'espère que cela vous aidera.
