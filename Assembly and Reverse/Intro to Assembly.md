#Assembly #x86 #reverse

												--- RUCKTOOA Thomas 1ère année, 2600 --
												Discord :  2600r.thomas

Le processeur est composé de : 

- L'unité de contrôle (décode les instructions)
- ALU (Arithmetic Logic Unit) (Code les instructions)
- Registres (états internes)
- Bus (Voies de communications)

# Les différentes instructions

L’instruction SAR (Shift Arithmetic Right) en assembleur est utilisée pour déplacer les bits d’un opérande vers la droite. C’est similaire à l’instruction SHR, sauf que le bit le plus significatif (MSB) est déplacé sur lui-même. Cela préserve le signe original de l’opérande de destination, car le MSB est le bit de signe. Chaque décalage divise l’opérande de destination par 2, tout en préservant le signe. Notez que le bit le moins significatif (LSB) est déplacé dans le drapeau de retenue (CF).

En termes simples, imaginez que vous avez une file de personnes et que vous demandez à tout le monde de faire un pas vers la droite. La personne à l’extrême droite sort de la file (c’est le LSB qui va dans le CF), et une nouvelle personne entre à gauche. Mais au lieu d’être une nouvelle personne, c’est la même personne qui était déjà à l’extrême gauche (c’est le MSB qui est déplacé sur lui-même).

# Le lexique

[MSB, ou Most Significant Bit, est un terme utilisé en informatique pour désigner le bit le plus significatif dans un nombre binaire](https://en.wikipedia.org/wiki/Bit_numbering)[1](https://en.wikipedia.org/wiki/Bit_numbering.

[Il représente la place la plus élevée de l’entier binaire](https://en.wikipedia.org/wiki/Bit_numbering)[1](https://en.wikipedia.org/wiki/Bit_numbering)

Par exemple, dans le nombre binaire 1001 (qui est 9 en décimal), le MSB est le premier 1.

Dans le contexte de la mémoire, le MSB peut se référer à l’organisation des octets dans la mémoire. [Par exemple, dans un système big-endian, le MSB (ou l’octet le plus significatif) est stocké à l’adresse mémoire la plus basse](https://www.allaboutcircuits.com/technical-articles/big-endian-little-endian-endianness-byte-arrangement-digital-systems/)[2](https://www.allaboutcircuits.com/technical-articles/big-endian-little-endian-endianness-byte-arrangement-digital-systems/). [Cela contraste avec les systèmes little-endian, où l’octet le moins significatif est stocké à l’adresse mémoire la plus basse](https://en.wikipedia.org/wiki/Bit_numbering)[2](https://www.allaboutcircuits.com/technical-articles/big-endian-little-endian-endianness-byte-arrangement-digital-systems/).

[Il est important de noter que le MSB et l’ordre des octets peuvent avoir un impact significatif sur la manière dont les données sont lues et interprétées dans différents systèmes](https://en.wikipedia.org/wiki/Bit_numbering)[2](https://www.allaboutcircuits.com/technical-articles/big-endian-little-endian-endianness-byte-arrangement-digital-systems/).

# Un exemple ? 

Voici un exemple :
________________________________________________________________
section .text 
global my_bsr my_bsr: 


test rdi, rdi 
jz done 



bsr rax, rdi 
inc rax 
ret 

done: 

 xor rax, rax ret

________________________________________________________________

Enfin bref voici une explication ligne par ligne : 



1. `section .text` : Cette ligne indique que la section suivante du code est la section `.text`, qui est là où le code exécutable est généralement placé.
    
2. `global my_bsr` : Cette ligne rend la fonction `my_bsr` accessible à partir d’autres fichiers. Je suis pas sûr mais à mon avis c'est nécessaire pour interagir avec le fichier .o que vous devez réaliser (avec nasm ?)
    
3. `my_bsr:` : C’est l’étiquette de la fonction. Le code qui suit est le corps de la fonction `my_bsr`.
    
4. `test rdi, rdi` : Cette instruction effectue une opération ET bit à bit sur la valeur dans `rdi` avec elle-même, ce qui a pour effet de tester si `rdi` est zéro.
    
5. `jz done` : Cette instruction signifie “jump if zero” (sauter si zéro). Si le résultat de l’instruction `test` précédente est zéro (ce qui signifie que `rdi` était zéro), alors le contrôle saute à l’étiquette `done`.
    
6. `bsr rax, rdi` : L’instruction BSR (Bit Scan Reverse) scanne les bits de `rdi`, en commençant par le bit le plus significatif, et place la position du premier bit défini rencontré dans `rax`. (en gros il va trouver le bit le plus grand)
    
7. `inc rax` : Cette instruction incrémente la valeur dans `rax` de 1.
    
8. `ret` : Cette instruction termine la fonction et renvoie le contrôle à l’appelant, en renvoyant la valeur dans `rax`.
    
9. `done:` : C’est une étiquette pour un point dans le code où le contrôle doit sauter si `rdi` est zéro.
    
10. `xor rax, rax` : Cette instruction effectue une opération XOR bit à bit sur la valeur dans `rax` avec elle-même, ce qui a pour effet de mettre à zéro `rax`.
    
11. `ret` : Cette instruction termine la fonction et renvoie le contrôle à l’appelant, en renvoyant la valeur dans `rax`.
    



# Un exemple mais plus difficile cette fois 

______________________________________________________________________________

section .text
global my_isalpha

my_isalpha:
    
    cmp rdi, 'a'
    jl .not_alpha
    cmp rdi, 'z'
    jg .check_uppercase
    mov rax, 1
    ret

.check_uppercase:
    
    cmp rdi, 'A'
    jl .not_alpha
    cmp rdi, 'Z'
    jg .not_alpha
    mov rax, 1
    ret

.not_alpha:
    
    xor rax, rax
    ret
___________________________________________________

A partir de maintenant, je vais décomposer le code :

```asm
section .text
```

Cette ligne indique que la section suivante du code est la section `.text`, qui est là où le code assembleur réside.

```asm
global my_isalpha
```

Cette ligne déclare `my_isalpha` comme une fonction globale, ce qui signifie qu’elle peut être appelée depuis d’autres fichiers.

```asm
my_isalpha:
```

C’est le début de la définition de la fonction `my_isalpha`.

```asm
    cmp rdi, 'a'
    jl .not_alpha
```

Ces deux lignes comparent le caractère dans `rdi` à `'a'`. Si le caractère est inférieur à `'a'`, il saute à l’étiquette `.not_alpha`.

```asm
    cmp rdi, 'z'
    jg .check_uppercase
```

Ces deux lignes comparent le caractère dans `rdi` à `'z'`. Si le caractère est supérieur à `'z'`, il saute à l’étiquette `.check_uppercase`.

```asm
    mov rax, 1
    ret
```

Si le caractère n’a pas sauté à une des étiquettes précédentes, cela signifie qu’il est une lettre minuscule. Donc, il met `1` dans `rax` et retourne.

```asm
.check_uppercase:
    cmp rdi, 'A'
    jl .not_alpha
    cmp rdi, 'Z'
    jg .not_alpha
```

C’est similaire aux lignes précédentes mais pour les lettres majuscules.

```asm
    mov rax, 1
    ret
```

Si le caractère est une lettre majuscule, il met `1` dans `rax` et retourne.

```asm
.not_alpha:
    xor rax, rax
    ret
```

Si le caractère n’est ni une lettre minuscule ni une lettre majuscule, il met `0` dans `rax` et retourne. L’instruction `xor rax, rax` est une façon efficace de mettre `0` dans un registre.
