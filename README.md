# Challenge : POP-APOP WRITEUP

## Énoncé : Retrouver le mot de passe de l’utilisateur dans la trame réseau

## **Préambule de POP-APOP**
> POP-APOP est une méthode d'authentification sécurisée pour le protocole POP3. Lors de la connexion à un serveur de messagerie POP3, APOP utilise un challenge unique envoyé par le serveur, combiné avec le mot de passe de l'utilisateur, pour créer un hachage cryptographique. Ce hachage est ensuite envoyé au serveur pour vérification. Cette méthode empêche l'envoi de mots de passe en clair, réduisant ainsi les risques d'interception et de compromission des informations d'identification.

##  **Qu'est-ce que le protocole POP ?**
> Le protocole POP (Post Office Protocol) est un protocole standard utilisé pour récupérer des courriels depuis un serveur de messagerie jusqu'à un client de messagerie. POP est l'un des protocoles les plus anciens et il est principalement utilisé pour télécharger les courriels sur un ordinateur local et les consulter hors ligne.

## **Fonctionnement de POP**
_Le protocole POP fonctionne selon les étapes suivantes:_

- **Connexion au serveur:** Le client de messagerie (comme Outlook, Thunderbird ou un client de messagerie intégré) se connecte au serveur de messagerie via POP.
- **Authentification :** L'utilisateur s'authentifie en fournissant son nom d'utilisateur et son mot de passe.
- **Téléchargement des emails :** Tous les courriels présents sur le serveur sont téléchargés sur le client local.
- **Suppression sur le serveur (optionnel) :** Par défaut, une fois les courriels téléchargés, ils peuvent être supprimés du serveur. Cependant, cette option peut être configurée pour laisser une copie des courriels sur le serveur.

![667502571004235776](https://github.com/user-attachments/assets/edc7cfed-c6da-40f4-a4da-06f9a7efba67)

## **Versions de POP**

**Il existe plusieurs versions de POP :**
- **POP1 :** La première version de POP, peu utilisée aujourd'hui.
- **POP2 :** Une version améliorée, également obsolète.
- **POP3 :** La version la plus utilisée actuellement. Elle offre plus de fonctionnalités et est standardisée par le RFC 1939

##  **Qu'est-ce que l'authentification APOP?**
> L'authentification APOP (Authenticated Post Office Protocol) est une méthode d'authentification utilisée avec le protocole POP3 pour sécuriser le processus de connexion entre un client de messagerie et un serveur de messagerie. APOP vise à protéger les informations de connexion (nom d'utilisateur et mot de passe) contre les interceptions en utilisant une forme de cryptographie.

## **Fonctionnement de l'authentification APOP**
> APOP ajoute une couche de sécurité en utilisant un challenge-response pour l'authentification, ce qui rend plus difficile pour un attaquant de capturer et de réutiliser les informations de connexion. Voici comment cela fonctionne :

- **Connexion au serveur :**
> Le client de messagerie se connecte au serveur POP3.

- **Envoi du challenge :**
> Le serveur POP3 envoie un challenge unique (généralement un timestamp ou une chaîne aléatoire) au client.

- **Génération de la réponse :**
> Le client de messagerie concatène le challenge avec le mot de passe de l'utilisateur.
> Le client applique ensuite une fonction de hachage (souvent MD5) au résultat pour produire un hachage.

- **Envoi de la réponse au serveur :**
> Le client envoie le hachage résultant au serveur POP3.

- **Vérification par le serveur :**
> Le serveur POP3, qui connaît le challenge et le mot de passe de l'utilisateur, exécute le même processus de hachage.
> Si le hachage généré par le serveur correspond à celui envoyé par le client, l'authentification est réussie.

## **Schéma succinct**
- **Connexion :** Le client se connecte au serveur POP3.
- **Challenge :** Le serveur envoie un challenge unique au client.
- **Hachage :** Le client concatène le challenge avec le mot de passe et génère un hachage MD5.
- **Envoi :** Le client envoie le hachage au serveur.
- **Validation :** Le serveur vérifie le hachage et authentifie le client si le hachage est correct.
> _Ce processus sécurise l'authentification en protégeant les mots de passe contre les interceptions en clair._
