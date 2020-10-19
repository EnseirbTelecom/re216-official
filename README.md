# RE216 - Projet de programmation réseau

1. [Contexte](#contexte)
2. [Soumission de code](#soumission-de-code)
3. [Evaluation](#evaluation)
4. [Notation](#notation)
5. [Jalons](#jalons)
* [Jalon 1 - Client-serveur TCP et serveur multi-clients](#jalon-1-\--client\-serveur-tcp-et-serveur-multi\-clients)
* [Jalon 2 - Gestion des utilisateurs](#jalon-2-\--gestion-des-utilisateurs)
* [Jalon 3 - Gestion des salons de discussion](#jalon-3-\--Gestion-des-salons-de-discussion)
* [Jalon 4 - Gestion des transferts de fichiers](#jalon-4-\--gestion-des-transferts-de-fichiers)
6. [Tips and Tricks](#tips-and-tricks)
7. [Rappel de C](#rappel-de-c)

# Contexte 
[Top](#re216-\--projet-de-programmation-réseau)

Ce projet consiste en la réalisation d'un grand classique de la programmation réseau, un cas pratique de discussion instantanée de type client/serveur. A titre d'exemple et de curiosité, vous pouvez jeter un coup d'œil au protocole IRC (Internet Relay Chat) défini originellement par la RFC1459.

Le projet a pour objectif la réalisation d'une application de chat client/serveur en C permettant d'échanger des messages entre 2 utilisateurs, entre plusieurs utilisateurs, ou à destination de la totalité des utilisateurs connectés sur le réseau, ainsi que de s'envoyer des fichiers.

L'objectif sous-jacent de ce projet est la manipulation des primitives réseaux et des sockets POSIX en C que vous avez vues en cours (socket(), bind(), listen(), connect(), accept(), send(), recv() ), ainsi que la mise œuvre de communications sur TCP/IP.



# Déroulement 
[Top](#re216-\--projet-de-programmation-réseau)

Pour réaliser ce système, vous allez construire votre code petit à petit en suivant des jalons pré-définis, décrits ci-dessous. Un jalon correspond à une étape de réalisation, et chaque jalon doit être atteint avant de passer à l'étape suivante. Une fois le jalon atteint, il faut le soumettre à l'équipe enseignante au travers de la procédure qui vous est donnée. Il est estimé qu'au minimum un jalon doit être atteint par séance de projet.

Les enseignements intégrés que vous avez suivis vous ont donné les bases solides pour débuter ce projet qui s'étalera sur 3,5 séances encadrées de 2h40 (soit 9h20 au total). Le quantité de travail à fournir hors classe est de l'ordre du simple au double de celle des séances encadréees. 

Le travail doit être fait en groupe de 2 étudiants qui sera déterminé aléatoirement par l'équipe enseignante avant le début du projet. 

[Support de cours](RE216_cours.pdf)


# Soumission de code 
[Top](#re216-\--projet-de-programmation-réseau)

### Soumission des jalons

La soumission des jalons se fait sur GitHub en créant une release de votre code qui sera disponible à toute instant pour l'équipe enseignante. Si vous ne savez pas comment faire une release de votre code sur GitHub, voici [la ressource officielle pour apprendre à le faire](https://help.github.com/en/articles/creating-releases). Le nom des releases sera `jalonx` avec `x` le numéro du jalon. 

### Deadline des jalons : 
L'horaire de rendu des jalons est 23h59. 

En ce qui concerne les dates :

- Jalon 1 : 23 octobre 
- Jalon 2 : 6 novembre 
- Jalon 3 : 11 novembre
- Jalon 4 : 15 novembre
- Rendu final : 15 novembre

### Soumission finale
Cette soumission prendra la forme d'un dernière release nommée `rendu_final` de votre code sur votre répository privé. C'est ce code là qui sera évalué.
Pour etre évalué, votre doit **impérativement** compiler sans erreurs et sans warning sur les machines de l'enseirb OU sur une machine linux ubuntu. 

Votre dernière release doit **obligatoirement** comporter un fichier rendu.txt à la racine de votre reposority qui contient les chaines de caractères :
- `jalonx` avec `x` dans {0,1,2,3,4,Surprise} indiquant le dernier jalon atteint dans son intégralité
- `ongoingy`avec `y` dans {0,1,2,3,4,Surprise} indiquant le jalon en cours s'il y en a un. Si `y` vaut `Surprise`, vous penserez à indiquer ce que vous avez fait en plus du jalon 4 pour permettre aux évaluateurs de savoir quoi tester et de comprendre ce qui a été fait.


# Evaluation 
[Top](#re216-\--projet-de-programmation-réseau)

L'évaluation de votre travail se fera en suivant deux méthodes : une évaluation automatique via des programmes de tests, et une évaluation détaillée.

### Evaluation automatique
A l'issue de ces évaluations, vos releases seront récupérés depuis votre repository github qui sera testé par des programmes d'évaluation sur :

0. La bonne soumission des jalons en temps et en heure sur votre répository github;
1. Le bon respect de l'implémentation des fonctionnalités spécifiées;
2. Le fonctionnement non erroné en cas de reception et traitement de messages non implémentés et de messages erronés (que ce soit du coté client ou du coté serveur);
3. La libération de mémoire et la fermeture des sockets (utilisation de valgrind et lsof)

# Notation 
[Top](#re216-\--projet-de-programmation-réseau)

Ce projet sera noté en suivant la grille de notation suivante et en prenant en compte des points bonus et malus.

### Grille de notation 

Voici la grille de notation à titre indicatif seulement.

| Note | Réalisation non buggée des requirements du(es) jalon(s) |
| ------ | ------ |
| \[0-5\[ | \[0 - Jalon 1\[ |
| 5 | Jalons 1 |
| \]5-8\[ | Jalon 1 + ]0 - Jalon 2\[ | 
| 8 | Jalon 1 + 2 |
| \]8-14\[  | Jalon 1 + 2 + \]0 - Jalon 3\[ |
| 14  | Jalon 1 + 2 + 3 |
| \]14-18\[ | Jalon 1 + 2 + 3 + \]0 - Jalon 4\[ |
| 18 | Jalon 1 + 2 + 3 + 4 |
| \[18-20\] | Jalon 1 + 2 + 3 + 4 + _Surprise_ |

_Surprise_ : _Faites-vous et faites-nous rêver ! Ajoutez des fonctionnalités à vos programmes en plus des jalonss 1+2+3+4._

### Points bonus
- Tout fonctionne en IPv6 et IPV4 : +0.25 point

### Point malus
Des points malus peuvent être appliqués dans les cas suivants:
- Non respect du rendu des jalons aux deadlines indiquées : -2 points;
- Mémoire non libérée : -2 points;
- Mauvaise reception des données lors d'operation de type read/write sur les sockets : -2 points
- Non utilisation de fonction pour rendre le code clair (i.e., si votre main() fait plus de 200 lignes) : -2 points
- File descriptors des sockets et des fichiers non fermés : -2 points;

# Jalons 

## Jalon 1 - Client-serveur TCP et serveur multi-clients 
[Top](#re216-\--projet-de-programmation-réseau)

### Description 

Dans ce jalon, vous allez vous concentrer sur la réalisation d'un modèle client/serveur IPv4 où le serveur renvoie au client la chaîne de caractère précédemment envoyée.
Dans ce modèle de communication, il y a une partie client et une partie serveur. Pour la première partie, le client devra créer une socket TCP (avec une adresse IPv4 et un numéro port renseigné en argument du programme), établir une connexion sur la socket du serveur. L'envoi et la réception de données pourra alors se faire pour le client.
Parallèlement, du côté du serveur, il faudra créer une socket, la lier à un port d'écoute et repérer la nouvelle connexion. Une fois la connexion acceptée, la réception et l'envoi de données peut se faire.
Dans ce jalon, une fois la connexion établie, le client doit envoyer une chaîne de caractère tapée au clavier au serveur. En réponse, le serveur récupère cette chaîne et la renvoie directement à l'utilisateur en question qui doit l'afficher sur son écran.

Le serveur doit être capable gérer plusieurs clients en parallèle. Pour cela, il faut utiliser un unique processus pour réaliser toutes les tâches en utilisant la fonction **poll()**. Les informations des clients (descripteur de fichier de la socket client et adresse/port) doivent être stockés par le serveur dans une liste chaînée.

Le client doit pouvoir gérer en même temps les messages provenant du serveur et le texte tapé au clavier. Pour cela, il faut également utiliser la fonction poll() côté client sur l'entrée standard du programme et la socket pour la communication avec le serveur.

### Exigences

Les exigences/requirements pour ce premier jalon sont définis comme suit :

**Req1.1** : Création d'un client qui se connecte en TCP à un serveur renseigné par un port et une adresse IPv4 qui sont passés comme arguments du programme comme suit :
```
./client <server_ip_adresse> <server_port>
```

**Req1.2** : Création d'un server avec une socket d'écoute qui accepte la connexion et gère les données entrantes. Le port du serveur doit être passé comme argument du programme.
```
./server <server_port>
```

**Req1.3** : Le serveur doit être capable d’accepter les connexions et de répondre à plusieurs clients en même temps.

**Req1.4** : Le client doit pouvoir prendre une chaîne de caractère tapée au clavier, l'envoyer au serveur et recevoir de ce dernier la même chaîne de caractère.

**Req1.5** : Le client doit pouvoir gérer les chaînes de caractère tapées au clavier et les messages provenant du serveur en même temps.

**Req1.6** : Le serveur, en recevant une chaîne de caractère depuis un client, doit répéter cette chaîne uniquement à ce même client.

**Req1.7** : La connexion doit se couper lorsque le client envoi '/quit'. Que ce soit du coté serveur ou du coté client, les sockets créés doivent être fermées et la mémoire allouée aux structures de données doit être libérée.

**Req1.8** : Le serveur doit stocker les informations des clients (descripteur de fichiers et adresse/port remplis par la fonction **accept()**) dans une liste chaînée.


## Jalon 2 - Gestion des utilisateurs 
[Top](#re216-\--projet-de-programmation-réseau)

### Description

L'objectif de ce jalon est de permettre au serveur de récupérer, stocker et utiliser des informations relatives aux utilisateurs du service de messagerie instantanée. Le serveur n'est plus, comme dans le jalon 1, qu'un serveur répétitif mais plutôt l'intermédiaire entre les utilisateurs pour l'envoi de messages. 
Grâce à cela, les utilisateurs seront capable de choisir un pseudo, de voir les pseudos des autres utilisateurs connectés, de récupérer des informations sur ces utilisateurs, d’envoyer des messages privés à un utilisateur et d’envoyer des messages de broadcast à tous les utilisateurs.
Pour faire cela, les utilisateurs devront taper des commandes avant leur message (/nick, /who, /whois <pseudo>, /msgall <msg>, /msg <pseudo> <msg>) qui seront interprétées par le client et le serveur.

À partir de ce jalon, il vous est demandé de ne plus envoyer de simple chaînes de caractères mais d’utiliser la structure suivante pour vos messages : 

```C
#define NICK_LEN 128
#define INFOS_LEN 128

enum msg_type { 
	NICKNAME_NEW,
	NICKNAME_LIST,
	NICKNAME_INFOS,
	ECHO_SEND,
	UNICAST_SEND, 
	BROADCAST_SEND,
	MULTICAST_CREATE,
	MULTICAST_LIST,
	MULTICAST_JOIN,
	MULTICAST_SEND,
	MULTICAST_QUIT,
	FILE_REQUEST,
	FILE_ACCEPT,
	FILE_REJECT,
	FILE_SEND,
	FILE_ACK
};

struct message {
	int pld_len;
	char nick_sender[NICK_LEN];
	enum msg_type type;
	char infos[INFOS_LEN];
};

static char* msg_type_str[] = {
	"NICKNAME_NEW",
	"NICKNAME_LIST",
	"NICKNAME_INFOS",
	"ECHO_SEND",
	"UNICAST_SEND", 
	"BROADCAST_SEND",
	"MULTICAST_CREATE",
	"MULTICAST_LIST",
	"MULTICAST_JOIN",
	"MULTICAST_SEND",
	"MULTICAST_QUIT",
	"FILE_REQUEST",
	"FILE_ACCEPT",
	"FILE_REJECT",
	"FILE_SEND",
	"FILE_ACK"
};
```

Cette structure est déclarée dans le fichier msg_struct.h.

La structure s’utilise de la façon suivante:

- Le champ **pld_len** contient le taille des données utiles à envoyer (généralement, la taille du message à envoyer). S’il n’y a pas de données utiles (par exemple la requête en question n’a pas de données de message ou de fichier), **pld_len** doit valoir 0.
- Le champ **nick_sender** contient le pseudo de l’utilisateur qui envoie le message.
- Le champ **type** contient le type de message (cf la liste dans enum msg_type). Ce gens va être utilisé pour différencier les actions demandées par l’utilisateur.
- Le champ **infos** va contenir des informations à envoyer. Ces informations dépendent du champ **type**.

Juste après ce message, il est possible d’envoyer un ensemble d'octet contenant le payload (i.e. les données utiles) de taille **pld_len**.

Dans ce jalon, il faut utiliser les types : NICKNAME_NEW, NICKNAME_LIST, NICKNAME_INFOS, ECHO_SEND, UNICAST_SEND, BROADCAST_SEND.

Les champs **infos** doivent contenir les valeurs suivantes en fonction des cas : 
 - Pour **NICKNAME_NEW**, le champ **infos** contient le nouveau pseudo. Le champ **nick_sender** contient une chaîne de caractères vide si l’utilisateur n’a pas encore de pseudo, ou le pseudo actuel si l’utilisateur change de pseudo.
- Pour **NICKNAME_LIST**, le champ **infos** contient une chaîne de caractères vide.
- Pour  **NICKNAME_INFOS**, le champ **infos** contient le pseudo de l’utilisateur dont on veut les informations.
- Pour **ECHO_SEND**, le champ **infos** contient une chaîne de caractères vide.
- Pour **UNICAST_SEND**, le champ **infos** contient le pseudo de l’utilisateur à qui on veut envoyer le message.
- Pour **BROADCAST_SEND**, le champ **infos** contient une chaîne de caractères vide.

### Exigences

**Req2.0** : Les messages échangés entre le client et le serveur doivent impérativement respecter la structure donnée dans le sujet. La seul façon de transmettre un message de taille non-déterminée à l'avance est d'utiliser 2 messages : Un premier avec le champ **pld_len** qui indique la taille du second message, un second qui contient le contenu du mssecond message de taille **pld_len**.

**Req2.1** : Une fois la connexion établie avec le serveur, le client doit s'identifier par son pseudo (avec la commande /nick, type NICKNAME_NEW). Le cas particulier où un utilisateur se connectent avec un pseudo trop long ou un pseudo avec des espaces et autres caractères spéciaux doivent être gérés.
```
Connecting to server ... done!
[Server] : please login with /nick <your pseudo>
/nick CoolestUserEver
[Serveur] : Welcome on the chat CoolestUserEver
```
**Req2.2** : Un utilisateur doit recevoir une erreur si le pseudo qu’il désire est déjà attribué.

**Req2.3** : Le serveur doit gérer plusieurs utilisateurs et plusieurs connexions. Les utilisateurs (pseudo) et leurs infos liées à leur connexion (numéro de socket et structure d’adresse) doivent être stockés par le serveur dans une liste chaînée.

**Req2.4** : Le serveur doit tenir compte du changement de pseudo d’un utilisateur.

**Req2.5** : un client doit pouvoir obtenir du serveur la liste des utilisateurs connectés. (avec la commande /who, type NICKNAME_LIST)

```
/who
[Server] : Online users are
                          - User1
                          - User2
                          - CoolestUserEver

```

**Req2.6** : un client doit pouvoir obtenir du serveur des informations sur un utilisateur en particulier (avec la commande /whois, type NICKNAME_INFOS)

```
/whois  User1
[Server] : User1 connected since 2014/09/29@19:23 with IP address 192.168.3.165 and port number 52322
```

**Req2.7** : Un utilisateur doit pouvoir envoyer un message à tous les autres utilisateurs (broadcast, commande /msgall, type BROADCAST_SEND).

```
%terminal_user0>  /msgall Hello all
                    %terminal_user1 > [user0] : Hello all
                                    %terminal_user2 > [user0] : Hello all
```

**Req2.8** : Un message envoyé ne doit pas être retransmis à l'expéditeur.

**Req2.9** : Un utilisateur doit pouvoir envoyer un message privé à un autre utilisateur (unicast, commande /msg <pseudo> <msg>, type UNICAST_SEND).

```
%terminal_user0> /msg user1 Hello
                    %terminal_user1 > [user0] : Hello
```

**Req2.10** : Le serveur doit traiter les requetes de type UNICAST_SEND lorsque l'utilisateur spécifié n'existe pas. Le serveur doit alors renvoyer à l'émetteur une information pertinente.
```
%terminal_user0> /msg userKJHDQ Hello
                    %terminal_user1 > [Server] : user userKJHDQ does not exist
```

	
**Req2.11** : Le serveur doit considerer sa fonction “echo” (i.e. renvoyer le message à l’utilisateur) si aucune commande n’est tapée avant le message (echo, type ECHO_SEND).


## Jalon 3 - Gestion des salons de discussion
[Top](#re216-\--projet-de-programmation-réseau)

### Description

Ce jalon a pour objectif la réalisation des messages entre les utilisateurs afin que votre application devienne une application de messagerie instantanée à part entière. Jusqu'à présent, le serveur ne permettait que d’envoyer des messages privés en unicast et des messages en broadcast. On introduit ici l'utilisation de la notion de multicast applicatif.
Pour le multicast applicatif, un utilisateur peut créer un salon. Les utilisateurs ont alors la possibilité de rejoindre ce salon, et une fois inscrits les utilisateurs du salon peuvent s'échanger des messages entre eux. Les utilisateurs peuvent quitter le salon ou changer de salon quand ils le souhaitent.

Dans ce jalon, il faut utiliser les types : MULTICAST_CREATE, MULTICAST_LIST, MULTICAST_JOIN, MULTICAST_SEND et MULTICAST_QUIT.

Les champs **infos** doivent contenir les valeurs suivantes en fonction des cas : 
 - Pour **MULTICAST_CREATE**, le champ **infos** contient le nom du salon à créer.
- Pour **MULTICAST_LIST**, le champ **infos** contient une chaîne de caractères vide.
- Pour  **MULTICAST_JOIN**, le champ **infos** contient le nom du salon à rejoindre.
- Pour **MULTICAST_SEND**, le champ **infos** contient le nom du salon dans lequel on veut envoyer le message.
- Pour **MULTICAST_QUIT**, le champ **infos** contient le nom du salon à quitter.

### Exigences

**Req3.1** : Un utilisateur doit pouvoir créer un salon (commande /create, type MULTICAST_CREATE). Les cas particulier où un utilisateur déclare un salon avec des espaces ou des caractères spéciaux doivent être gérés.

**Req3.2** : Un utilisateur doit pouvoir rejoindre automatiquement le salon qu’il vient de créer.

**Req3.3** : Un utilisateur doit pouvoir demander la liste des salons (commande /channel_list, type MULTICAST_LIST).

**Req3.4** : Le serveur doit retourner un message d'erreur à l'utilisateur qui demande la création d'un salon déjà existant.

**Req3.5** : Un utilisateur doit pouvoir rejoindre et quitter un salon(commandes /join et /quit, type MULTICAST_JOIN et MULTICAST_QUIT).

**Req3.6** : Un utilisateur inscrit à un salon doit pouvoir changer de salon, ce qui lui fait quitter le salon en cours.

**Req3.7** : Le serveur doit détruire le salon lorsque son dernier occupant le quitte.

**Req3.8** : Un message envoyé dans un salon ne doit pas être transmis à d'autres utilisateurs que ceux présents dans le salon (multicast, type MULTICAST_SEND).

Exemple de fonctionnement des salons : 


```
%terminal_user0> /create channel_name
%terminal_user0> You have created channel channel_name
%terminal_user0[channel_name]> You have joined channel_name
                    %terminal_user1> /join channel_name
                    %terminal_user1[channel_name]> You have joined channel_name
%terminal_user0[channel_name]>  I'm downtown
                    %terminal_user1[channel_name]> user0> : I'm downtown
%terminal_user0[channel_name] > /quit channel_name
                    %terminal_user1[channel_name] > /quit channel_name
%terminal_user0> Channel name has been destroyed

```




## Jalon 4 - Gestion des transferts de fichiers
[Top](#re216-\--projet-de-programmation-réseau)

### Description

L'objectif de ce jalon est de permettre à un utilisateur d'envoyer un fichier à un autre utilisateur. Plusieurs schémas sont possibles pour implémenter cette fonctionnalité. Nous retiendrons le mode P2P (Peer to Peer) ne nécessitant pas de passer le serveur pour échanger des données. Le serveur n'est utilisé que pour mettre en relation les utilisateurs.

Les différentes étapes d’un échange de fichiers sont les suivantes : 
- L’émetteur envoie une demande d’envoi de fichier au serveur, en précisant le nom du récepteur et le nom du fichier (commande /send, type FILE_REQUEST).
- Le serveur transmet cette demande à l’utilisateur récepteur.
- L’utilisateur récepteur peut accepter le téléchargement ou non.
- La réponse est renvoyée à l’émetteur par le biais du serveur (type FILE_ACCEPT ou FILE_REJECT).
- Si le récepteur a refusé l’envoi, l’émetteur en est informé et le fichier n’est pas envoyé.
- Si le récepteur a accepté, la réponse doit contenir l’adresse IP  et le port d’écoute du récepteur pour la connection pair-à-pair. 
- L’émetteur se connecte alors directement au récepteur, et lui envoie le fichier en direct, sans passer par le serveur (type FILE_SEND).
- Une fois le fichier reçu, le récepteur confirme la réception (type FILE_ACK).

Dans ce jalon, il faut utiliser les types : FILE_REQUEST, FILE_ACCEPT, FILE_REJECT, FILE_SEND et FILE_ACK.

Les champs **infos** doivent contenir les valeurs suivantes en fonction des cas : 
 - Pour **FILE_REQUEST**, le champ **infos** contient le pseudo de l’utilisateur à qui envoyer le fichier. Le nom du fichier se trouvera dans le payload.
- Pour  **FILE_ACCEPT**, le champ **infos** contient le pseudo de l’utilisateur qui avait envoyé le message FILE_REQUEST. Le payload du message contient l’adresse et le port sur lequel le récepteur écoutera la connexion de l’émetteur (de la forme “addr:port”, par exemple : “127.0.0.1:8081”).
- Pour **FILE_REJECT**, le champ **infos** contient le pseudo de l’utilisateur qui avait envoyé le message FILE_REQUEST.
- Pour **FILE_SEND**, le champ **infos** contient le nom du fichier qui est envoyé. Le payload contient les données du fichier lui-même. Attention, ce fichier n’est pas obligatoire un fichier texte et peut contenir des caractères ‘\0’. Il ne faut donc pas utiliser de fonctions propres à la lecture des chaînes de caractères sur ce payload (comme strlen(), strcpy(), strcmp(), etc.).
- Pour **FILE_ACK**, le champ **infos** contient le nom du fichier qui a été correctement reçu par le récepteur.

### Exigences
**Req 5.1** : Un utilisateur (l'émetteur) doit pouvoir envoyer un fichier à un autre utilisateur (le récepteur).

**Req 5.2** : Lors du transfert d'un fichier, le récepteur doit donner son approbation.

**Req 5.3** : Si le récepteur accepte l’échange de fichier, l’émetteur soit pouvoir se connecter directement au récepteur le temps de lui envoyer le fichier.

**Req 5.4** : Si le récepteur refuse l’échange de fichier, l’émetteur doit en être informé.

**Req 5.5** : Lors du transfert d'un fichier, le récepteur et l'émetteur doivent avoir confirmation que l'envoi s'est déroulé correctement.

Exemple de fonctionnement : 

```
%terminal_user1> /send user2 "/home/user/file.txt"
                            %terminal_user2> user1 wants you to accept the
                            transfer of the file named "file.txt". Do you
                            accept? [Y/N]
                            %terminal_user2> Y
%terminal_user1> user2 accepted file transfert.
%terminal_user1> Connecting to user2 and sending the file...
                            %terminal_user2> Receiving the file from 
                            user1...
                            %terminal_user2> file.txt saved in 
                            .re216/inbox/file.txt
%terminal_user1> user2 has received the file.

%terminal_user1> /send user2 "/home/user/correction_du_projet.txt"
                            %terminal_user2> user1 wants you to accept the 
                            transfer of the file named 
                            "correction_du_projet.txt". Do you accept? 
                            [Y/N]
                            %terminal_user2> N
%terminal_user1> user2 cancelled file transfer.
```


# Tips and Tricks
[Top](#re216-\--projet-de-programmation-réseau)

## Debugger les segfault sans printf
Si votre programme crash à cause d'un problème mémoire ou tout autre problème, vous pouvez identifier la ligne exacte en utilisant gdb.

```
    gdb --args path/to/program/prog localhost 8080
```


notez le --args qui vous permet de passer des arguments à votre programme.

Vous entrez alors dans l'interface de GDB.

Tapez "run" (ou "r") pour lancer l'application.

```
    (gdb) r
    Starting program: path/to/program/prog arg1 arg2

    Program received signal SIGSEGV, Segmentation fault.
    0x000000000040085b in main (argc=3, argv=0x7fffffffdda8) at path/to/program/prog.c:24
    24  printf("%d",*d);
    (gdb)  
```

de là, vous pouvez voir la ligne qui pose problème et même voir la pile d'appel en tapant "backtrace" (ou "bt")

```
(gdb) bt
#0  0x0000000000400849 in do_ () at path/to/program/prog.c:14
#1  0x00000000004008a2 in main (argc=3, argv=0x7fffffffdda8) at path/to/program/prog.c:28
(gdb) 
```

Vous pouvez même utiliser gdb pour afficher la valeur des variables.

```
(gdb) p ma_variable
$1 = (int *) 0x0
(gdb) 
```

Pour quitter gdb, faites quit

## Se connecter à votre serveur sans passer par le client
Votre serveur est un serveur de socket TCP. Telnet est un client TCP, vous pouvez donc l'utiliser pour vous connecter et envoyer directement des inputs au serveur. Imaginons que votre serveur écoute sur le port 8080, la commande suivante vous permet de vous connecter au serveur et taper directement des commandes. Vous recevrez également ses réponses. Pour quitter telnet, faites CTRL + ALT + ] et taper quit

```telnet localhost 8080```

## Se faire passer pour un serveur pour votre client
la commande nc permet d'émuler un serveur écoutant sur un port donné. Par exemple, pour écouter sur le port 8080, tapez la commande suivante. Vous pourrez envoyer et recevoir des commandes de la part de votre client.

```nc -l 8080```

## Savoir combien de socket sont ouvertes pour le serveur
Utile pour être sûr que vous ne laissez pas trainer vos sockets

```lsof -c path/to/program/serveur 2>/dev/null|grep TCP|wc -l```


## Tester les fuites mémoire de votre programme

```Valgrind path/to/program/serveur ```

# Rappel de C
[Top](#re216-\--projet-de-programmation-réseau)

## Structures
Syntaxe pour déclarer les structures :

```
struct module {
    int moduleId;
    double moduleGrade;
    char padding[20];
};
```

Syntaxe pour déclarer une variable de type structure

``` struct module re216;```


Syntaxe pour accéder aux champs d'une structure

```
struct module re216;
re216.moduleId = 5
re216.moduleGrade = 12.5;
```

Les structures peuvent être manipulées avec des pointeurs aussi

```
struct module re216;
struct module *pre216 = &re216;
pre216->moduleId = 5;
pre216->moduleGrade = 12.5;
```

On peut créer des alias pour simplifier le nommage des structures

```
typedef struct module s_module ;

s_module re216;
re216.moduleId = 1;
re216.moduleGrade = 12.5;
```


## Pointeurs
Les types de base : int, double, float, char

Les pointeurs correspondants : int*, double*, float*, char*

Obtenir le pointeur d'une variable déjà déclarée, utiliser &

```
int a;
int *pa = &a;
```

À l'inverse, pour obtenir la valeur pointée utiliser *

```
int a = 5;
int *pa = &a; 
if ((*pa) == 5){ // }
```

Les pointeurs fonctionnent aussi avec les structures, mais avec l'opérateur ->

```
struct module re216; 
re216.moduleId = 5; 
struct module *p_re216 = &re216;
re216->moduleId = 5; //utilise -> et pas le .
```

Passer un pointeur en paramètre d'une fonction

```
int func(int* a, int* b){
	return *a+*b;
}
...
int a = 5;
int b = 7;
int res;
res = func(&a,&b);
if (res == 7) { // }
```


## Conversion de type
On peut convertir les types en C avec l'opérateur (.)

Ça marche pour les types de base: 


```
int sum = 17, count = 5;
double mean;
mean = (double) sum / count;
```

Mais c'est surtout utile pour les pointeurs.

```
int main(int argc, char** argv) {

//create a pointer to a structure allocated on the heap with malloc
struct information *info = malloc(sizeof(struct module));

//clean the data
memset(info, 0, sizeof(mod));

//fill it up with some data
strcpy(info->base, "firstname"); 
strcpy(info->base+12, "lastname");

//mod->base is firstname___lastname____
printf("who am I: %s %s \n",info->base,info->base+10);

//but we could also cast the structure to the student structure, and access directly fname and lname
struct student * stu = (struct student*) info;

//stu->fname is firstname  stu->lastname is lastname
printf("who am I 2: %s %s\n", stu->fname, stu->lname);
free(mod);

}
```

[Top](#re216-\--projet-de-programmation-réseau)

