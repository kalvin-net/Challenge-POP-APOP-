# ![WRITEUP copy](https://github.com/user-attachments/assets/cc4a2333-10c3-47e3-b3ff-0eef936456d0)

## 🎯 Objectif : Retrouver le mot de passe de l’utilisateur dans la trame réseau

## **Introduction à POP-APOP**
> POP-APOP est une méthode d'authentification sécurisée pour le protocole POP3. Lors de la connexion à un serveur de messagerie POP3, APOP utilise un challenge unique envoyé par le serveur, combiné avec le mot de passe de l'utilisateur, pour créer un hachage cryptographique. Ce hachage est ensuite envoyé au serveur pour vérification. Cette méthode empêche l'envoi de mots de passe en clair, réduisant ainsi les risques d'interception et de compromission des informations d'identification.
## Compréhension du Mécanisme POP - APOP

- **Qu'est-ce que le protocole POP ?**
> Le protocole POP (Post Office Protocol) est un protocole standard utilisé pour récupérer des courriels depuis un serveur de messagerie jusqu'à un client de messagerie. POP est l'un des protocoles les plus anciens et il est principalement utilisé pour télécharger les courriels sur un ordinateur local et les consulter hors ligne.

![schema-fonctionnement-protocole-pop-768x483](https://github.com/user-attachments/assets/d50ced9a-1647-464d-aad9-5e0ffd7c5e4e)

-  **🔐  Qu'est-ce que l'authentification APOP?**
> L'authentification APOP (Authenticated Post Office Protocol) est une méthode d'authentification utilisée avec le protocole POP3 pour sécuriser le processus de connexion entre un client de messagerie et un serveur de messagerie. APOP vise à protéger les informations de connexion (nom d'utilisateur et mot de passe) contre les interceptions en utilisant une forme de cryptographie MD5($pass.$salt).

> APOP ajoute une couche de sécurité en utilisant un challenge-response pour l'authentification, ce qui rend plus difficile pour un attaquant de capturer et de réutiliser les informations de connexion.

## **Schéma succinct**

> ![Diagramme sans nom drawio (1)](https://github.com/user-attachments/assets/6ec75ccc-f87e-4ed8-866f-190ff74d438b)

> _Ce processus sécurise l'authentification en protégeant les mots de passe contre les interceptions en clair._

## 🎯  SOLUTION

### Outils à utiliser : 

> Internet / Wireshark / Kali-linux / Worldlist / Hash-Identifier / John The Ripper

 1. **Extraction et Analyse**
   
 - Téléchargéons le fichier **ch23.zip.** Décompressons-le, et nous obtiendrons un fichier **pcapng** qui s'ouvrira dans **Wireshark**.

> Le nom du défi nous donne un indice utile sur le fait que ce défi est basé sur le protocole POP et l'authentification APOP.

 - Utilisons l'option de filtrage pour filtrer les paquets **POP** dans Wireshark..

- Après avoir examiné les paquets, nous avons appris que l'authentification APOP est utilisée pour crypter le mot de passe suivant : **4ddd4137b84ff2db7291b568289717f0.**
> ![Capture d'écran 2024-07-23 124144](https://github.com/user-attachments/assets/c6cc5f62-e722-4f2d-8e18-da13fcf100e5)

- Identifions le type de hachage à l'aide de l'outil **hash-identifier**
> ![Capture d'écran 2024-07-23 132120](https://github.com/user-attachments/assets/a9c34463-a11f-4d65-a499-22faf257eba8)

2. **Crack du Mot de Passe**

   - Installons le **Wordlists :**
  > - sudo apt-get install wordlists
  > - sudo gunzip /usr/share/wordlists/rockyou.txt.gz

 - Nous allons maintenant installer l'outil **John The Ripper** dans le Kali-linux pour déchiffrer le mot de passe.
   > - wget https://github.com/openwall/john/archive/refs/heads/bleeding-jumbo.zip -O john.zip
   > - unzip john.zip
   > - cd john-bleeding-jumbo/src
   > - ./configure && make

 - Créons un format dynamique dans le répertoire d'exécution **sudo nano /usr/share/john/john-local.conf**  afin de permettre le craquage de mots de passe en utilisant une expression MD5 personnalisée en ajoutant la configuration suivante:
   
> List.Generic:dynamic_1520]
> Expression=md5(CONST:$p) (md5 with prefix password)
> Flag=MGF_FLAT_BUFFERS
> CONST1=<1755.1.5f403625.BcWGgpKzUPRC8vscWn0wuA==@vps-7e2f5a72>
> MaxInputLen=70
> Func=DynamicFunc__clean_input
> Func=DynamicFunc__append_input1_from_CONST1
> Func=DynamicFunc__append_keys
> Func=DynamicFunc__crypt
> # Test with RFC example
> Test=$dynamic_1520$7b11054a9dd9230eedf08e59e3d90760:tanstaaf

  ![Scripts_JTR](https://github.com/user-attachments/assets/5b7671ae-c51e-45bf-81bc-d4ca5a3f06ea)
      
 - Créons un fichier texte contenant le hach MD5 que nous allons déchiffrer : **echo "4ddd4137b84ff2db7291b568289717f0" > hash_flag.txt**

 - Effectuons le décryptage final en exécutant la commande suivante pour lancer John The Ripper avec le format dynamique que nous avons défini et un dictionnaire de mots de passe : **john --format=dynamic_1520 hash_flag.txt --wordlist=/usr/share/wordlists/rockyou.txt --fork=4**  

> ![John_The_Ripper](https://github.com/user-attachments/assets/532456a9-a049-49d7-b9a6-c3bc815398aa)

## 🎯  CONCLUSION: 
> En suivant ces étapes, j'ai pu déchiffrer le mot de passe de l'utilisateur à partir des trames réseau capturées. Ce défi démontre l'efficacité des outils de décryptage modernes et la nécessité de comprendre les protocoles de sécurité.

