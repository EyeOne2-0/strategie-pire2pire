# **Front-end**

### **Introduction**

Le front-end est la partie visible de l'application avec laquelle les utilisateurs interagissent directement. Bien que de nombreuses mesures de sécurité soient implémentées côté serveur, il est essentiel de ne pas négliger la sécurité du front-end. En effet, les vulnérabilités côté client peuvent être exploitées pour compromettre une application, voler des informations sensibles ou même prendre le contrôle de sessions utilisateur.

- **Jamais faire confiance au client (navigateur) – règle d'or**  
  La règle d'or de la sécurité dans le développement front-end est simple mais vitale : **ne jamais faire confiance au client**. 
  Le client, c'est-à-dire le navigateur de l'utilisateur, peut être manipulé à tout moment. Cela inclut la modification du JavaScript exécuté, la falsification des données envoyées au serveur, ou encore l'injection de scripts malveillants. Par conséquent, toute donnée provenant du client doit être considérée comme potentiellement non fiable ou dangereuse.

  Voici les raisons pour lesquelles il est crucial de ne jamais se fier uniquement au front-end pour la sécurité de l'application :

  - **Manipulation des données** :  
    Les utilisateurs peuvent manipuler les données envoyées par le navigateur à l'aide de simples outils de développement (comme les DevTools de Chrome) ou des scripts. Cela inclut la modification des formulaires HTML, la falsification des headers HTTP, ou l'envoi direct de requêtes API altérées. Par exemple, un utilisateur malveillant pourrait changer le prix d'un produit dans une application de commerce électronique avant d'envoyer la requête d'achat. Pour éviter cela, il est indispensable de toujours valider les données sur le serveur avant de les traiter.

  - **Contournement des validations** :  
    Les validations côté client sont souvent utilisées pour améliorer l'expérience utilisateur en fournissant des retours rapides (par exemple, vérifier la longueur d'un mot de passe ou s'assurer qu'un champ d'e-mail est correctement formaté). Cependant, un utilisateur malveillant peut facilement contourner ces validations en désactivant JavaScript ou en modifiant les requêtes. Par conséquent, toutes les validations doivent être répétées côté serveur, car le front-end ne peut pas être considéré comme une source fiable de contrôle.

  - **Attaques par injection** :  
    Le front-end est un point d'entrée pour plusieurs types d'attaques par injection, comme les attaques **XSS (Cross-Site Scripting)** ou les **injections SQL**. Un attaquant pourrait injecter du code malveillant dans des champs de saisie, comme des commentaires ou des formulaires de contact, qui seraient ensuite exécutés dans le navigateur d’un autre utilisateur ou envoyé directement au serveur si les données ne sont pas correctement filtrées. Le serveur doit donc toujours désinfecter et valider les entrées du client pour éviter l'exécution de scripts malveillants ou l'accès non autorisé à la base de données.

  - **Sécurité des sessions** :  
    Le front-end n'est pas responsable de la gestion des sessions de manière sécurisée. Si un utilisateur malveillant obtient accès à un token ou un cookie de session via une attaque XSS, il pourrait se faire passer pour un utilisateur légitime. Il est donc crucial de mettre en place des mesures de sécurité côté serveur, comme l'utilisation de tokens à durée limitée, la sécurisation des cookies avec des attributs `HttpOnly` et `Secure`, ainsi que la gestion stricte des permissions et des rôles pour chaque utilisateur.

  - **Protection contre les attaques par force brute** :  
    Le front-end peut limiter la vitesse à laquelle un utilisateur tente de se connecter ou de soumettre un formulaire, mais cela ne suffit pas à bloquer des attaques automatisées à grande échelle. Il est indispensable que des contrôles supplémentaires, comme la **limitation des appels API** (rate limiting) et la détection d'activités suspectes, soient mis en place côté serveur pour éviter les attaques par force brute ou les attaques de type DDoS.


### **Protocoles de sécurité (côté front-end)**

Le front-end d'une application web doit respecter plusieurs protocoles de sécurité afin d'assurer la protection des utilisateurs et des données échangées. Ces protocoles permettent de sécuriser les communications, de protéger contre des attaques courantes et de garantir l'intégrité des ressources chargées.

- **HTTP + TLS = HTTPS**  
  L'utilisation de **HTTPS** combine le protocole HTTP avec **TLS (Transport Layer Security)** pour chiffrer les communications entre le navigateur et le serveur. Cela empêche quiconque d'intercepter ou de modifier les données en transit.

  **Cela permet de se protéger contre :**
  - **Écoutes clandestines** : Le chiffrement via TLS empêche les attaquants d'intercepter des données sensibles (comme des mots de passe ou des informations personnelles) en transit.
  - **Attaques man-in-the-middle (MITM)** : HTTPS empêche les attaquants de manipuler les communications entre le client et le serveur.

- **HSTS (HTTP Strict Transport Security)**  
  **HSTS** est une politique de sécurité que le serveur impose au navigateur, garantissant que seules les connexions HTTPS sont utilisées pour toutes les communications futures avec ce domaine. Une fois qu'un site a activé HSTS, les requêtes HTTP non sécurisées sont automatiquement converties en HTTPS.

  **Cela permet de se protéger contre :**
  - **Attaques de type downgrade** : HSTS empêche les attaquants de forcer une connexion HTTP non sécurisée (SSL stripping), en s'assurant que seules les connexions HTTPS sont acceptées.
  - **Exposition accidentelle de données** : HSTS force les connexions HTTPS, même si l'utilisateur essaie de se connecter via HTTP par erreur.

- **TLS (Transport Layer Security)**  
  **TLS** est un protocole de chiffrement utilisé pour sécuriser les communications entre les utilisateurs et le serveur. En plus d’assurer la confidentialité, il garantit l’intégrité des données échangées et l’authentification du serveur.

  **Cela permet de se protéger contre :**
  - **Écoutes et altérations** : TLS empêche les attaquants d'écouter ou de modifier les communications en cours entre le navigateur et le serveur.

- **SOP (Same-Origin Policy)**  
  La **politique de même origine** est un mécanisme de sécurité des navigateurs qui limite l'accès des scripts provenant d'une page web à des ressources d'autres origines (domaine, protocole, port). Cette politique garantit qu'une page web ne peut interagir qu'avec des ressources provenant de la même origine, protégeant ainsi les données des utilisateurs.

  **Cela permet de se protéger contre :**
  - **Attaques cross-origin** : SOP empêche les sites malveillants d'accéder aux ressources sensibles d'un autre site via des scripts malveillants.

- **CSP (Content Security Policy)**  
  La **Content Security Policy** permet de contrôler quelles ressources (scripts, styles, images, etc.) peuvent être chargées par une application web. Elle définit quelles sources de contenu sont autorisées, empêchant ainsi le chargement de ressources non approuvées.

  **Cela permet de se protéger contre :**
  - **Attaques XSS (Cross-Site Scripting)** : CSP empêche l’exécution de scripts non approuvés ou malveillants injectés dans la page web.
  - **Exécution de ressources non sécurisées** : CSP garantit que seules les ressources provenant de domaines de confiance peuvent être chargées et exécutées dans l'application.

- **Referrer Policy**  
  La **Referrer Policy** contrôle quelles informations sur la page d'origine (URL) sont transmises lors d'une requête HTTP vers un autre site. Elle peut limiter la quantité d'informations envoyées dans l'en-tête `Referer`, protégeant ainsi la confidentialité de l'utilisateur.

  **Cela permet de se protéger contre :**
  - **Fuite d'informations** : Limite la divulgation de l'URL complète de la page d'origine, qui pourrait contenir des informations sensibles comme des jetons ou des paramètres privés.
  - **Traçage et identification** : Réduit les risques de traçage en limitant la quantité d’informations sur l’utilisateur partagée avec d’autres sites.

- **SRI (Subresource Integrity)**  
  **SRI** est une fonctionnalité de sécurité permettant de s'assurer que les fichiers externes (comme les scripts ou les styles CSS) n'ont pas été modifiés depuis leur publication. En ajoutant un hash cryptographique à la balise de ressource, le navigateur peut vérifier que le fichier téléchargé est bien celui attendu.

  **Cela permet de se protéger contre :**
  - **Manipulation de ressources externes** : SRI garantit que les ressources externes n’ont pas été compromises ou modifiées par un attaquant après leur publication.
  - **Injections malveillantes** : Empêche les scripts externes modifiés de s'exécuter si leur intégrité ne correspond pas à celle attendue par le navigateur.
