# General information

- Name of the challenge: Randsomware

- Download date: 5/12/2023
- Resolved: Yes/No

# step 1
-Resolved: Yes
- Solution (Password): Resolved: /home,/root,/var/lib/mysql,/var/www,/etc/nginx,/etc/apache2,/var/log
- Finish date: 5/12/2023

- Tools used: STRINGS GHIDRA

# Resolution steps

j'ai executé la commande strings file1 | less
j'ai parcourue le fichier, et j'ai trouvé une liste de repertoires /root/.ssh
/usr/bin
/etc/ssh
/home
/root
/var/lib/mysql
/var/www
/etc/nginx
/etc/apache2
/var/log

j'ai essayé cette reponse et elle n'a pas fonctioné, par la suite j'ai ouvert le fichier avec ghidra pour comprendre comment adapter la solution que j'ai obtenu, en parcourant le fichier je suis tombé sur la fonction void encrypt_directory(char *param_1) et à lìinterieur de la fonction je suis tombé sur la fonction void encrypt_directory(char *param_1) qui verifie si le repertoir passé en parametre est à exclure. j'ai deduit qu'il fallait exclure certains repertoirs. J'ai essayé la precedente solution en excluant à chaque fois le premier repertoire et j 'ai finit par obtenir la solution.

# step 2
-Resolved: Yes
- Solution (Password): Resolved: MBEDTLS,RSA_AES_CBC,2048,128
- Finish date: 5/12/2023

- Tools used: STRINGS GHIDRA

# Resolution steps

j'ai executé la commande strings file1 | less
j'ai supposé que la librairie utilisée etait openssl, j'ai recherché des refferences à openssl et je ne les ai pas trouvées, j'ai donc exclue cette hyphothèse. j'ai continué à parcourir le fichier et a regarder les differentes fonctions qui sont utilisées, j'ai trouvé plusieures fonctions qui commençaient par mbedtls, en faisant des recherches sur internet je me suis rendu compte qu 'il s 'agissait effectivement d 'une librairie  de chiffrement. en parcourant la doc j'ai de ouvert qu'il propose plusieurs algorithmes symetriques et assymetriques. je suis retourné sur ghidra en parcourant le main je suis tombé sur la fonction encrypdirectory et en parcourant cette fonction je suis tombé sur la fonction encryptfile et à l'interieur de cette fonction j'ai la fonction Aes_encrypt et cette fonction à son tour, contient la fonction mbedtls_aes_crypt_cbc à partir de la je peux conclure que l'algorythme symetrique est AES, le mode est CBC et la taille de clé est 128. La fonction LoadRSA presente dans le main me fait conclure que l'algo asymétrique est RSA et la clé etant stockée dans un fichier externe je conclue que la taille de la clè est 2048.

# step 3
-Resolved: Yes
- Solution (Password): 81 FC 95 DF 61 7C 27 6F 2C 05 7F D6 3B 0F 63 82
- Finish date: 12/12/2023

- Tools used: STRINGS GHIDRA,VM

# Resolution steps
pour trouver  le AES IV du /root/flag je commence par analyser la fonction encrypt_directory je constate qu 'elle ouvre le repertoire et qu'elle cree des fichier avec l'extention .encrypted  et en observant la fonction encryptfile, on constate que celle ci ouvre le fichier passè en parametre en mode écriture binaire donc je suppose qu'il faut regarder le contenu du fichier flag.encrypted dans le repertoire root. j'ai monté disque et j'ai constaté que le fichier  flag.encrypted est un fichier binaire, j'ai executé la commande xxd flag.encrypted > result_hex.txt le contenu du ficiher result_hex.txt n'est pas très comprehensible du coup je retourne sur ghidra pour inspecter la fonction encrytfile, à l'interieur de cette fonction je constate un appel à la fofnction mbedtls_pk_encrypt cette fonction prends en parametre la taille du message à chiffrer dans notre cas 16 bytes j'ai supposé par intuition qu'il correspond au IV et elle prends egalement en parametre la taille du buffer de sortie dans notre cas 256 byte. je suis retourné dans le fichier result_hex.txt j'ai exclue les 256 premiers bytes correspondants à la sortie et j'ai récupéré les 16 octect suivant qui correspondent au message j'ai essayé la solution et elle a fonctioné. 

...

# Challenge evaluation

- How do you estimate the difficulty of the challenge?
4. Hard; 

X

- How do you estimate the ratio between the points and the difficulty of the challenge?
1. Not enough point;

X

- How many points would you accord to the challenge?

500 points
