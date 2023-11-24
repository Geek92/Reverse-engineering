# General information

- Name of the challenge: no_strings_rereloaded

- Download date: 21/11/2023
- Resolved: Yes

- Solution (Password): DOUG145 4d4m5
- Finish date: 21/11/2023
- Time spent: 45 min 

- Tools used: ghidra, gdb

# Resolution steps

j'ai essayé bonjour comme argv[1] et j'ai vu que ce n'etait pas le mot de passe

j 'ai exécuté la commande ltrace ./nsrr je n'ai pas trouvé le mot de passe

j 'ai exécuté la commande strace ./nsrr je n'ai pas trouvé le mot de passe

j'ai ouvert le programme avec ghidra

j 'ai selectioné la fonction entry

au niveau de la ligne 7 on peut voir un appel à la fonction de la libc qui à son tour appele la fonction main
'__libc_start_main(FUN_001012d0,param_2,&stack0x00000008,0,0,param_1,auStack_8);'

j'ai renomé le premier parametre en main

j'ai analysé la fonction main 

à la ligne 33 on peut observer un appel à une fonction  qui prends comme premier un pointeur vers la chaine decharactère inserée lors de l'execution du fichier binaire, et comme deuxieme parametre un pointeur vers une seconde chaine de charactère qui represente le mot de passe
'iVar1 = FUN_00101200(local_18[1],local_148);'

j'ai renomé la fonction FUN_00101200 en strcmp

j 'ai recuperé les adresse du point d'entrée:00101100, de la fonction main:001012d0, de la fonction strcmp:00101200

j'ai executé le fichier avec gdb

j'ai lancé la commande starti bonjour

j'ai lancé la commande info file 

j'ai recuperé l'adresse du point d 'entrée 0x555555555100

j'ai calculé l'offset entre l'adresse de la fonction entry et celle de la fonction main 001012d0 - 00101100 = 1D0

j'ai rajouté l'offset à l'adresse du point d'entrée pour obtenir l'adresse de la fonction main sur gdb 0x555555555100 + 0x1D0 =0x00005555555552d0

on observant et en comparant les adresses des fonction entry, main et strcmp, obtenues avec ghidra à celles des fonctions main et entry obtenues avec gdb, j'ai déduit que l'adresse de la fonction strcmp au niveau de gdb devait se trouver à l'adresse 0x0000555555555200 

j'ai placé un breakpoint à l'adresse 0x0000555555555200  et j'ai controlé les valeurs des registres rsi et rdi, le registre rsi contenait le mot de passe.


# Challenge evaluation

- How do you estimate the difficulty of the challenge?
1. 3. Medium;

X

- How do you estimate the ratio between the points and the difficulty of the challenge?
1.  2. No problem ;

X

- How many points would you accord to the challenge?

100 points
