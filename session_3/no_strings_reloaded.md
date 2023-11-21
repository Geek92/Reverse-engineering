# General information

- Name of the challenge: no_strings_reloaded

- Download date: 21/11/2023
- Resolved: Yes

- Solution (Password): N.*K.*j3m1s1n
- Finish date: 21/11/2023
- Time spent:  10min

- Tools used: ltrace 

# Resolution steps

j'ai lancé la commande ltrace ./nsr password

dans la fonction main on observe cette ligne de code "strcmp("password", "N.*K.*j3m1s1n")"

a partir de là on peut deduire la valeur du mot de passe.

# Challenge evaluation

- How do you estimate the difficulty of the challenge?
1.  2. Easy ;

X

- How do you estimate the ratio between the points and the difficulty of the challenge?
1. 2. No problem ;
X

- How many points would you accord to the challenge?

50 points
