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

## **Back-end**

#### Introduction
1. Politique de moindre privilège
- *Pourquoi ?*
- *Pour lutter contre quoi ? Dans quel contexte ?*
2. RBAC (Role-Based Access Control)

Voici une structure pour la section "Back-end" en français :

---

### **Back-End**
Le back-end d'une application est l'endroit où se déroulent la logique centrale, le traitement des données et la communication entre l'interface utilisateur et la base de données. Il est crucial de mettre en œuvre des pratiques de sécurité solides à ce niveau, car il traite souvent des informations sensibles et constitue une cible privilégiée pour les attaques. Les sections suivantes abordent des principes clés pour sécuriser le back-end, en commençant par la politique de moindre privilège et le contrôle d'accès basé sur les rôles (RBAC).

### **Politique de moindre privilège**
#### **Pourquoi ?**
La politique de moindre privilège repose sur l'idée que chaque utilisateur ou composant d'un système ne devrait avoir accès qu'aux ressources et aux permissions strictement nécessaires pour accomplir sa tâche. Cela réduit le risque d'accès non autorisé ou d'exploitation d'une faille. En limitant les privilèges, on empêche qu'une éventuelle compromission ne s'étende à l'ensemble du système.

#### **Pour lutter contre quoi ? Dans quel contexte ?**
Cette politique permet de se prémunir contre les abus de privilèges et les attaques internes ou externes qui visent à exploiter des droits excessifs. Elle est particulièrement utile dans les environnements où plusieurs utilisateurs, services ou microservices interagissent avec des ressources sensibles. En limitant chaque acteur à son strict périmètre, on minimise l'impact potentiel d'une attaque.

### **RBAC (Role-Based Access Control)**
Le **contrôle d'accès basé sur les rôles** (RBAC) est un modèle de gestion des droits où les utilisateurs se voient attribuer des rôles en fonction de leur fonction ou de leur position dans l'organisation. Chaque rôle est associé à un ensemble de permissions, ce qui permet une gestion centralisée et plus simple des accès.

RBAC s'intègre parfaitement avec la politique de moindre privilège, car il permet de restreindre l'accès aux seules ressources nécessaires en fonction du rôle d'un utilisateur. Par exemple, un administrateur pourrait avoir accès à des paramètres critiques du système, tandis qu'un utilisateur régulier serait limité à des actions plus simples et moins risquées.

---

Ce plan vous permet d’introduire les concepts essentiels de sécurité pour le back-end et d’expliquer les bénéfices de ces politiques.  


#### Base de Données (BDD)

- **Politique des mots de passe** :
  - *Hachage*
  - *Salage* 
  - *Complexité*
    - *Longueur minimale*
    - *Robustesse*
- Utilisation des UUID
- Politique de rétention :
    - Sauvegarde   
      - Automatisation
        - *Nombre*
        - *Fréquence*
    - Politique de rétention
        - Nombre de sauvegardes
        - Support (stockage)


#### API

- *Sécurisation des communications* :
  - TLS (Transport Layer Security)
  - HSTS

- **Sécurité des origines** :
  - *SOP (Same-Origin Policy) : même origine*
    - *CORS (Cross-Origin Resource Sharing) : différentes origines*
  - *CSP (Content Security Policy) : différentes ressources*
- *Utilisation d'un ORM (Object-Relational Mapping)*
- **Authentification** :
  - *Token*
- *Limitation d'appel API*

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