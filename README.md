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

POP1 : La première version de POP, peu utilisée aujourd'hui.
POP2 : Une version améliorée, également obsolète.
POP3 : La version la plus utilisée actuellement. Elle offre plus de fonctionnalités et est standardisée par le RFC 1939

##  What is APOP Authentication?
> APOP (Authenticated POP) is an extension of the standard POP3 protocol. In simple words apop is used to encrypt the username or password.
