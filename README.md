# ![WRITEUP-VF](https://github.com/user-attachments/assets/531221b0-e4ad-4d4b-aa28-b07208b28506)

## 🎯 Énoncé : Retrouver le mot de passe de l’utilisateur dans la trame réseau

## **Préambule de POP-APOP**
> POP-APOP est une méthode d'authentification sécurisée pour le protocole POP3. Lors de la connexion à un serveur de messagerie POP3, APOP utilise un challenge unique envoyé par le serveur, combiné avec le mot de passe de l'utilisateur, pour créer un hachage cryptographique. Ce hachage est ensuite envoyé au serveur pour vérification. Cette méthode empêche l'envoi de mots de passe en clair, réduisant ainsi les risques d'interception et de compromission des informations d'identification.
## Compréhension du Mécanisme POP - APOP

- **Qu'est-ce que le protocole POP ?**
> Le protocole POP (Post Office Protocol) est un protocole standard utilisé pour récupérer des courriels depuis un serveur de messagerie jusqu'à un client de messagerie. POP est l'un des protocoles les plus anciens et il est principalement utilisé pour télécharger les courriels sur un ordinateur local et les consulter hors ligne.

![schema-fonctionnement-protocole-pop-768x483](https://github.com/user-attachments/assets/d50ced9a-1647-464d-aad9-5e0ffd7c5e4e)

-  **🔐 Qu'est-ce que l'authentification APOP?**
> L'authentification APOP (Authenticated Post Office Protocol) est une méthode d'authentification utilisée avec le protocole POP3 pour sécuriser le processus de connexion entre un client de messagerie et un serveur de messagerie. APOP vise à protéger les informations de connexion (nom d'utilisateur et mot de passe) contre les interceptions en utilisant une forme de cryptographie MD5($pass.$salt).

> APOP ajoute une couche de sécurité en utilisant un challenge-response pour l'authentification, ce qui rend plus difficile pour un attaquant de capturer et de réutiliser les informations de connexion.

## **Schéma succinct**

![Diagramme sans nom drawio (1)](https://github.com/user-attachments/assets/6ec75ccc-f87e-4ed8-866f-190ff74d438b)

> _Ce processus sécurise l'authentification en protégeant les mots de passe contre les interceptions en clair._

## SOLUTION

1. **Extraction et Analyse**
   
- Téléchargéons le fichier **ch23.zip.** Décompressons-le, et nous obtiendrons un fichier **pcapng** qui s'ouvrira dans **Wireshark**.

> Le nom du défi nous donne un indice utile sur le fait que ce défi est basé sur le protocole pop et l'authentification apop.

- Utilisons l'option filter pour filtrer les paquets **pop** dans Wireshark.

- Après avoir examiné les paquets, nous avons appris que l'authentification apop est utilisée pour crypter le mot de passe est: **4ddd4137b84ff2db7291b568289717f0.**
![Capture d'écran 2024-07-23 124144](https://github.com/user-attachments/assets/c6cc5f62-e722-4f2d-8e18-da13fcf100e5)

- Identifier le type de hachage à l'aide de l'outil **hash-identifier**
![Capture d'écran 2024-07-23 132120](https://github.com/user-attachments/assets/a9c34463-a11f-4d65-a499-22faf257eba8)

2. **Crack du Mot de Passe**
   
- Nous allons maintenant utiliser l'outil **John The Ripper** pour déchiffrer le mot de passe.

![John_The_Ripper](https://github.com/user-attachments/assets/532456a9-a049-49d7-b9a6-c3bc815398aa)

## CONCLUSION: 
> Ce challenge m'a montré l'importance de maîtriser les protocoles de communication et les mécanismes d'authentification. Après avoir analysé le fichier pcapng et identifié l'authentification APOP, j'ai utilisé John The Ripper pour craquer le mot de passe haché. Ce défi démontre l'efficacité des outils modernes de craquage et la nécessité de comprendre les protocoles de sécurité.

