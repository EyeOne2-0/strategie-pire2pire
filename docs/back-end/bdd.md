# Base de Données (BDD)

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

