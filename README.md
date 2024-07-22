# Challenge: POP-APOP WRITEUP

##  **Qu'est-ce que le protocole POP ?**
> Le protocole POP (Post Office Protocol) est un protocole standard utilisé pour récupérer des courriels depuis un serveur de messagerie jusqu'à un client de messagerie. POP est l'un des protocoles les plus anciens et il est principalement utilisé pour télécharger les courriels sur un ordinateur local et les consulter hors ligne.

## **Fonctionnement de POP**
_Le protocole POP fonctionne selon les étapes suivantes:_

- **Connexion au serveur:** Le client de messagerie (comme Outlook, Thunderbird ou un client de messagerie intégré) se connecte au serveur de messagerie via POP.
- **Authentification:** L'utilisateur s'authentifie en fournissant son nom d'utilisateur et son mot de passe.
- **Téléchargement des emails:** Tous les courriels présents sur le serveur sont téléchargés sur le client local.
- **Suppression sur le serveur (optionnel):** Par défaut, une fois les courriels téléchargés, ils peuvent être supprimés du serveur. Cependant, cette option peut être configurée pour laisser une copie des courriels sur le serveur.
Versions de POP
## **Il existe plusieurs versions de POP:**

- **POP1:** La première version de POP, peu utilisée aujourd'hui.
- **POP2:** Une version améliorée, également obsolète.
- **POP3:** La version la plus utilisée actuellement. Elle offre plus de fonctionnalités et est standardisée par le RFC 1939

##  **Qu'est-ce que l'authentification APOP?**
> L'authentification APOP (Authenticated Post Office Protocol) est une méthode d'authentification utilisée avec le protocole POP3 pour sécuriser le processus de connexion entre un client de messagerie et un serveur de messagerie. APOP vise à protéger les informations de connexion (nom d'utilisateur et mot de passe) contre les interceptions en utilisant une forme de cryptographie.

## **Fonctionnement de l'authentification APOP**
> APOP ajoute une couche de sécurité en utilisant un challenge-response pour l'authentification, ce qui rend plus difficile pour un attaquant de capturer et de réutiliser les informations de connexion. Voici comment cela fonctionne :

- **Connexion au serveur:**
> Le client de messagerie se connecte au serveur POP3.

- **Envoi du challenge:**
> Le serveur POP3 envoie un challenge unique (généralement un timestamp ou une chaîne aléatoire) au client.

- **Génération de la réponse:**
> Le client de messagerie concatène le challenge avec le mot de passe de l'utilisateur.
> Le client applique ensuite une fonction de hachage (souvent MD5) au résultat pour produire un hachage.

- **Envoi de la réponse au serveur:**
> Le client envoie le hachage résultant au serveur POP3.

- **Vérification par le serveur:**
> Le serveur POP3, qui connaît le challenge et le mot de passe de l'utilisateur, exécute le même processus de hachage.
> Si le hachage généré par le serveur correspond à celui envoyé par le client, l'authentification est réussie.