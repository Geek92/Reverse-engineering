# General information

- Name of the challenge: no_strings

- Download date: 07/11/2023
- Resolved: Yes

- Solution (Password): Ar7hU c. Cl4rk3
- Finish date: 07/11/2023
- Time spent: 0day 00h 40min

- Tools used: XXX

# Resolution steps

J'ai exécuté le programme

j'ai lancé la commande readelf -a

j'ai lancé la commande objdump -d -M intel notring

j'ai examiné le code de la fonction main 

j'ai decouvert un tableau qui est initialisé,
ce tableau est utilisé par la suite pour faire une comparaison avec la chaine de caractères inserée par l'utilisateur.

j'ai decodé la chaine de caractère stockée dans le tableau, celle ci correspondait au mot de passe.

# Challenge evaluation

- How do you estimate the difficulty of the challenge?
 2. Easy;

X

- How do you estimate the ratio between the points and the difficulty of the challenge?
2. No problem ;

X

- How many points would you accord to the challenge?

100 points
