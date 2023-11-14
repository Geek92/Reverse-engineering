# General information

- Name of the challenge: static_linking

- Download date: 08/11/2023
- Resolved: Yes

- Solution (Password): 1984
- Finish date: 08/11/2023
- Time spent:  30min

- Tools used: XXX

# Resolution steps

J'ai exécuté le programme.

j'ai inseré un nombre, ce n'etait pas le nombre exact

j'ai lançé la commande readelf -a

j'ai lancé la commande objdump -d -M intel stat_link > fichier.txt 

j'ai examiné le code de la fonction main.

en analisant le main on constate qu'on va recuperer le nombre passé en parametre à la fonction scanf ensuite on fait un xor entre entre celui-ci et le nombre 0x2323,ensuite on le compare au nombre 0x24e3.

pour trouver la valeur du mot de passe j'ai effectué un xor entre 0x2323 et 0x24e3.

...

# Challenge evaluation

- How do you estimate the difficulty of the challenge?
 2. Easy;

X

- How do you estimate the ratio between the points and the difficulty of the challenge?
 2. No problem; 

X

- How many points would you accord to the challenge?

150 points
