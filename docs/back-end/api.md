# API

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


Voici une version plus développée pour la section **Front-end**, avec une introduction approfondie sur la règle d'or de ne jamais faire confiance au client (navigateur) :
