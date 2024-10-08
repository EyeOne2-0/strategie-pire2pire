# Document sur la stratégie de sécurisation de pire2pire.

### Introduction

Application security is a fundamental concern in the development of any digital platform. To effectively protect users and data, a rigorous and methodical approach is required. This document outlines the essential strategies to implement in order to ensure the security of an application, particularly for a platform like pire2pire.com, while also complying with legal and regulatory requirements such as GDPR. We will discuss two key concepts in cybersecurity: defense in depth and attack surface reduction, along with the implementation of GDPR, which is critical for the protection of personal data.

### **Défense en profondeur**
La défense en profondeur repose sur le principe de multiplier les couches de sécurité pour protéger une application. Chaque couche agit comme une barrière, rendant plus difficile l'accès aux ressources sensibles. Cette stratégie est cruciale car elle permet de renforcer la résilience de l'application face aux attaques, en évitant qu'une seule faille ne compromette l'ensemble du système.

Pour mettre en place une défense en profondeur, il faut :
- **Segmenter** les systèmes et les réseaux pour réduire l'impact potentiel d'une attaque.
- **Isoler** les services critiques afin de limiter les interactions non autorisées.
- Appliquer des **contrôles de sécurité à plusieurs niveaux**, comme des pare-feu, la surveillance réseau, et des politiques de sécurité sur les applications.
- Utiliser des mécanismes de **chiffrement**, de **détection des intrusions** et des systèmes d'authentification forts à chaque niveau.

### **Réduction de la surface d'attaque**
Réduire la surface d'attaque consiste à limiter le nombre de points d'entrée possibles pour les attaquants. Moins il y a de points vulnérables, moins les attaquants ont de chances de réussir à infiltrer le système. C'est une stratégie essentielle pour minimiser les risques de cyberattaques.

Pour réduire la surface d'attaque, il faut :
- Désactiver ou supprimer les services et fonctionnalités non utilisés.
- Restreindre l'accès aux ressources et aux services critiques.
- Veiller à ce que les applications ne fournissent que le strict nécessaire en termes de fonctionnalités publiques.
- Utiliser des technologies comme des **pare-feu applicatifs** pour filtrer les accès non autorisés.

### **RGPD (Règlement Général sur la Protection des Données)**
Le RGPD vise à protéger les données personnelles des utilisateurs en imposant des règles strictes sur la collecte, le traitement, et la conservation de ces informations. En tant qu'application qui gère des données d'utilisateurs, *pire2pire.com* doit se conformer à cette réglementation pour éviter des sanctions légales, mais aussi pour assurer la confiance des utilisateurs.

Pour être conforme au RGPD, il est nécessaire de :
- Mettre en place des **politiques de confidentialité claires**, expliquant comment les données sont utilisées.
- Obtenir un **consentement explicite** des utilisateurs pour la collecte et le traitement de leurs données.
- Proposer des **mécanismes de gestion des droits** des utilisateurs, comme l'accès à leurs données ou leur suppression.
- S'assurer de la **sécurisation des données** (chiffrement, pseudonymisation) pour éviter toute fuite ou accès non autorisé.

---

# **Back-End**
Le back-end d'une application est l'endroit où se déroulent la logique centrale, le traitement des données et la communication entre l'interface utilisateur et la base de données. Il est crucial de mettre en œuvre des pratiques de sécurité solides à ce niveau, car il traite souvent des informations sensibles et constitue une cible privilégiée pour les attaques. Les sections suivantes abordent des principes clés pour sécuriser le back-end, en commençant par la politique de moindre privilège et le contrôle d'accès basé sur les rôles (RBAC).

## **Politique de moindre privilège**
La politique de moindre privilège repose sur l'idée que chaque utilisateur ou composant d'un système ne devrait avoir accès qu'aux ressources et aux permissions strictement nécessaires pour accomplir sa tâche. Cela réduit le risque d'accès non autorisé ou d'exploitation d'une faille. En limitant les privilèges, on empêche qu'une éventuelle compromission ne s'étende à l'ensemble du système.

Cette politique permet de se prémunir contre les abus de privilèges et les attaques internes ou externes qui visent à exploiter des droits excessifs. Elle est particulièrement utile dans les environnements où plusieurs utilisateurs, services ou microservices interagissent avec des ressources sensibles. En limitant chaque acteur à son strict périmètre, on minimise l'impact potentiel d'une attaque.

#### **RBAC (Role-Based Access Control)**
Le **contrôle d'accès basé sur les rôles** (RBAC) est un modèle de gestion des droits où les utilisateurs se voient attribuer des rôles en fonction de leur fonction ou de leur position dans l'organisation. Chaque rôle est associé à un ensemble de permissions, ce qui permet une gestion centralisée et plus simple des accès.

RBAC s'intègre parfaitement avec la politique de moindre privilège, car il permet de restreindre l'accès aux seules ressources nécessaires en fonction du rôle d'un utilisateur. Par exemple, un administrateur pourrait avoir accès à des paramètres critiques du système, tandis qu'un utilisateur régulier serait limité à des actions plus simples et moins risquées.

---


## Base de Données (BDD)

### **Politique des mots de passe**

Une gestion efficace des mots de passe est cruciale pour protéger les utilisateurs et les systèmes contre de nombreuses menaces. Voici les principales pratiques à adopter et les menaces qu'elles permettent de contrer :

- **Hachage**  
  Le hachage transforme les mots de passe en une série de caractères illisibles grâce à une fonction cryptographique. Même si une base de données est compromise, les mots de passe ne sont pas exposés directement. L'utilisation d'algorithmes de hachage robustes comme **bcrypt** ou **Argon2** rend très difficile la récupération du mot de passe original. Cela protège contre l'exposition des mots de passe en cas de fuite de données.

- **Salage**  
  Le salage ajoute une donnée aléatoire unique (appelée **sel**) à chaque mot de passe avant de le hacher. Même si deux utilisateurs ont le même mot de passe, leurs hachages seront différents grâce au sel. Cette technique empêche les attaques basées sur les **rainbow tables**, qui utilisent des correspondances préconstruites entre mots de passe et hachages.

- **Complexité**  
  Exiger des mots de passe complexes (utilisant des lettres majuscules et minuscules, des chiffres et des caractères spéciaux) augmente la difficulté à deviner ou casser un mot de passe. Cela réduit l'efficacité des attaques par dictionnaire, où des mots de passe courants sont testés, et diminue le risque d'utilisation de mots de passe simples comme "123456".

- **Longueur minimale**  
  Plus un mot de passe est long, plus il est difficile à casser, même avec des attaques automatisées. Une longueur minimale de **12 caractères** est recommandée pour résister aux attaques par force brute, où toutes les combinaisons possibles sont testées. Chaque caractère supplémentaire rend l'attaque exponentiellement plus complexe.

- **Robustesse**  
  La robustesse d'un mot de passe provient de sa complexité et de sa longueur combinées. Des mots de passe robustes sont plus résistants aux attaques automatisées. Encourager l'utilisation de gestionnaires de mots de passe permet de créer des mots de passe uniques et complexes pour chaque service, réduisant ainsi les risques de compromission dus à la réutilisation des mots de passe.


Voici une explication sur l'utilisation des UUID, ainsi que les menaces que cette pratique permet de contrer :


### **Utilisation des UUID**

Les **UUID** (Universally Unique Identifiers) sont des identifiants uniques utilisés pour attribuer des références distinctes à des objets, utilisateurs, sessions ou autres entités dans un système. Un UUID est une chaîne alphanumérique générée de manière à être unique, ce qui garantit qu'il n'y aura pas de conflit ou de duplication entre les différents identifiants.

Les UUID sont souvent utilisés à la place des identifiants incrémentaux classiques (comme des identifiants numériques), qui peuvent être prévisibles et sujets à des attaques.

#### Menaces contrées par l'utilisation des UUID :

- **Attaques par prédiction d'ID**  
  Les identifiants incrémentaux peuvent être facilement devinés par un attaquant, permettant à celui-ci d'accéder à des ressources ou des informations associées à d'autres utilisateurs en devinant leurs ID. Avec un UUID, l'identifiant est aléatoire et donc pratiquement impossible à deviner. Cela protège contre les attaques comme l’énumération des ressources ou des utilisateurs.

- **Attaques par force brute**  
  Les UUID, avec leur longueur (généralement 128 bits), sont bien plus complexes que des identifiants numériques séquentiels ou plus courts. Cela rend les attaques par force brute inefficaces, car tester un grand nombre d'UUIDs aléatoires pour obtenir une correspondance prendrait un temps considérable.

- **Réutilisation d'ID**  
  Dans les systèmes où les identifiants peuvent être réutilisés après la suppression d'une entrée (par exemple, un utilisateur ou un objet supprimé), cela peut créer des conflits ou permettre à des attaquants d'accéder à des informations sensibles liées à un ancien utilisateur. Avec un UUID, chaque identifiant est unique pour toute la durée de vie de l'objet, éliminant le risque de réutilisation accidentelle.

- **Énumération des objets ou des utilisateurs**  
  Lorsque les identifiants sont séquentiels, un attaquant peut facilement itérer sur les ID pour énumérer des objets ou des comptes utilisateurs. L'utilisation d'UUID empêche cette énumération, car chaque identifiant est aléatoire et ne suit pas un schéma prédictible.

Voici une version en liste à puces de la **politique de rétention** avec une explication sur les menaces, en particulier les ransomwares :


### **Politique de rétention**

La politique de rétention des données définit comment les sauvegardes sont effectuées et conservées sur une certaine période, garantissant ainsi que les données critiques soient toujours disponibles en cas d'incident. Une bonne politique de rétention est essentielle pour protéger contre les pertes de données et les attaques, notamment les ransomwares.

- ### **Sauvegarde**

  - **Automatisation**  
    L’automatisation des sauvegardes garantit que les données sont régulièrement sauvegardées sans intervention humaine, minimisant ainsi les risques d’oubli ou d'erreur humaine.

    - **Nombre**  
      Il est important de définir combien de copies de sauvegarde sont effectuées à chaque cycle pour assurer que des versions antérieures des données soient toujours disponibles en cas de corruption ou d'attaque.

    - **Fréquence**  
      La fréquence des sauvegardes doit être suffisamment élevée pour garantir que les données critiques puissent être restaurées sans perte importante. Une fréquence trop faible pourrait laisser un intervalle pendant lequel des modifications importantes des données seraient perdues en cas d'attaque.

    L'automatisation des sauvegardes protège contre les erreurs humaines et garantit que les données sont régulièrement sauvegardées, minimisant l'impact d'une attaque par ransomware. En cas d'attaque, il est possible de restaurer une version antérieure des données sans payer la rançon.

- ###  **Politique de rétention**

  - **Nombre de sauvegardes**  
    Il est essentiel de conserver plusieurs versions des sauvegardes, permettant de revenir à une version antérieure en cas de problème avec une sauvegarde récente (corruption, attaque ransomware).

  - **Support (stockage)**  
    Les sauvegardes doivent être stockées sur des supports sécurisés, idéalement isolés du réseau principal pour empêcher les ransomwares d'y accéder. Des solutions comme les **stockages hors-ligne** ou **cloud sécurisé** peuvent offrir une protection supplémentaire contre les attaques.

    Les ransomwares ciblent souvent les fichiers et bases de données critiques. Une bonne politique de rétention avec des sauvegardes stockées sur des supports sécurisés permet de restaurer les données même si l'attaque a chiffré les données en production. En conservant plusieurs versions, les administrateurs peuvent choisir une version saine à restaurer.

---


## API

### **Sécurisation des communications (API)**

La sécurisation des communications entre les clients et les serveurs API est cruciale pour protéger les échanges de données sensibles. Les protocoles **TLS** et **HSTS** jouent un rôle clé dans la protection contre diverses attaques visant les API.

- **TLS (Transport Layer Security)**  
  TLS est utilisé pour chiffrer les communications entre le client (souvent une application ou un navigateur) et le serveur API. Cela garantit que les données échangées restent privées et ne peuvent pas être modifiées en cours de route.

  **Cela permet de se protéger contre :**  
  - **Attaques de type man-in-the-middle (MITM)** : TLS empêche un attaquant d'intercepter ou d'injecter des données dans les requêtes API en s'assurant que les données transmises sont chiffrées et authentifiées.
  - **Écoutes clandestines** : TLS protège les communications API en empêchant les attaquants d'accéder aux données sensibles transmises, comme les identifiants d'authentification ou les données utilisateur.
  - **Altération des données** : En assurant l'intégrité des messages, TLS garantit que les requêtes et réponses API n'ont pas été modifiées par un tiers malveillant pendant leur transit.

- **HSTS (HTTP Strict Transport Security)**  
  HSTS est une politique de sécurité utilisée pour les API accessibles via des navigateurs ou des applications web, qui force l'utilisation du HTTPS pour toutes les communications. Cela garantit que les API ne seront jamais appelées via HTTP, même si l'utilisateur ou l'application tente de le faire.

  **Cela permet de se protéger contre :**  
  - **Attaques par downgrade** : HSTS empêche les attaquants d'abaisser la connexion vers un protocole non sécurisé (HTTP) en forçant systématiquement le HTTPS. Cela est particulièrement utile pour éviter les attaques comme le SSL stripping.
  - **Accès non sécurisé** : HSTS garantit que toutes les interactions avec les API se font via des canaux sécurisés (HTTPS), empêchant ainsi la transmission de données sensibles en clair.


Voici une structure pour la section **Sécurité des origines** dans le cadre de la sécurisation des API, en utilisant des concepts comme SOP, CORS, CSP et ORM :


### **Sécurité des origines**

La sécurité des origines est un aspect fondamental dans la protection des échanges entre différents domaines (origines) et des interactions avec des ressources externes. Les politiques telles que **SOP**, **CORS**, et **CSP** permettent de contrôler et de restreindre les accès aux ressources d'une application, tandis que l'utilisation d'un **ORM** contribue à la sécurité des interactions avec la base de données.

- **SOP (Same-Origin Policy)**  
  La politique de même origine (SOP) est un mécanisme de sécurité des navigateurs qui limite les interactions entre des ressources provenant de différentes origines (domaine, protocole, port). Elle assure qu'une page web ou une API ne peut interagir qu'avec des ressources provenant de la même origine.

  **Cela permet de se protéger contre :**  
  - **Attaques Cross-Site Scripting (XSS)** et **Cross-Site Request Forgery (CSRF)** : SOP empêche une page malveillante de faire des requêtes non autorisées vers une autre origine (API), protégeant ainsi contre les attaques qui tentent de voler des informations ou d’exécuter des actions à l’insu de l’utilisateur.

- **CORS (Cross-Origin Resource Sharing)**  
  CORS permet de définir quelles origines peuvent interagir avec l'API. Cela est utile pour autoriser certaines applications ou domaines spécifiques à accéder à une API depuis une origine différente.

  **Cela permet de se protéger contre :**  
  - **Accès non autorisé aux ressources d'une API** : En spécifiant quelles origines sont autorisées à effectuer des requêtes vers l’API, CORS protège contre les attaques provenant de domaines non approuvés.
  - **Réduire les risques de fuites de données** : CORS assure que seules les origines de confiance peuvent accéder aux ressources sensibles de l’API, minimisant ainsi les risques de transmission de données à des domaines malveillants.

- **CSP (Content Security Policy)**  
  CSP permet de contrôler quelles ressources (scripts, styles, images, etc.) peuvent être chargées par une application ou une page web. En définissant une politique de sécurité du contenu, il est possible de restreindre le chargement de ressources provenant d’origines non approuvées.

  **Cela permet de se protéger contre :**  
  - **Attaques par injection (XSS)** : CSP limite l'exécution de scripts provenant de sources non autorisées, empêchant les attaquants d'injecter des scripts malveillants dans l’application web ou dans les réponses API.
  - **Exécution de contenu non sécurisé** : CSP permet de restreindre les ressources à des domaines spécifiques de confiance, évitant ainsi le chargement de contenu provenant de serveurs compromis ou non sécurisés.

- **Utilisation d'un ORM (Object-Relational Mapping)**  
  Un ORM est une technique qui permet de manipuler des bases de données relationnelles en utilisant des objets plutôt que du code SQL direct. L’ORM assure une abstraction des requêtes SQL, empêchant l'injection de code SQL malveillant dans les applications.

  **Cela permet de se protéger contre :**  
  - **Injection SQL** : En utilisant un ORM, les requêtes SQL sont générées automatiquement par le framework, évitant les erreurs de manipulation de données qui pourraient permettre des attaques d'injection SQL. Cela protège les bases de données de toute exécution de commandes malveillantes introduites via des entrées non sécurisées.
  - **Accès non contrôlé aux données** : L’ORM gère les interactions avec la base de données de manière sécurisée, évitant la manipulation directe des requêtes SQL qui pourrait exposer des données sensibles en cas de mauvaise implémentation.


### **Authentification**

L'authentification est essentielle pour s'assurer que seules les entités autorisées peuvent interagir avec une API. L'utilisation de tokens pour authentifier les utilisateurs et la limitation des appels API contribuent à la sécurité et à la performance des services.

- **Token**  
  Les tokens sont des jetons d'authentification utilisés pour valider l'identité des utilisateurs ou des systèmes qui interagissent avec une API. Après une authentification réussie, un token est émis, souvent sous forme de **JWT (JSON Web Token)**, et inclus dans chaque requête à l'API. Ces tokens contiennent généralement des informations telles que l'identité de l'utilisateur, le temps d'expiration, et les permissions associées.  
  **Cela permet de se protéger contre :**
  - **Accès non autorisé** : Les tokens garantissent que seules les entités ayant fourni les informations correctes lors de l'authentification peuvent accéder aux ressources API.
  - **Usurpation d'identité** : En utilisant des tokens sécurisés et souvent chiffrés, il est difficile pour un attaquant de falsifier un token pour accéder à l'API sans autorisation.

- **Limitation d'appel API**  
  La **limitation d'appel API** (ou **rate limiting**) impose un nombre maximum de requêtes qu'un utilisateur ou une application peut envoyer à l'API sur une période définie. Cela empêche les abus, les attaques par déni de service (DoS) et assure la bonne gestion des ressources du serveur.

  **Cela permet de se protéger contre :**
  - **Attaques par déni de service (DoS)** : Limiter le nombre d'appels API par utilisateur ou application empêche les attaquants de surcharger le serveur avec des requêtes malveillantes.
  - **Abus de ressources** : En contrôlant la fréquence des requêtes, on s'assure que les utilisateurs ne consomment pas de manière excessive les ressources, garantissant ainsi une meilleure disponibilité de l'API pour tous les utilisateurs légitimes.


### *Front-end*

#### Introduction
- *Jamais faire confiance au client (navigateur) -> règle d'or* 

#### Protocoles de sécurité (côté front-end)
- HTTP + TLS = HTTPS
    - HSTS
    - TLS
- SOP
- CSP
  - Referrer Policy
  - SRI